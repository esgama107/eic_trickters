# Experience Profile — Portable Format

This YAML template is the **canonical source of truth** for a person's professional experiences.
It is designed to be:

- **Human-readable** — easy to review and edit in any text editor
- **Portable** — can be uploaded to any chat interface (Copilot, Claude, ChatGPT) as context
- **Structured** — parseable by AI assistants to generate tailored resumes, CVs, and letters
- **Append-friendly** — new experiences are added; nothing is deleted

## How to use

1. Run the [Experience Capture prompt](../prompts/experience-capture.md) in your preferred chat interface
2. The assistant will walk you through an interview and produce a filled YAML file
3. Save the file locally (e.g., `my-experience-profile.yaml`)
4. When generating a resume, upload this file as context along with the [Resume Builder prompt](../prompts/resume-builder.md)

## Schema overview

```
profile:
  name, contact, summary

experiences[]:
  title, organization, type, dates
  context       — what the role/project was about
  actions[]     — what you did (verb-first)
  skills[]      — tools, technologies, competencies used
  outcomes[]    — results, impact, evidence
  learnings[]   — what you grew from
  keywords[]    — ATS-relevant terms

education[]:
  degree, institution, dates, highlights

skills_inventory:
  technical[], interpersonal[], languages[]

interests[]     — optional, for cultural fit signals
```

See [`experience-profile-template.yaml`](experience-profile-template.yaml) for the full template with guidance comments.
