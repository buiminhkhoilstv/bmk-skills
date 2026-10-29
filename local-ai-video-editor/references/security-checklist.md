# Security and safety checklist

- [ ] All production AI inference executes locally.
- [ ] No source media, transcript, confidential prompts, or metadata sent to cloud AI providers.
- [ ] API binds to `127.0.0.1` only; authenticate and narrowly restrict clients.
- [ ] Canonicalize media paths; reject traversal and paths outside allowed roots.
- [ ] Allowlist executable programs and arguments; avoid shell injection.
- [ ] Protect source media as read-only; retain checksums.
- [ ] Separate working, export, approval, and log directories.
- [ ] Never log raw transcripts or confidential media contents by default.
- [ ] Approval stores exact SHA-256, version, path, sequence, reviewer, timestamp.
- [ ] Export fails closed if artifact/version/hash differs from approval.
- [ ] Explicit human approval before release; no automatic publishing.
- [ ] Lock/pin dependencies and review model licenses.
- [ ] Document offline restore, backup, error handling, and rollback procedures.
- [ ] Verify Adobe UXP capabilities with official docs and practical tests.
