---
name: local-ai-video-editor
description: Guide development of a local-first AI-assisted video editor integrated with Adobe Premiere Pro 26.x, human review, and strict media privacy.
---
# Local AI Video Editor v2

## Mission
Build a professional AI-assisted video editing workflow for a broadcast workstation. AI can analyze, transcribe, suggest cuts, and prepare editable drafts, but cannot publish or export approved masters unattended.

## Known workstation baseline
- Dell Precision 7960 Tower
- Intel Xeon w7-3445, 64 GB RAM
- NVIDIA RTX 2000 Ada Generation (16 GB VRAM)
- 8 TB HDD, Adobe Premiere Pro 26.x, Windows
- Treat hardware as accepted; do not repeatedly audit the user's workstation.
- Internet access is allowed for documentation and installing trusted dependencies. Production media, transcripts, project files, and confidential metadata must remain local.

## System boundaries
1. Adobe Premiere Pro extension: UXP panel for user-initiated commands, status, and review.
2. Local Python orchestrator: job queue, validation, state transitions, traceability.
3. Local AI workers: transcription, scene detection, audio analysis, rough-cut suggestions.
4. Approval service: independent human review with immutable approved-version metadata.
5. Controlled export: release only the exact reviewed and approved artifact.

Do not assume unverified Premiere UXP APIs; validate operations against official Adobe documentation and a compatible installed version. Do not assume a UXP panel can directly spawn Python processes. Prefer a well-defined loopback service and test actual platform restrictions.

## Non-negotiable rules
- Never alter source footage in place; maintain original filenames, checksums, and provenance.
- Do not upload media, transcriptions, scripts, embeddings, project metadata, or confidential prompts to remote AI APIs.
- Bind local APIs to 127.0.0.1 with authentication, narrow CORS policy, and validated requests.
- Never expose the orchestration API to the LAN without a separate security review.
- An AI edit is a proposal requiring explicit human review. Preserve editable sequences and rollback points.
- Approval binds project ID, sequence ID, version, exact path, SHA-256, reviewer, and timestamp. Artifact changes revoke approval.
- No automatic driver, OS, Premiere, or model upgrades. Pin versions and check licenses for models and dependencies.
- Logs must not contain raw confidential transcript or sensitive production media contents.

## Job state machine
QUEUED -> RUNNING -> REVIEW_REQUIRED -> APPROVED -> EXPORTED
RUNNING -> FAILED
QUEUED or RUNNING -> CANCELLED
A changed approved artifact returns to REVIEW_REQUIRED.

## Implementation phases
M0: Repository structure, data contract, threat model, acceptance criteria.
M1: Loopback Python orchestration with deterministic test jobs.
M2: Offline speech-to-text for a non-sensitive sample clip.
M3: Basic UXP panel integration confirmed against Premiere 26.x.
M4: Non-destructive cut suggestions and preview.
M5: Approval workflow with hash binding and audit evidence.
M6: Controlled export with pre-export integrity check.
M7: Security hardening, recovery, and full workflow acceptance tests.

## Suggested development workflow
1. Explicitly distinguish *verified*, *prototype*, *planned*, and *unknown*.
2. Implement one vertical slice at a time, including unit tests and rollback.
3. Generate precise architecture, file tree, interfaces, commands, test cases, and failure handling.
4. Ask human approval before destructive actions or production publishing.
5. Maintain release notes and a reproducible dependency manifest.

## Required response format for future work
- Objective and boundary
- Current phase and implementation status
- Files to add/change, with complete source where requested
- Local setup and safe run instructions
- Verification and acceptance criteria
- Security risks and rollback

See references and templates bundled with this skill.
