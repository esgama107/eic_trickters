# GMI Mentorships

A collection of ideas and tools born from mentorship sessions, designed to help **early-in-career (EIC)** professionals — and anyone revisiting their career narrative — build stronger professional documents.

## Current Projects

### 📄 CV / Resume / Cover Letter System (`cv_resume_cover/`)

**Core idea:** Capture professional experiences *once* in rich detail, then derive resumes, CVs, cover letters, and other documents by changing *focus* — not relying on memory.

This decouples **memory from presentation**, reducing cognitive load and preventing information loss across document iterations.

#### Quick Start

1. **Capture your experiences** — paste the [Experience Capture prompt](cv_resume_cover/prompts/experience-capture.md) into your preferred chat assistant and go through the interview
2. **Save your profile** — the assistant produces a YAML file; save it as `my-experience-profile.yaml`
3. **Generate a resume** — upload your YAML + a job description + the [Resume Builder prompt](cv_resume_cover/prompts/resume-builder.md)
4. **Set up memory** — follow the [Memory Integration Guide](cv_resume_cover/guides/memory-integration.md) for a smoother experience across sessions

#### Structure

```
cv_resume_cover/
  proposal.md                              # Original proposal & analysis
  prompts/
    experience-capture.md                  # Interview-style experience capture prompt
    resume-builder.md                      # ATS-optimized resume generation prompt
  schema/
    README.md                              # Schema documentation
    experience-profile-template.yaml       # Portable experience file template
  guides/
    memory-integration.md                  # Chat memory setup across platforms
```

See [`cv_resume_cover/proposal.md`](cv_resume_cover/proposal.md) for the full proposal and multi-perspective analysis.

## Design Principles

- **Chat-first interaction** — designed to work through conversational AI interfaces (Copilot, Claude, ChatGPT) using memories and structured prompts
- **EIC-friendly, expert-compatible** — approachable for early-career users, valuable for experienced professionals too
- **Capture once, tailor many** — experiences are stable; framing changes per audience and purpose
- **Iterate without losing** — every version builds on a canonical source, nothing gets forgotten
- **Portable by default** — YAML file travels across platforms; no vendor lock-in

## Status

🚧 MVP — experience capture and resume generation prompt kits are ready for use. Cover letters, academic CVs, and experienced-user flows are planned for future iterations.

---

*This README will evolve as the project grows.*
