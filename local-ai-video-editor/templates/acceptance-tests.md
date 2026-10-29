# Acceptance tests

## M1 local orchestrator
- [ ] Starts and stops without administrator privileges.
- [ ] Listens on loopback only; refuses remote clients.
- [ ] Rejects invalid jobs and paths outside authorized roots.
- [ ] Tracks QUEUED, RUNNING, REVIEW_REQUIRED, FAILED, CANCELLED.
- [ ] Does not modify source footage.

## M2–M4 offline AI and editor UI
- [ ] Sample media transcription runs without external inference calls.
- [ ] Human can inspect and correct transcription.
- [ ] UXP panel is tested in installed Premiere version.
- [ ] Proposed edits remain editable/non-destructive.
- [ ] Failure does not damage the original Premiere project.

## M5–M6 approval and release
- [ ] Reviewer explicitly approves a specific version and SHA-256.
- [ ] Any modification invalidates approval.
- [ ] Export is blocked without matching approval record.
- [ ] Auditable reviewer and timestamp are saved.
- [ ] An operator can revert to the previous accepted state.

## M7
- [ ] Backups and rollback tested.
- [ ] No confidential media contents in application logs.
- [ ] Network traffic reviewed for unexpected outbound requests.
