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
4. **Generate a cover letter** — upload your YAML + job description + company info + the [Cover Letter Builder prompt](cv_resume_cover/prompts/cover-letter-builder.md)
5. **Update your profile** — use the [Experience Update prompt](cv_resume_cover/prompts/experience-update.md) to add new experiences without re-interviewing
6. **Set up memory** — follow the [Memory Integration Guide](cv_resume_cover/guides/memory-integration.md) for a smoother experience across sessions
7. **Run a mentorship session** — follow the [Session Workflow Guide](cv_resume_cover/guides/session-workflow.md) for a structured 3-session model

#### Structure

```
cv_resume_cover/
  proposal.md                              # Original proposal & analysis
  TODO.md                                  # Backlog from baseline testing
  prompts/
    experience-capture.md                  # Interview-style experience capture (8 phases)
    experience-update.md                   # Lightweight profile update prompt
    resume-builder.md                      # ATS-optimized resume generation
    cover-letter-builder.md                # Narrative cover letter generation
  schema/
    README.md                              # Schema documentation
    experience-profile-template.yaml       # Portable experience file template
  reference/
    translation-guide.md                   # Academic → industry language mapping
    action-verbs/                          # Field-specific action verb lists
    ats-keywords/                          # ATS keyword glossaries by sector
    star-examples/                         # STAR/CAR bullet examples
    job-descriptions/                      # Sample JDs for practice
  guides/
    memory-integration.md                  # Chat memory setup across platforms
    session-workflow.md                    # 3-session mentorship facilitation guide
  testing/
    personas.md                            # 10 test personas (7 archetypes)
```

See [`cv_resume_cover/proposal.md`](cv_resume_cover/proposal.md) for the full proposal and multi-perspective analysis.

## Design Principles

- **Chat-first interaction** — designed to work through conversational AI interfaces (Copilot, Claude, ChatGPT) using memories and structured prompts
- **EIC-friendly, expert-compatible** — approachable for early-career users, valuable for experienced professionals too
- **Capture once, tailor many** — experiences are stable; framing changes per audience and purpose
- **Iterate without losing** — every version builds on a canonical source, nothing gets forgotten
- **Portable by default** — YAML file travels across platforms; no vendor lock-in

## Status

✅ **v1.0** — Full application package pipeline is operational:
- Experience capture (8-phase interview, 10+ experience types, field-aware coaching)
- Resume generation (ATS-optimized, keyword translation, career pivot support)
- Cover letter generation (narrative structure, tone switching, company-specific)
- Profile maintenance (lightweight update prompt)
- Tested across 10 personas, 7 archetypes — avg score 4.16/5.00 (resume), 4.90/5.00 (cover letter)

🔮 **Next:** Feedback loops, CV generation.

---

*This README will evolve as the project grows.*
