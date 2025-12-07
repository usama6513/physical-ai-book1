# Implementation Plan: Physical AI Book Structure and Lesson Design

**Branch**: `1-book-structure` | **Date**: 2025-12-07 | **Spec**: [spec.md](spec.md)
**Input**: Feature specification from `/specs/1-book-structure/spec.md`

## Summary

Build a production-ready Docusaurus-based documentation site for the Physical AI book. The initial release includes a single chapter with 3 hands-on lessons (Sensor Basics, Actuators, Control Loops), each featuring runnable Python/JavaScript code examples, interactive visualizations, and guided experiments. The implementation prioritizes beginner-friendly learning through progressive difficulty levels (Beginner/Intermediate/Advanced), tested code examples, and interactive components that allow real-time parameter exploration.

## Technical Context

**Language/Version**: Python 3.9+ (primary examples), JavaScript/TypeScript with React (interactive components)
**Primary Dependencies**: Docusaurus 3.x, MDX, Matplotlib/Three.js (visualization), pytest (Python testing), Jest (JS testing), ROS 2 (simulation environment)
**Storage**: Static file-based (Docusaurus generates static HTML); code examples use local file I/O
**Testing**: pytest for Python examples, Jest for JavaScript/React components, Cypress for end-to-end Docusaurus site validation
**Target Platform**: Web browsers (Chrome, Firefox, Safari); mobile responsive (iOS Safari, Android Chrome)
**Project Type**: Web documentation site with embedded code examples and interactive components
**Performance Goals**: Load pages in <3 seconds; Docusaurus build completes in <30 seconds; interactive components render without lag (60 fps)
**Constraints**: WCAG 2.1 AA accessibility; offline-capable core content; <100MB total site size; open-source tooling only
**Scale/Scope**: 1 chapter, 3 lessons, 3 code examples per lesson (Python + JS variants), 3 interactive components, 3 guided experiments

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

### Principles Alignment

✅ **I. Hands-On Learning (Non-Negotiable)**
- Every lesson includes runnable code example + interactive component + guided experiment
- Code is production-ready, tested, and immediately executable
- No abstract theory without practical application

✅ **II. Progressive Difficulty**
- Each lesson structured with Beginner/Intermediate/Advanced sections
- Clearly marked difficulty levels and prerequisites
- Content flows linearly from sensors → actuators → control loops

✅ **III. Clear Abstraction Boundaries**
- Three content levels per lesson: intuition (Beginner), implementation (Intermediate), math (Advanced)
- Beginner can understand core concept; Advanced readers access deeper theory
- Each section builds on prior knowledge without redundant re-explanation

✅ **IV. Code Quality and Reproducibility**
- All code examples include inline comments explaining "why" and "what"
- Dependencies pinned to specific versions (requirements.txt, package.json)
- Every example includes unit tests (pytest for Python, Jest for JS)
- Tested in documented environments (Python 3.9+, Node 16+)

✅ **V. Interactivity and Experimentation**
- Each lesson includes interactive component (parameter sliders, real-time graphs)
- Guided experiments with step-by-step instructions and success criteria
- Learners can observe cause-effect relationships in real-time

✅ **VI. Inclusive and Accessible Language**
- Metaphors from everyday experience (e.g., "sensor like your nose")
- WCAG 2.1 AA compliance on all interactive components
- Jargon defined on first use; multiple learning styles supported (text, code, visualization)

### Technology Stack Alignment

✅ **Documentation Platform**: Docusaurus 3.x with MDX support enabled
✅ **Code Examples**: Python (primary) + JavaScript (secondary); version-pinned dependencies
✅ **Testing**: pytest (Python), Jest (JavaScript); ≥80% code coverage
✅ **Simulation & Visualization**: Matplotlib (Python), Three.js (interactive), custom simulators
✅ **Repository Structure**: Matches constitution specification (docs/, examples/, experiments/, .specify/)

### Decision Gate: PASS
No constitution violations detected. Technical context aligns with all 6 core principles and technology stack standards.

## Project Structure

### Documentation (this feature)

```text
specs/1-book-structure/
├── spec.md                      # Feature specification (user stories, requirements, success criteria)
├── plan.md                      # This file (technical design, phasing, architecture)
├── research.md                  # Phase 0 output (design decisions documented)
├── data-model.md                # Phase 1 output (lesson/chapter/content entity definitions)
├── quickstart.md                # Phase 1 output (local development setup guide)
├── contracts/                   # Phase 1 output (content structure contracts/schemas)
│   ├── lesson-schema.json       # Lesson structure validation schema
│   ├── interactive-component-spec.md  # Interactive component interface specification
│   └── code-example-spec.md     # Code example requirements and testing interface
├── checklists/
│   └── requirements.md          # Quality assurance checklist (PASS)
└── tasks.md                     # Phase 2 output (/sp.tasks command - executable task breakdown)
```

### Source Code (repository root)

```text
physical-ai-book/
│
├── docs/                        # Docusaurus content (MDX + MD)
│   ├── intro.md                 # Landing page and book overview
│   ├── 01-chapter-1/            # First chapter on Physical AI Fundamentals
│   │   ├── _category_.json      # Docusaurus sidebar configuration
│   │   ├── 01-lesson-1-sensors.mdx
│   │   ├── 02-lesson-2-actuators.mdx
│   │   └── 03-lesson-3-control-loops.mdx
│   ├── 02-appendix/             # Additional reference material
│   │   └── glossary.md          # Technical term definitions
│   └── docs-setup.md            # Contributing guide (content standards, MDX guidelines)
│
├── examples/                    # Runnable code examples (organized by chapter)
│   ├── chapter-1/
│   │   ├── lesson-1-sensors/
│   │   │   ├── requirements.txt  # Python dependencies (e.g., matplotlib==3.8.0, numpy==1.24.0)
│   │   │   ├── package.json      # JS dependencies (if applicable)
│   │   │   ├── sensor_basics.py  # Main example code
│   │   │   ├── test_sensor_basics.py  # Unit tests (pytest)
│   │   │   └── README.md         # Local execution instructions
│   │   ├── lesson-2-actuators/
│   │   │   ├── requirements.txt
│   │   │   ├── actuator_control.py
│   │   │   ├── test_actuator_control.py
│   │   │   └── README.md
│   │   └── lesson-3-control-loops/
│   │       ├── requirements.txt
│   │       ├── pid_controller.py
│   │       ├── test_pid_controller.py
│   │       └── README.md
│   ├── package.json             # Root JS/Node configuration for all JS examples
│   └── README.md                # Code examples setup and testing guide
│
├── experiments/                 # Interactive simulations and React components
│   ├── sensor-simulator/        # React component: Sensor parameter simulator
│   │   ├── SensorSimulator.jsx   # Main React component
│   │   ├── SensorSimulator.test.jsx  # Jest tests
│   │   ├── utils/
│   │   │   ├── sensorCalculations.js
│   │   │   └── sensorCalculations.test.js
│   │   └── README.md
│   ├── actuator-visualizer/     # React component: Actuator output visualization
│   │   ├── ActuatorVisualizer.jsx
│   │   ├── ActuatorVisualizer.test.jsx
│   │   └── README.md
│   ├── control-loop-viz/        # React component: Control loop feedback visualization
│   │   ├── ControlLoopViz.jsx
│   │   ├── ControlLoopViz.test.jsx
│   │   └── README.md
│   ├── package.json             # React, Three.js, and testing dependencies
│   └── README.md                # Interactive components setup and development guide
│
├── .specify/
│   ├── memory/
│   │   └── constitution.md      # Project constitution (principles, constraints, governance)
│   ├── templates/
│   │   └── (spec, plan, task templates)
│   └── scripts/                 # Automation scripts (referenced by sp.* commands)
│
├── .github/
│   └── workflows/
│       ├── build.yml            # CI/CD: Build Docusaurus site on every commit
│       ├── test-examples.yml    # CI/CD: Test Python/JS examples on every commit
│       └── accessibility.yml    # CI/CD: Run accessibility audit (Lighthouse, axe)
│
├── docusaurus.config.js         # Docusaurus configuration (theme, plugins, sidebar)
├── sidebars.js                  # Docusaurus sidebar navigation structure
├── package.json                 # Root Node dependencies (Docusaurus, build tools)
├── README.md                    # Project overview and quickstart (Getting Started guide)
├── CONTRIBUTING.md              # Contributor guide (content standards, testing, deployment)
└── .gitignore                   # Ignore node_modules, build artifacts, .env files
```

**Structure Decision**: Web documentation site (Option 2: Frontend-focused). Repository splits into three logical zones:
- **docs/**: MDX content files (Docusaurus renders these into HTML pages)
- **examples/**: Executable Python/JavaScript code with tests and local environment setup
- **experiments/**: React components for interactive visualizations (imported into MDX via Docusaurus)

Rationale: This structure enables independent development and testing of content, code examples, and interactive components. Docusaurus pulls from all three zones to generate the final site.

## Implementation Phases

### Phase 1: Setup & Infrastructure
**Duration estimate**: 2-3 days
**Blocking for**: All subsequent phases
**Success criteria**: Docusaurus dev environment runs locally; CI/CD pipelines configured; project structure in place

**Key deliverables**:
- Docusaurus project initialized with MDX support
- GitHub workflows configured (build, test-examples, accessibility)
- Example Python/JavaScript project structures created
- Local development README with setup instructions

**Constitution alignment**: Ensures reproducibility (Principle IV) and accessible development (Principle VI)

---

### Phase 2: Foundational & Shared Components
**Duration estimate**: 3-4 days
**Blocking for**: User story phases
**Success criteria**: Docusaurus builds without errors; navigation structure verified; accessibility baseline met

**Key deliverables**:
- Landing page (docs/intro.md)
- Chapter overview page (docs/01-chapter-1/_category_.json + overview section)
- Glossary page (docs/02-appendix/glossary.md)
- Contributing guide (docs/docs-setup.md)
- Code examples build harness (Makefile or npm scripts to test all examples)
- React component testing setup in experiments/

**Constitution alignment**: Clear abstraction boundaries (Principle III) via navigation and glossary; accessibility baseline (Principle VI)

---

### Phase 3: User Story 1 - Beginner Learns Fundamentals (P1)
**Duration estimate**: 5-7 days
**Priority**: CRITICAL (validates core value proposition)
**Success criteria**:
- Lesson 1 (Sensor Basics) loads in Docusaurus
- Python code example runs without errors
- Interactive sensor simulator component renders and responds to user input
- Guided experiment has clear success criteria
- 90%+ of beginner users report understanding the concept

**Key deliverables**:
- docs/01-chapter-1/01-lesson-1-sensors.mdx (complete lesson with 3 difficulty sections)
- examples/chapter-1/lesson-1-sensors/ (Python code + tests)
- experiments/sensor-simulator/ (React component + tests)
- PDF export validates (lesson content, code, visualization all render)

**Lesson structure**:
1. Learning Objectives (2-3 measurable outcomes)
2. Estimated time (read: 10 min, code: 15 min, experiment: 20 min)
3. Prerequisites (none for first lesson)
4. Conceptual Overview (500-800 words; no code yet)
5. Beginner Section: "What is a sensor?" + simple example + interactive sandbox
6. Intermediate Section: Implementation details + commented code + visualization
7. Advanced Section: Signal processing theory + references + extension challenges
8. Guided Experiment: 5-step project with success criteria
9. Reflection Prompt: "Explain what a sensor does in your own words"

**Constitution alignment**: Hands-on learning (Principle I), progressive difficulty (Principle II), code quality (Principle IV), interactivity (Principle V)

---

### Phase 4: User Story 2 - Intermediate Developer Extends Examples (P2)
**Duration estimate**: 4-5 days
**Priority**: HIGH (validates code clarity and extensibility)
**Success criteria**:
- Lesson 2 (Actuators) complete with 3 difficulty sections
- JavaScript code example provided alongside Python
- Intermediate learner can modify example for their use case
- 80%+ of intermediate users report successful code modification

**Key deliverables**:
- docs/01-chapter-1/02-lesson-2-actuators.mdx
- examples/chapter-1/lesson-2-actuators/ (Python + JavaScript code with tests)
- experiments/actuator-visualizer/ (React component + tests)

**Constitution alignment**: Code quality with clear comments (Principle IV), clear abstraction boundaries (Principle III)

---

### Phase 5: User Story 3 - Instructor Uses Book as Course Material (P3)
**Duration estimate**: 3-4 days
**Priority**: MEDIUM (secondary use case)
**Success criteria**:
- Lesson 3 (Control Loops) complete with 3 difficulty sections
- Chapter-level learning objectives documented
- Time estimates and lab setup guidance available
- PDF export of full chapter validates
- Instructor can extract lessons for their course

**Key deliverables**:
- docs/01-chapter-1/03-lesson-3-control-loops.mdx
- examples/chapter-1/lesson-3-control-loops/ (Python code + tests)
- experiments/control-loop-viz/ (React component + tests)
- Chapter overview with learning objectives and time breakdowns

**Constitution alignment**: Accessibility for educators (Principle VI), clear objectives (Principle II)

---

### Phase 6: Polish & Cross-Cutting Concerns
**Duration estimate**: 2-3 days
**Blocking for**: Release
**Success criteria**:
- All internal links validated (no broken links)
- Accessibility audit passes (WCAG 2.1 AA, Lighthouse ≥90)
- All code examples have ≥80% test coverage
- Site builds and deploys without errors

**Key deliverables**:
- Link validation in CI/CD
- Accessibility testing (automated via Lighthouse/axe)
- Code coverage reporting for examples/
- Deployment verification (staging and production)

**Constitution alignment**: Quality gates (Principle IV), accessibility compliance (Principle VI)

## Dependencies & Phasing Strategy

```
Phase 1 (Setup & Infrastructure)
    ↓
Phase 2 (Foundational & Shared Components)
    ↓
Phase 3 (User Story 1 - P1) ← CRITICAL PATH
    ↓
Phase 4 (User Story 2 - P2) [Can start in parallel with Phase 3 after Week 1]
    ↓
Phase 5 (User Story 3 - P3) [Can start in parallel with Phase 4 after Week 2]
    ↓
Phase 6 (Polish & Cross-Cutting Concerns)
```

## MVP Scope

**Recommended MVP (Minimal Viable Product)**: Phases 1-3 only (Setup + Foundational + User Story 1)

**Why**:
- Validates core value proposition (hands-on learning for beginners)
- Demonstrates Docusaurus integration with interactive components
- Provides proof-of-concept for content structure
- Can be released and gather feedback before investing in US2 & US3

**Time to MVP**: ~10-12 days (2 weeks)

## Parallel Execution Opportunities

- **Weeks 1-2**: Phase 1 (Setup) can proceed independently
- **Week 2-3**: Phase 2 (Foundational) and early Phase 3 (Lesson 1 content outline) can proceed in parallel
- **Week 3+**:
  - Phase 3 (Python example code) can proceed in parallel with Phase 3 (React component design)
  - Phase 4 (Lesson 2 content) can start once Lesson 1 structure is validated
  - Phase 5 (Lesson 3 content) can start once Lessons 1-2 patterns are established

## Complexity Tracking

| Area | Complexity | Mitigation |
|------|-----------|-----------|
| React component library (3 interactive components) | Medium (state management, real-time updates) | Use React hooks for state; leverage Plotly.js or Three.js for visualization; test components in isolation |
| Python example testing across versions | Medium (version compatibility) | Pin all dependencies; test in Docker container for Python 3.9+; CI/CD matrix testing |
| Docusaurus MDX integration with embedded components | Low-Medium (learning curve) | Create reusable component import pattern; document in quickstart.md; test MDX compilation early |
| Accessibility compliance (WCAG 2.1 AA) | Medium (semantic HTML, keyboard navigation, color contrast) | Use Lighthouse/axe in CI/CD; manual review of interactive components; test with screen readers |
| Content review & iteration | Low-Medium (depends on stakeholder feedback) | Plan for 1-2 rounds of community review per lesson; document feedback process in CONTRIBUTING.md |

## Architecture Decisions

### Decision 1: Docusaurus 3.x with MDX
**Chosen**: Docusaurus 3.x + MDX
**Rationale**: Industry-standard documentation platform; native React component support via MDX; excellent for technical content; strong accessibility defaults; active maintenance

### Decision 2: Python (Primary) + JavaScript (Secondary) for Examples
**Chosen**: Python primary (scikit-learn, numpy, matplotlib ecosystem); JavaScript secondary (web-based interactivity)
**Rationale**: Python dominates AI/ML education; JavaScript enables browser-native interactivity; covers both communities

### Decision 3: React for Interactive Components
**Chosen**: React (functional components with hooks)
**Rationale**: Integrates natively with Docusaurus; component model simplifies interactive development; large ecosystem for visualization libraries; testable with Jest

### Decision 4: Three-Level Content Structure (Beginner/Intermediate/Advanced)
**Chosen**: Per-lesson three-level structure
**Rationale**: Enables single lessons to serve multiple audiences; reduces redundancy; learners can self-select depth; aligns with "Clear Abstraction Boundaries" principle

### Decision 5: Static Site + Local Testing (No Backend)
**Chosen**: Docusaurus static generation + local code example testing
**Rationale**: Offline-first capability; reduces operational complexity; enables free hosting; examples test locally before publication

---

**Implementation Ready**: All gates passed. Proceed to `/sp.tasks` for detailed task breakdown.
