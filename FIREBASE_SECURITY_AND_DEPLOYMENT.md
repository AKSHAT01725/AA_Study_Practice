# Firebase security and deployment notes

## Current project integration
The existing application uses Firebase Authentication and Cloud Firestore. The inspected client code accesses these paths:

- `users/{uid}` — student profile and summary statistics
- `users/{uid}/aaStudyHubProgress/current` — synchronised AA practice state
- `attempts/{attemptId}` — individual practice attempts
- `gradings/{gradingId}` — tutor/admin marking records, queried by `uid`
- `pdfs/{pdfId}` — shared resource links
- `config/planner` — shared exam date/time

## Administrator identities
The current frontend allow-list contains:
- `akshat.y.shah1725@gmail.com`
- `yateseducationaccaresource@gmail.com`

The Firestore rules require a verified Firebase email claim and one of these addresses. Keep the frontend and backend lists identical. For a larger deployment, migrate to custom claims assigned by a trusted server rather than relying on an email allow-list.

## Critical deployment sequence
1. Export/back up current Firestore data and rules.
2. Review `firestore.rules` with the project owner.
3. Test using Firebase Emulator Suite or a non-production Firebase project.
4. Verify a student cannot list all users, read another student's progress/attempts, create grading records, modify the shared planner, or write protected user fields.
5. Verify an administrator can manage students, attempts, grading records, PDFs and planner configuration.
6. Publish rules only after those tests pass.

## Known limitations / items requiring owner configuration
- No live Firebase project was connected during this development pass; deployment and cross-device sync remain unverified.
- Firebase Authentication provider settings and authorised domains must be checked in the owner's console.
- The email allow-list is suitable as an immediate restriction for the current small project, but custom claims backed by a trusted server are preferable for enterprise administration.
- Existing account progress uses browser local storage as a local cache plus Firestore cloud sync. Local storage is not the permanent cross-device source of truth.
- No automated emulator security tests have been run in this environment.

## Pre-production acceptance checklist
- [ ] Student A can sign in and sync progress.
- [ ] Student A cannot read Student B's profile or progress.
- [ ] Student A cannot read Student B's attempts or grading.
- [ ] Student A cannot create/update/delete PDFs or planner configuration.
- [ ] Student A cannot grant themselves admin or unban themselves.
- [ ] Admin can view student list and attempts.
- [ ] Admin can publish grades and manage PDFs/planner.
- [ ] Sign-out clears the local account state as intended.
- [ ] Same student account restores progress on a second device.
