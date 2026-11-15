# Development status — Phases 2–5

## Phase 2 — security foundation (prepared, not deployed)
- Added a candidate Firestore ruleset for the collections observed in the current student/admin code.
- Added deployment and security notes.
- **Not certified:** rules have not been deployed or validated with the Firebase Emulator Suite or the owner's live Firebase project.

## Phase 3 — automated testing and application architecture
- Added `package.json` with Node.js test commands.
- Added `tests/syntax-check.cjs` to parse executable inline JavaScript in both HTML entry points.
- Added a Node built-in test suite for app entry points, question-bank integrity, scenario references, six Section A answer formats, Section B tutor-marking structure, practice-engine entry points, absolute-end-time mock timer, dashboard data source, accessibility hooks and Firestore policy structure.
- Added `docs/ARCHITECTURE.md` describing current logical boundaries, target module boundaries, staged refactoring rules and release gates.
- **Validation:** `npm run test:all` passes: 9 tests, 0 failures; 3 inline executable JavaScript blocks parse successfully.
- The 2.2 MB monolithic page has not yet been split into modules; it remains intact as the rollback baseline to avoid an untested rewrite.

## Phase 4 — premium UI/UX and design system
- Added design tokens for spacing, radii, focus rings and translucent surfaces.
- Added glass-style sticky navigation treatment, subtle card interactions, keyboard focus states, responsive navigation/pulse layout and reduced-motion handling.
- Preserved existing theme variables and existing practice component semantics.

## Phase 5 — student dashboard and advanced practice engine
- Added a weekly Section A learning-pulse panel based on actual `ST.log` entries, including attempt count, accuracy, active days and daily activity bars.
- Added accessible labels for the activity chart and a timer role for the per-question timer.
- Preserved the existing six Section A answer formats and existing Section B tutor-marking workflow.
- Preserved existing mock exam timer behavior, which stores an absolute end timestamp and derives remaining time from the current time.
- Corrected the home-screen storage note to distinguish browser persistence from optional account/cloud sync.

## Not completed / not claimed
- No full browser-driven Playwright interaction suite has been run. A local headless Chromium smoke attempt did not complete within the execution window, so runtime rendering is not certified by this pass.
- No Firebase Emulator Suite tests, live sign-in, cross-device sync, Firestore deployment, EmailJS delivery, PDF hosting verification or production deployment were performed.
- The product remains AA-focused. It is not yet the requested 50+ page multi-paper public platform.
- No new official ACCA question content has been added. Existing question data and supplied learning resources were preserved.

## Next steps
1. Add Playwright browser tests and run them against a local HTTP server with deterministic Firebase test configuration.
2. Run Firebase Emulator security tests for student isolation and admin authorization before deploying rules.
3. Extract embedded question data into a validated JSON module, with count/ID parity tests.
4. Extract pure practice-domain logic into tested modules before changing the UI layer.
5. Continue dashboard improvements for Section B and cross-device state reconciliation.
6. Build the wider public/SEO site and multi-paper architecture only after the current AA product is regression protected.
