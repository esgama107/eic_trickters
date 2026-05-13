# CV / Resume / Cover Letter Prompt Kit

**An AI-powered system for capturing professional experiences once and tailoring resumes, cover letters, and CVs for any job — without starting from scratch each time.**

> **Core insight:** Experiences are stable; framing changes per audience. Capture once, tailor many.

Built for **early-in-career (EIC) professionals**, mentors, and anyone revisiting their career narrative. The system replaces the painful cycle of rewriting documents from memory with a structured process: capture your experiences in a rich, portable format, then let AI translate and present them for each opportunity.

---

### How to use a prompt from this kit

1. Click the prompt link to open the file
2. Find the text inside the gray code block (it starts with `You are a...`)
3. Copy all of that text (use the copy button in the corner of the code block, or select all and copy)
4. Open your chat AI (ChatGPT, GitHub Copilot, Claude, or similar)
5. Paste the text into the chat and press Enter
6. The AI will guide you from there

> **Terminology:** A *prompt* is the text you copy and paste into a chat AI.
> The *prompt kit* is this collection of prompts, guides, and reference materials.
> Your *Experience Profile* is the YAML file that stores all your professional experiences.

---

## Getting Started

### 🎓 For Users (EIC Professionals)

| Step | What to do | File |
|------|-----------|------|
| **1. Capture your experiences** | Paste the prompt into any chat AI and complete the 8-phase interview (~45-60 min) | [experience-capture.md](prompts/experience-capture.md) |
| **1b. Already have a resume?** | Upload your resume and convert it to a YAML profile (~5-30 min depending on mode) | [experience-from-resume.md](prompts/experience-from-resume.md) |
| **2. Save your profile** | Save the YAML output as `my-experience-profile.yaml` — this is your portable career record | [experience-profile-template.yaml](schema/experience-profile-template.yaml) |
| **3. Find a job → generate resume** | Upload your YAML + the job description + the resume prompt | [resume-builder.md](prompts/resume-builder.md) |
| **3b. Evaluate an existing resume** | Upload your resume + job description to get an ATS readiness score and actionable fixes | [resume-builder.md](prompts/resume-builder.md) |
| **4. Research the company → generate cover letter** | Upload your YAML + job description + company info + the cover letter prompt | [cover-letter-builder.md](prompts/cover-letter-builder.md) |
| **5. Get feedback → revise** | Share the output with a mentor, then use the feedback prompt to apply revisions | [feedback-revision.md](prompts/feedback-revision.md) |
| **6. New experience → update profile** | Add new jobs, projects, or skills without re-doing the full interview (~5-10 min) | [experience-update.md](prompts/experience-update.md) |

> **Tip:** Set up [chat memory](guides/memory-integration.md) so the AI remembers your profile across sessions.

---

### 🧑‍🏫 For Mentors

**Start here:** Read the [Session Workflow Guide](guides/session-workflow.md) — it maps the prompt kit to a **3-session mentorship model** (~60 min each):

| Session | Goal | Output |
|---------|------|--------|
| **1. Capture & Explore** | Build a complete experience profile | Completed `experience-profile.yaml` |
| **2. Resume & Target** | Generate a tailored resume for a real job | Resume v1 |
| **3. Cover Letter & Iterate** | Generate a cover letter + plan for iteration | Cover letter v1 + revision plan |

**What mentors should know:**

- **The system captures, AI formats — mentors coach on framing.** Your job is to help the mentee *articulate* their experiences, not to worry about document formatting.
- **Push for specifics.** "I helped with the project" → "I designed the survey instrument used to collect data from 150 participants." The richer the capture, the better the output.
- **The feedback-revision prompt closes the loop.** After reviewing a resume or cover letter, the mentee feeds your feedback back into the system — no manual reformatting needed.
- **Optional deep-dive:** Read [How Translation Works](guides/how-translation-works.md) to understand the 3-layer model (experience inventory → translation layer → presentation output).

---

<details>
<summary><strong>How It Works — Architecture Diagram</strong></summary>

```
                                                  ┌─────────────────────┐
                                                  │  Reference Materials│
                                                  │  ─────────────────  │
                                                  │  · Translation Guide│
                                                  │  · Action Verbs     │
                                                  │  · ATS Keywords     │
                                                  │  · STAR Examples    │
                                                  └──────────┬──────────┘
                                                             │
                                                             │ (feeds into builders)
                                                             │
                     ┌─────────────────┐                     │
                     │  Experience     │                     │
                     │  Capture        │                     │
                     │  (8-phase       │                     │
                     │   interview)    │                     │
                     └────────┬────────┘                     │
                              │                              │
                              ▼                              │
                     ┌─────────────────┐                     │
                     │  Experience     │                     │
                     │  Profile        │◄── Experience       │
                     │  (YAML)         │    Update           │
                     │                 │    (add new         │
                     │  source of      │     experiences)    │
                     │  truth          │                     │
                     └───┬────┬────┬───┘                     │
                         │    │    │                          │
              ┌──────────┘    │    └──────────┐               │
              │               │               │               │
              ▼               ▼               ▼               │
     ┌────────────┐  ┌────────────┐  ┌────────────┐          │
     │  Resume    │  │  Cover     │  │  Future:   │          │
     │  Builder   │◄─┤  Letter    │◄─┤  CV, etc.  │◄─────────┘
     │            │  │  Builder   │  │            │
     │  + JD      │  │  + JD      │  │            │
     └──────┬─────┘  │  + Company │  └────────────┘
            │        └──────┬─────┘
            │               │
            ▼               ▼
     ┌────────────────────────────┐
     │  Feedback & Revision      │
     │  (mentor feedback prompt  │
     │   loops back to profile)  │
     └────────────────────────────┘
```

**The YAML never changes for a specific job.** One file feeds dozens of different resumes and cover letters — what changes is which parts get selected and how they get phrased.

</details>

---

## Directory Map

```
cv_resume_cover/
├── README.md                    ← You are here
├── proposal.md                  ← Original idea and multi-perspective analysis
├── TODO.md                      ← Backlog from baseline testing
│
├── prompts/                          ── The core prompt kit ──
│   ├── experience-capture.md    ← 8-phase interview (start here)
│   ├── experience-from-resume.md← Convert existing resume → YAML profile
│   ├── experience-update.md     ← Add new experiences (5-10 min)
│   ├── resume-builder.md        ← ATS-optimized resume from profile + JD
│   │                               (also evaluates existing resumes)
│   ├── cover-letter-builder.md  ← Narrative cover letter from profile + JD + company
│   └── feedback-revision.md     ← Apply mentor feedback, loop back to profile
│
├── schema/                           ── The portable file format ──
│   ├── experience-profile-template.yaml  ← YAML template for your profile
│   └── README.md                ← Schema documentation and field reference
│
├── reference/                        ── Supporting materials (used by prompts) ──
│   ├── translation-guide.md     ← Academic → industry language mapping
│   ├── action-verbs/            ← Field-specific verb lists (3 files)
│   ├── ats-keywords/            ← ATS keyword glossaries (4 files)
│   ├── star-examples/           ← STAR/CAR bullet examples (4 files)
│   └── job-descriptions/        ← Sample JDs for practice (1 file)
│
├── guides/                           ── How-tos and deep dives ──
│   ├── memory-integration.md    ← Chat memory setup (Copilot/Claude/ChatGPT)
│   ├── session-workflow.md      ← 3-session mentorship model + checklists
│   └── how-translation-works.md ← Under-the-hood explainer (optional reading)
│
├── testing/                          ── Quality assurance ──
│   └── personas.md              ← 10 test personas across 7 archetypes
│
└── *.pdf                        ← GMI mentorship session guides (source material)
```

---

## Design Principles

| Principle | What it means |
|-----------|--------------|
| **Chat-first** | Works in any chat AI interface — Copilot, Claude, ChatGPT. No special tools needed. |
| **Capture once, tailor many** | The YAML profile is the single source of truth. One file, many documents. |
| **EIC-friendly** | Warm tone, hand-holding, confidence nudges. Designed for people who undervalue their experiences. |
| **Field-agnostic** | Tested across 7 archetypes and 10 majors — from mechanical engineering to philosophy to nursing. |
| **AI does the formatting** | Humans capture experiences and make framing decisions. AI handles translation, structure, and ATS (Applicant Tracking Systems — software that filters resumes) optimization. |

---

## For Contributors & Testers

Want to improve or test the system? Here's how.

### Run tests

Use the 10 personas in [`testing/personas.md`](testing/personas.md). Each persona is designed to stress-test a specific weakness — career pivots, clinical hours capture, portfolio-first fields, humanities reframing, etc.

**Basic test flow:**
1. Pick a persona → run the Experience Capture prompt with their background
2. Run the Resume Builder with their target job
3. Evaluate the output against their `tests` field

### Evaluate results

Score outputs on four dimensions:

| Dimension | What to look for |
|-----------|-----------------|
| **Capture completeness** | Did the interview extract all relevant experiences, skills, and outcomes? |
| **Resume quality** | ATS keyword match, bullet impact, section ordering, tailoring to the JD |
| **Prompt inclusivity** | Does the prompt handle non-traditional backgrounds without bias or dismissal? |
| **Career translation** | Are academic/non-industry experiences reframed into professional language? |

**Current baseline:** overall avg 3.85/5.00 (worst 3.25, best 4.75) — from the initial 10-persona test. Resume avg 4.16/5.00, cover letter avg 4.90/5.00 after improvements.

### Add a new persona

Follow the format in [`testing/personas.md`](testing/personas.md):
- Define background, experiences, skills, target job, and friction points
- Tag the archetype (STEM Quant, Humanities, Creative, etc.)
- Include a `tests` field with specific things to check in the output

### Propose changes

1. Create a branch
2. Implement your change
3. Test with at least 3 personas (pick ones relevant to your change)
4. Show before/after scores
5. Open a PR with the results

### Where help is needed

See [`TODO.md`](TODO.md) for the full backlog. High-priority items include:
- Adding a licensure section to the schema (nursing, teaching, EMT)
- Expanding the translation guide for under-covered fields (biology, design, education)
- Improving career-pivot keyword matching
- Adding clinical/supervised hours capture

---

*Part of the [GMI Mentorships](../README.md) project.*
