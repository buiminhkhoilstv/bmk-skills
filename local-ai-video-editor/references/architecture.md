# Architecture (planned)

```text
Adobe Premiere Pro 26.x
       |
    UXP panel
       |
  HTTP API on 127.0.0.1 (authentication)
       |
  Python orchestrator + job state machine
       |--------------------------|
  local AI workers         approval service
       |                          |
  draft artifacts            approved hashes
       |--------------------------|
             controlled export
```

## Suggested modules
- `app/orchestrator/`: queue, job state, API handlers
- `app/workers/`: offline transcription, audio, scene, rough-cut suggestions
- `app/approval/`: reviewer identity, approval records, SHA-256 verification
- `app/common/`: schemas, error handling, path safety
- `premiere-uxp/`: UI and Premiere integration only where official API supports it
- `config/`, `tests/`, `docs/`, `models/`
- `data/source/`, `data/work/`, `data/cache/`, `data/ai-results/`, `data/exports/`, `data/approvals/`, `data/logs/`

Keep source footage read-only and retain provenance. Fast SSD storage for active cache is recommended where available, but is not a blocker to beginning development. The 8 TB HDD can store bulk media/archive.
