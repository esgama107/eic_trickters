# Experience Profile — Portable Format

This YAML template is the **central source of truth** for a person's professional experiences.
It is designed to be:

- **Human-readable** — easy to review and edit in any text editor
- **Portable** — can be uploaded to any chat interface (Copilot, Claude, ChatGPT) as context
- **Structured** — readable by AI assistants to generate tailored resumes, CVs, and letters
- **Append-friendly** — designed so you can keep adding new experiences without changing what's already there

## How to use

1. Run the [Experience Capture prompt](../prompts/experience-capture.md) in your preferred chat interface
2. The assistant will walk you through an interview and produce a filled YAML file
3. Save the file locally (e.g., `my-experience-profile.yaml`)
4. When generating a resume, upload this file as context along with the [Resume Builder prompt](../prompts/resume-builder.md)

## Schema overview

```
profile:
  name, contact, summary, work_authorization
  career_narrative:
    interests, target_industries[], values[]
    short_term_goal, long_term_goal

experiences[]:
  title, organization, type, scope, dates
  context       — what the role/project was about
  team_context  — size, role_in_team (solo, led, collaborated, supported)
  actions[]     — what you did (verb-first)
  skills[]      — tools, methods, skills, and approaches used
  outcomes[]    — results: quantitative, qualitative, or artifacts
  learnings[]   — what you grew from
  challenges[]  — obstacles faced (fuels cover letter narratives)
  keywords[]    — ATS-relevant terms (AI-populated)
  supervised_hours — total, type, supervisor_title (clinical/practicum)
  populations_served — who you served or worked with
  client        — for freelance or consulting work

education[]:
  degree, institution, dates, highlights

skills_inventory:
  technical[]   — supports optional proficiency levels (basic → expert)
  interpersonal[], languages[]

publications[]:   — papers, articles, blog posts
portfolio_pieces[] — things you built or created
awards[]          — honors, competitions, recognition
interests[]       — optional, for cultural fit signals
certifications[]  — courses, credentials
licensure[]       — legally required licenses (nursing, teaching, etc.)
```

**Experience types:** work, internship, project, volunteering, freelance, research, teaching, fieldwork, thesis, practicum, competition, editorial, exhibition

**Date format:** Mon YYYY (e.g., Jan 2024, Present)

See [`experience-profile-template.yaml`](experience-profile-template.yaml) for the full template with guidance comments.
