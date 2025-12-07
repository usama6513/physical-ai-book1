---
description: "Executable task list for Physical AI Book Structure and Lesson Design"
---

# Tasks: Physical AI Book Structure and Lesson Design

**Input**: Design documents from `/specs/1-book-structure/`
**Prerequisites**: plan.md (required), spec.md (required for user stories)

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story. Tests are OPTIONAL and included here based on specification requirements.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Project initialization, Docusaurus setup, and repository structure

**Duration**: 2-3 days | **Blocking for**: All subsequent phases

- [ ] T001 Initialize Docusaurus 3.x project at repo root with `npx create-docusaurus@latest`
- [ ] T002 [P] Configure MDX support in docusaurus.config.js (enable @docusaurus/preset-classic with remarkPlugins and rehypePlugins)
- [ ] T003 [P] Create repository structure: docs/, examples/, experiments/, .specify/ directories per plan.md
- [ ] T004 [P] Initialize Node project root: create package.json with Docusaurus, React, Jest, and build tool dependencies
- [ ] T005 [P] Initialize Python examples: create examples/requirements.txt and examples/chapter-1/ subdirectories
- [ ] T006 [P] Configure ESLint and Prettier for JS/React code in experiments/
- [ ] T007 [P] Configure pytest for Python examples in examples/
- [ ] T008 Create .gitignore for node_modules/, build artifacts, and .env files
- [ ] T009 [P] Set up GitHub Actions workflows in .github/workflows/:
  - [ ] T009a create build.yml (run `npm run build` on every push)
  - [ ] T009b create test-examples.yml (run pytest + Jest on every push)
  - [ ] T009c create accessibility.yml (run Lighthouse and axe scans)
- [ ] T010 Create root README.md with project overview, quickstart instructions, and local development setup

**Checkpoint**: Docusaurus dev server runs (`npm run start`); directory structure matches plan.md; CI/CD pipelines configured

---

## Phase 2: Foundational & Shared Components

**Purpose**: Core infrastructure that MUST be complete before ANY user story can be implemented

**Duration**: 3-4 days | **Blocks**: All user stories

**⚠️ CRITICAL**: No user story work can begin until this phase is complete

- [ ] T011 [P] Create Docusaurus configuration: docusaurus.config.js with MDX preset, theme color, dark mode, and sidebar plugin
- [ ] T012 [P] Create sidebars.js with navigation structure: Introduction → Chapter 1 (3 lessons) → Appendix → Glossary
- [ ] T013 [P] Create docs/intro.md (landing page): 1000-word book overview, key concepts, and navigation guide
- [ ] T014 [P] Create docs/01-chapter-1/_category_.json with chapter metadata (title, position, collapsed state)
- [ ] T015 [P] Create docs/01-chapter-1/overview.md with chapter learning objectives (2-3 per chapter) and time estimates
- [ ] T016 [P] Create docs/02-appendix/glossary.md with 15-20 key terms (sensor, actuator, control loop, feedback, etc.) with definitions and cross-references
- [ ] T017 Create docs/docs-setup.md (Contributing guide): Content standards, MDX patterns, code example formatting, and testing requirements
- [ ] T018 [P] Create docs/CONTRIBUTING.md (Developer guide): How to write lessons, test code examples, and accessibility checklist
- [ ] T019 [P] Create docs/ACCESSIBILITY.md: WCAG 2.1 AA compliance guidelines for content and interactive components
- [ ] T020 [P] Create examples/chapter-1/ subdirectories: lesson-1-sensors/, lesson-2-actuators/, lesson-3-control-loops/
- [ ] T021 [P] Create examples/README.md with instructions for testing all examples locally (Python and JavaScript)
- [ ] T022 [P] Create examples/Makefile or npm scripts for:
  - [ ] T022a run all Python tests (`pytest examples/`)
  - [ ] T022b run all JS tests (`npm test` in experiments/)
  - [ ] T022c validate code examples work standalone
- [ ] T023 [P] Create experiments/ directory structure: sensor-simulator/, actuator-visualizer/, control-loop-viz/ (each with src/, tests/ subdirs)
- [ ] T024 Create experiments/README.md with React component development setup and Jest testing guide
- [ ] T025 [P] Create experiments/package.json with React, ReactDOM, Jest, and visualization dependencies (Three.js, Plotly.js)
- [ ] T026 Set up component testing infrastructure in experiments/ (Jest config, testing utilities, mock data)
- [ ] T027 [P] Create base CSS/theme files in docs/ for syntax highlighting and component styling consistency
- [ ] T028 Create docs/lesson-template.mdx as reference template showing proper MDX structure, code block patterns, and component import examples

**Checkpoint**: Docusaurus builds without errors (`npm run build`); all docs render; navigation structure complete; accessibility baseline established; all CI/CD pipelines passing

---

## Phase 3: User Story 1 - Beginner Learns Fundamentals Through Hands-On Experiments (Priority: P1) 🎯 MVP

**Goal**: Create Lesson 1 (Sensor Basics) that demonstrates hands-on learning with working code, interactive visualization, and guided experiment.

**Independent Test**:
1. Lesson loads in Docusaurus without errors
2. Copy-paste Python example runs locally without modification
3. Interactive sensor simulator component renders and responds to user input (parameter sliders)
4. Beginner can complete guided experiment with clear success criteria
5. PDF export renders lesson content, code, and visualization

### Implementation for User Story 1

#### Content Development (Lesson 1: Sensor Basics)

- [ ] T029 [US1] Create docs/01-chapter-1/01-lesson-1-sensors.mdx (skeleton) with YAML front matter:
  - Title: "Lesson 1: Sensor Basics"
  - Learning objectives: (2-3 measurable outcomes)
  - Estimated time: read 10 min, code 15 min, experiment 20 min
  - Prerequisites: none
  - Difficulty: Beginner → Intermediate → Advanced
- [ ] T030 [P] [US1] Write "Conceptual Overview" section (500-800 words): What is a sensor? Explain in everyday language with metaphors (e.g., "sensor is like your nose detecting changes"). No code yet.
- [ ] T031 [P] [US1] Write "Beginner Section" (300-400 words): Simple explanation of sensor types (digital vs. analog), basic properties (sensitivity, range, accuracy), and one foundational example
- [ ] T032 [P] [US1] Write "Intermediate Section" (400-600 words): Implementation details of sensor reading, signal conditioning, and calibration. Include inline diagrams or charts showing signal patterns.
- [ ] T033 [P] [US1] Write "Advanced Section" (300-500 words): Signal processing theory (sampling, quantization, noise), sensor fusion concepts, and references to research papers or textbooks
- [ ] T034 [US1] Write "Guided Experiment" section with 5-step project:
  - Step 1: Set up sensor simulator
  - Step 2: Read 10 sensor samples
  - Step 3: Calculate moving average
  - Step 4: Visualize results
  - Step 5: Verify output matches expected values
- [ ] T035 [US1] Write "Reflection Prompt": "In your own words, explain what a sensor does and why it's important for physical AI. Describe a sensor you use in your daily life (e.g., phone accelerometer, camera) and what it measures."

#### Python Code Example (Lesson 1)

- [ ] T036 [P] [US1] Create examples/chapter-1/lesson-1-sensors/sensor_basics.py with:
  - Function to simulate sensor reading (digital and analog)
  - Function to read N samples and return as list
  - Function to calculate moving average
  - Clear inline comments explaining each function ("why" and "what")
  - Example output in docstring
- [ ] T037 [P] [US1] Create examples/chapter-1/lesson-1-sensors/requirements.txt with pinned versions:
  - numpy==1.24.0
  - matplotlib==3.8.0
  - Other dependencies as needed
- [ ] T038 [P] [US1] Create examples/chapter-1/lesson-1-sensors/test_sensor_basics.py with pytest tests:
  - Test sensor reading returns within valid range
  - Test moving average calculation
  - Test edge cases (empty list, single value, outliers)
  - Target: ≥80% code coverage
- [ ] T039 [US1] Create examples/chapter-1/lesson-1-sensors/README.md with:
  - Execution instructions: `python sensor_basics.py`
  - Expected output sample
  - Explanation of what the code does
  - Prerequisites (Python 3.9+, pip install -r requirements.txt)
- [ ] T040 [US1] Verify all Python tests pass locally: `pytest examples/chapter-1/lesson-1-sensors/test_sensor_basics.py -v`

#### React Interactive Component (Sensor Simulator)

- [ ] T041 [P] [US1] Create experiments/sensor-simulator/SensorSimulator.jsx with React component:
  - Parameter sliders: sensor range (0-100), noise level (0-10), sampling rate (1-100 Hz)
  - Real-time graph showing sensor readings vs. time
  - Input field for manual test value
  - Reset button to restore defaults
  - Clear labels and units (e.g., "Sensor Range (units)")
- [ ] T042 [P] [US1] Create experiments/sensor-simulator/utils/sensorCalculations.js with:
  - Function to generate sensor reading with noise
  - Function to apply filtering/smoothing
  - Helper functions for state calculations
  - Unit tests for each function
- [ ] T043 [P] [US1] Create experiments/sensor-simulator/SensorSimulator.test.jsx with Jest tests:
  - Test component renders without crashing
  - Test parameter sliders update state
  - Test graph updates when parameters change
  - Test reset button restores defaults
  - Target: ≥80% component coverage
- [ ] T044 [US1] Create experiments/sensor-simulator/README.md with development instructions and component API documentation
- [ ] T045 [US1] Verify React tests pass: `npm test -- SensorSimulator.test.jsx` (from experiments/ directory)

#### Integration (Lesson 1 into Docusaurus)

- [ ] T046 [US1] Add import statement to docs/01-chapter-1/01-lesson-1-sensors.mdx:
  ```javascript
  import SensorSimulator from '@site/experiments/sensor-simulator/SensorSimulator';
  ```
- [ ] T047 [US1] Add component instance in Intermediate section of lesson:
  ```javascript
  <SensorSimulator />
  ```
- [ ] T048 [US1] Add code example block to lesson showing Python code with language tag:
  ```markdown
  ```python
  // Content from sensor_basics.py
  ```
  ```
- [ ] T049 [US1] Add links in lesson to:
  - examples/chapter-1/lesson-1-sensors/README.md (to run locally)
  - examples/chapter-1/lesson-1-sensors/test_sensor_basics.py (to see tests)
- [ ] T050 [US1] Build Docusaurus and verify lesson renders without errors: `npm run build`
- [ ] T051 [US1] Verify PDF export works: Check that lesson content, code, and component all render in static export

#### Testing & Validation (User Story 1)

- [ ] T052 [US1] Run manual user test: Have someone unfamiliar with code work through Lesson 1:
  - Read conceptual overview → understand sensor concept?
  - Run Python example locally → code works without errors?
  - Interact with simulator → understand cause-effect relationship?
  - Complete guided experiment → can verify results match expected output?
  - Document feedback and iterate if needed
- [ ] T053 [US1] Verify accessibility of interactive component:
  - Keyboard navigation on sliders
  - Color contrast on graph (WCAG AA compliant)
  - Screen reader compatibility on labels
  - Run Lighthouse accessibility audit (target score ≥90)

**Checkpoint**: User Story 1 is fully functional and independently testable. Lesson loads, code runs, component is interactive, experiment is completable. Ready to demo or deploy.

---

## Phase 4: User Story 2 - Intermediate Developer Extends Examples and Explores Advanced Topics (Priority: P2)

**Goal**: Create Lesson 2 (Actuators) with clear code comments and advanced theory, enabling intermediate learners to understand implementation details and modify examples.

**Independent Test**:
1. Lesson loads in Docusaurus
2. Python AND JavaScript code examples both run locally without modification
3. Code comments enable understanding of implementation details
4. Intermediate learner can successfully modify example (verified by working modified code)
5. Advanced section provides deeper theory without requiring prior re-explanation

### Implementation for User Story 2

#### Content Development (Lesson 2: Actuators)

- [ ] T054 [P] [US2] Create docs/01-chapter-1/02-lesson-2-actuators.mdx with same structure as Lesson 1:
  - Conceptual overview (500-800 words)
  - Beginner section (simple motor/servo explanation)
  - Intermediate section (PWM control, driving signals, with commented code)
  - Advanced section (motor theory, efficiency, control algorithms)
  - Guided experiment (control actuator output)
  - Reflection prompt
- [ ] T055 [US2] Write "Intermediate Section" emphasizing well-commented code: Each code block should have comments explaining "why" this line exists, not just "what" it does

#### Python Code Example (Lesson 2)

- [ ] T056 [P] [US2] Create examples/chapter-1/lesson-2-actuators/actuator_control.py with:
  - Actuator simulation class (motor, servo, or linear actuator)
  - PWM (Pulse Width Modulation) control function with detailed comments
  - Position/velocity/torque calculations
  - Clear variable names and function signatures
- [ ] T057 [P] [US2] Create examples/chapter-1/lesson-2-actuators/requirements.txt with pinned versions
- [ ] T058 [P] [US2] Create examples/chapter-1/lesson-2-actuators/test_actuator_control.py with pytest tests (≥80% coverage)
- [ ] T059 [US2] Create examples/chapter-1/lesson-2-actuators/README.md with execution instructions

#### JavaScript Code Example (Lesson 2)

- [ ] T060 [P] [US2] Create examples/chapter-1/lesson-2-actuators/actuator_control.js with:
  - Same functionality as Python version (for web-based learners)
  - Clear, well-commented code for intermediate learners
  - Export functions for Jest testing
- [ ] T061 [P] [US2] Create examples/chapter-1/lesson-2-actuators/package.json with JS dependencies
- [ ] T062 [P] [US2] Create examples/chapter-1/lesson-2-actuators/actuator_control.test.js with Jest tests (≥80% coverage)

#### React Interactive Component (Actuator Visualizer)

- [ ] T063 [P] [US2] Create experiments/actuator-visualizer/ActuatorVisualizer.jsx with React component:
  - Real-time visualization of actuator output (position, velocity, torque)
  - Parameter control: input command, feedback type (position/velocity), response time
  - Graph showing commanded vs. actual output
  - Comparison view (ideal response vs. realistic with delays/constraints)
- [ ] T064 [P] [US2] Create experiments/actuator-visualizer/utils/actuatorCalculations.js with physics calculations
- [ ] T065 [P] [US2] Create experiments/actuator-visualizer/ActuatorVisualizer.test.jsx with Jest tests (≥80% coverage)

#### Integration (Lesson 2 into Docusaurus)

- [ ] T066 [US2] Add import and component instance to docs/01-chapter-1/02-lesson-2-actuators.mdx
- [ ] T067 [US2] Add both Python and JavaScript code examples to lesson with language tags
- [ ] T068 [US2] Add links to code examples and tests in lesson
- [ ] T069 [US2] Build and verify: `npm run build` (Lesson 2 should render without errors)

#### Testing & Validation (User Story 2)

- [ ] T070 [US2] Run manual test: Have intermediate developer attempt to modify Python example (e.g., change PWM frequency) and verify modified code works
- [ ] T071 [US2] Verify accessibility of ActuatorVisualizer component (keyboard, color contrast, screen reader)

**Checkpoint**: User Story 2 is functional. Lessons 1 AND 2 both load, code examples work, intermediate learners can extend. Ready for incremental deployment.

---

## Phase 5: User Story 3 - Instructor Uses Book as Course Material with Clear Learning Objectives (Priority: P3)

**Goal**: Create Lesson 3 (Control Loops) with clear learning objectives, time estimates, and instructor guidance. Enable full chapter PDF export.

**Independent Test**:
1. Lesson 3 loads in Docusaurus
2. Code example (Python) runs locally
3. Interactive component renders and is interactive
4. Chapter-level PDF export completes without errors and includes all lessons
5. Instructor can view lesson objectives and time estimates for planning

### Implementation for User Story 3

#### Content Development (Lesson 3: Control Loops)

- [ ] T072 [P] [US3] Create docs/01-chapter-1/03-lesson-3-control-loops.mdx with:
  - Learning objectives (clearly measurable)
  - Time estimate breakdown (read: 15 min, code: 20 min, experiment: 25 min)
  - Prerequisites: "Understand sensors (Lesson 1) and actuators (Lesson 2)"
  - Conceptual overview (closed-loop feedback, PID controller, stability)
  - Beginner section (simple feedback loop)
  - Intermediate section (PID implementation with detailed comments)
  - Advanced section (control theory, stability analysis, tuning methods)
  - Guided experiment (tune PID controller to achieve target setpoint)

#### Python Code Example (Lesson 3)

- [ ] T073 [P] [US3] Create examples/chapter-1/lesson-3-control-loops/pid_controller.py with:
  - PID controller class (P, I, D components with clear comments)
  - Simulation of control loop (sensor read → compute error → apply control → repeat)
  - Well-commented implementation explaining each component
- [ ] T074 [P] [US3] Create examples/chapter-1/lesson-3-control-loops/requirements.txt
- [ ] T075 [P] [US3] Create examples/chapter-1/lesson-3-control-loops/test_pid_controller.py with pytest tests (≥80% coverage)
- [ ] T076 [US3] Create examples/chapter-1/lesson-3-control-loops/README.md

#### React Interactive Component (Control Loop Visualizer)

- [ ] T077 [P] [US3] Create experiments/control-loop-viz/ControlLoopViz.jsx with React component:
  - Real-time visualization of control loop:
    - Setpoint (target value)
    - Sensor feedback (actual value)
    - PID output (control signal)
    - Error over time
  - Parameter sliders: Kp (proportional), Ki (integral), Kd (derivative)
  - Live tuning: Adjust PID values and see effect on control performance
  - Success indicator: System reaches setpoint within tolerance
- [ ] T078 [P] [US3] Create experiments/control-loop-viz/utils/pidCalculations.js with PID math
- [ ] T079 [P] [US3] Create experiments/control-loop-viz/ControlLoopViz.test.jsx with Jest tests (≥80% coverage)

#### Integration (Lesson 3 into Docusaurus)

- [ ] T080 [US3] Add import and component to docs/01-chapter-1/03-lesson-3-control-loops.mdx
- [ ] T081 [US3] Add code examples and links to lesson
- [ ] T082 [US3] Build and verify: `npm run build`

#### Instructor Features

- [ ] T083 [US3] Update docs/01-chapter-1/overview.md with:
  - Chapter-level learning objectives (aggregate from all 3 lessons)
  - Time estimates (total: ~2 hours for full chapter; breakdown per lesson)
  - Lab setup requirements (for hands-on experiments)
  - Assessment rubric (how to verify student completion)
- [ ] T084 [US3] Add docs/INSTRUCTOR_GUIDE.md with:
  - How to use book in course (pacing suggestions, assessment strategies)
  - Answer key or solution sketches for guided experiments
  - Links to lab equipment recommendations (but hardware-agnostic)
- [ ] T085 [US3] Verify PDF export works: `npm run docusaurus build -- --out-dir build_pdf` and export to PDF (all 3 lessons, chapter overview, glossary)
- [ ] T086 [US3] Validate PDF rendering (all text, code, visuals render legibly; no broken links)

#### Testing & Validation (User Story 3)

- [ ] T087 [US3] Manual test with educator: Verify they can:
  - View chapter learning objectives
  - See time estimates and prerequisites
  - Download full chapter as PDF
  - Plan a 2-hour lab session using the lesson material
- [ ] T088 [US3] Verify all 3 lessons load together without conflicts

**Checkpoint**: All user stories are complete and independently functional. Full chapter is ready for release or demo to stakeholders.

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Improvements affecting multiple user stories, final validation, and deployment preparation

**Duration**: 2-3 days | **Blocking for**: Release

- [ ] T089 [P] Validate all internal links in Docusaurus (no broken link checker or manual review)
- [ ] T090 [P] Run accessibility audit (Lighthouse, axe DevTools) on all lesson pages and interactive components (target: ≥90 score)
- [ ] T091 [P] Run full test suite:
  - [ ] T091a `npm run test` (Jest for React components)
  - [ ] T091b `pytest examples/` (pytest for Python code)
  - [ ] T091c Verify all tests pass and coverage ≥80%
- [ ] T092 [P] Verify Docusaurus build completes in <30 seconds: `npm run build`
- [ ] T093 [P] Run spelling and grammar check on all lesson content (automated tool + manual review)
- [ ] T094 [P] Mobile responsiveness check: Test site on iPhone and Android browsers (code blocks, graphs, sliders all readable)
- [ ] T095 Validate offline capability: Ensure core docs can be downloaded as PDF and code examples run offline
- [ ] T096 [P] Add deployment metadata: Update package.json version and docusaurus.config.js version to 0.1.0 (first release)
- [ ] T097 Add release notes to docs (RELEASE_NOTES.md): Summary of v0.1.0 content and known limitations
- [ ] T098 Update CONTRIBUTING.md with feedback and issue reporting instructions
- [ ] T099 [P] Set up analytics in Docusaurus config (Google Analytics or equivalent) for tracking engagement
- [ ] T100 Final check: Review spec.md success criteria against actual implementation:
  - [ ] T100a SC-001: Code examples run in Python 3.9+, Node 16+? ✅
  - [ ] T100b SC-002: Pages load <3s, build <30s? ✅
  - [ ] T100c SC-003: Beginner completion target 90%? (Set up feedback collection) ✅
  - [ ] T100d SC-004: Intermediate modification success 80%? (Track in community forum) ✅
  - [ ] T100e SC-005: PDF export works? ✅
  - [ ] T100f SC-006: Build + links validated? ✅
  - [ ] T100g SC-007: Mobile responsive? ✅
  - [ ] T100h SC-008: WCAG AA compliance? ✅
  - [ ] T100i SC-009: Code coverage ≥80%? ✅

**Checkpoint**: All user stories complete, all tests pass, accessibility verified, deployment ready

---

## Dependencies & Execution Order

### Phase Dependencies

```
Phase 1: Setup (Shared Infrastructure)
    ↓
Phase 2: Foundational (Blocking Prerequisites)
    ↓
Phase 3: User Story 1 (P1) ← CRITICAL for MVP
    ↓
Phase 4: User Story 2 (P2) [Can start after Phase 3 basics established]
    ↓
Phase 5: User Story 3 (P3) [Can start after Phase 4 basics established]
    ↓
Phase 6: Polish & Cross-Cutting Concerns
```

### User Story Dependencies

- **User Story 1 (P1)**: Starts after Phase 2 - No dependencies on other stories
- **User Story 2 (P2)**: Starts after Phase 2 - Can run parallel with US1 after US1 content structure validated
- **User Story 3 (P3)**: Starts after Phase 2 - Can run parallel with US1+US2 after their patterns established

### Within Each User Story

- Content development (writing) before code
- Python code before JavaScript variant
- Code before React component
- Component tests before integration into Docusaurus
- All tests passing before integration

### Parallel Opportunities

**Phase 1 (Setup)**: All [P] tasks can run in parallel
**Phase 2 (Foundational)**: All [P] tasks can run in parallel
**Phase 3+ (User Stories)**:
- Different user stories CAN run in parallel if staffed (different developers)
- Within each story: Content, code, and components can proceed in parallel (different developers) once structure established

### Example: Parallel Execution with 3 Developers

**Week 1-2 (All developers)**:
- Complete Phase 1: Setup
- Complete Phase 2: Foundational

**Week 2-3+ (Parallel)**:
- Developer A: Phase 3 (Lesson 1) → Lesson 1 content, Python code, SensorSimulator component
- Developer B: Phase 4 (Lesson 2) → Lesson 2 content, Python + JS code, ActuatorVisualizer component
- Developer C: Phase 5 (Lesson 3) → Lesson 3 content, Python code, ControlLoopViz component

**Week 4+ (Serial or Overlapped)**:
- All developers: Phase 6 (Polish) → final validation, accessibility, testing

---

## Implementation Strategy

### MVP First (User Story 1 Only) - Recommended for v0.1.0

1. ✅ Complete Phase 1: Setup (T001-T010)
2. ✅ Complete Phase 2: Foundational (T011-T028)
3. ✅ Complete Phase 3: User Story 1 (T029-T053) 🎯
4. ⏸️ **STOP and VALIDATE**: Test Lesson 1 independently
5. ✅ Optional: Deploy/demo Lesson 1 to gather feedback
6. ➡️ **Next**: Add US2 and US3 based on feedback

**Time to MVP**: ~10-12 days (2 weeks)

### Incremental Delivery (Full v0.1.0)

1. Phase 1 + 2: Foundation (foundation ready)
2. Phase 3: Add User Story 1 → Test independently → Deploy (MVP!)
3. Phase 4: Add User Story 2 → Test independently → Deploy (v0.1.1)
4. Phase 5: Add User Story 3 → Test independently → Deploy (v0.1.2)
5. Phase 6: Polish and release as v0.2.0

Each story adds value independently; no story breaks previous stories.

### Single Developer Strategy

1. Complete Phase 1 + 2 sequentially
2. Complete Phase 3 (US1) fully before moving to Phase 4
3. Complete Phase 4 (US2) fully before moving to Phase 5
4. Complete Phase 5 (US3) fully before moving to Phase 6
5. Complete Phase 6 (Polish) and release

**Total time**: ~3-4 weeks for full feature

---

## Task Statistics

| Category | Count |
|----------|-------|
| **Phase 1 (Setup)** | 10 tasks |
| **Phase 2 (Foundational)** | 18 tasks |
| **Phase 3 (User Story 1)** | 25 tasks |
| **Phase 4 (User Story 2)** | 18 tasks |
| **Phase 5 (User Story 3)** | 18 tasks |
| **Phase 6 (Polish)** | 12 tasks |
| **TOTAL** | **101 tasks** |

### Parallelizable Tasks

- **[P] marked tasks**: 65 tasks can potentially run in parallel
- **Serial tasks** (blocked by dependencies): 36 tasks

### By User Story

- **User Story 1 (P1)**: 25 tasks (content, Python code, React component, integration)
- **User Story 2 (P2)**: 18 tasks (content, Python + JS code, React component, integration)
- **User Story 3 (P3)**: 18 tasks (content, Python code, React component, integration, instructor features)

---

## Notes

- Tasks follow strict checklist format: `- [ ] [ID] [P?] [Story?] Description with file path`
- [P] = parallelizable (different files, no cross-task dependencies)
- [Story] = user story label (US1, US2, US3) for traceability
- Stop at any checkpoint to validate story independently
- Commit after each task or logical group (typically 3-5 related tasks)
- Avoid: vague tasks, same file conflicts, cross-story dependencies that break independence
- Each user story should be independently completable and testable before proceeding to next

