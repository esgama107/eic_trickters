# How the Prompt Kit Translation System Works

> **Reading level:** Optional — for mentors and power users who want to understand the mechanics.
>
> **What this covers:** How raw experiences in a YAML profile become tailored resumes and cover letters. The decision logic, the failure modes, and what to watch for.
>
> **You don't need this to use the tools.** The prompts work without understanding the internals. But if you're coaching someone through the process, or debugging why an output doesn't feel right, this is the guide that explains what's happening under the hood.

---

## 1. The Three-Layer Model

The prompt kit system works in three layers. Each layer has a specific job, adds something, and filters something out.

```
┌─────────────────────────────────────────────────────────┐
│  LAYER 1: Experience Inventory                          │
│  (experience-profile.yaml)                              │
│                                                         │
│  Everything the user has done. Unfiltered, unranked.    │
│  One file that grows over time.                         │
│                                                         │
│  Contains: actions, skills, outcomes, learnings,        │
│            context, career_narrative, keywords           │
└──────────────────────────┬──────────────────────────────┘
                           │
                   Selection + Reframing
                   (What matters for THIS job?
                    How should it be phrased?)
                           │
                           ▼
┌─────────────────────────────────────────────────────────┐
│  LAYER 2: Translation Layer                             │
│  (prompts + translation guide)                          │
│                                                         │
│  The intelligence. Analyzes the job description,        │
│  maps requirements to experiences, translates           │
│  academic language into industry terms.                 │
│                                                         │
│  Adds: relevance ranking, keyword mapping,              │
│        professional reframing, gap identification        │
│  Filters: irrelevant experiences, academic jargon,      │
│           low-impact details                             │
└──────────────────────────┬──────────────────────────────┘
                           │
                   Formatting + Optimization
                   (What format? What tone?
                    What structure?)
                           │
                           ▼
┌─────────────────────────────────────────────────────────┐
│  LAYER 3: Presentation Output                           │
│  (resume, cover letter, CV)                             │
│                                                         │
│  The final document. Tailored to one specific role      │
│  at one specific company.                               │
│                                                         │
│  Adds: formatting, narrative structure, ATS (Applicant Tracking Systems)  │
│        keywords, tone, document-specific conventions               │
│  Filters: redundancy, anything that doesn't earn its    │
│           space on the page                              │
└─────────────────────────────────────────────────────────┘
```

### What each layer owns

| Layer | Owns | Doesn't Own |
|---|---|---|
| **Experience Inventory** | The truth — what actually happened, complete and unedited | Relevance, phrasing, formatting |
| **Translation Layer** | Relevance decisions, language mapping, gap analysis | The raw facts, the final format |
| **Presentation Output** | Format, tone, structure, ATS compliance | What experiences exist, what's true |

### The key design principle

**The YAML never changes for a specific job.** It's the single source of truth. What changes is which parts get selected and how they get phrased. One YAML file feeds dozens of different resumes and cover letters — each tailored to a different role.

---

## 2. How the Resume Builder Decides

The resume builder prompt runs through a structured decision process before writing a single bullet point. Here's how it works, step by step.

### a. Matching: Job Requirements → Experiences

The builder starts with the job description and works backward:

```
Job Description                    Experience Profile
─────────────                      ──────────────────
"3+ years data analysis"    ──→    Research Assistant (2 years, used SPSS)
                                   Thesis (1 year, statistical modeling)
                                   ∴ Combined: ~3 years of data work

"Strong communication"      ──→    Teaching Assistant (led tutorials)
                                   Conference Presentation
                                   ∴ Multiple matches — pick strongest

"Experience with SQL"        ──→    No direct match
                                   ∴ GAP — check for transferable skills
```

It identifies the **top 5 requirements** from the job posting and maps each one to the best-matching experience. This is not just keyword matching — it looks at the `actions`, `skills`, `outcomes`, and `keywords` fields for each experience.

### b. Selection: Not Everything Makes the Cut

The resume is one page. The YAML might have 10+ experiences. The builder's selection logic works like this:

```
All Experiences in YAML
        │
        ▼
   ┌─────────┐
   │ Relevant │──→ Does this experience connect to ANY job requirement?
   │  Filter  │    No → Leave it out
   └────┬────┘
        │
        ▼
   ┌─────────┐
   │  Rank    │──→ Which matches are STRONGEST?
   │  Filter  │    Consider: recency, depth, outcomes, skill overlap
   └────┬────┘
        │
        ▼
   ┌─────────┐
   │  Space   │──→ Does it fit on one page?
   │  Filter  │    Cut weakest remaining entries
   └────┬────┘
        │
        ▼
   3-5 experiences on the final resume
```

**What doesn't get selected isn't lost.** It stays in the YAML for a different job application where it might be the strongest match.

### c. Bullet Formula Choice

The builder picks from three formulas depending on the type of experience and what data is available:

| Formula | Best For | Structure | Example |
|---|---|---|---|
| **XYZ** | Quantitative results | Accomplished [X] by doing [Y], resulting in [Z] | "Reduced data processing time by 40% by automating weekly reports using Python scripts, saving the team 8 hours per week" |
| **CAR** | Complex or qualitative work | Faced [Challenge], took [Action], achieved [Result] | "Faced inconsistent participant recruitment across three study sites; redesigned screening protocol, increasing enrollment by 25%" |
| **Narrative** | Research, writing, teaching | [Action verb] [what you did], [artifact or outcome] | "Designed and delivered weekly tutoring sessions for 15 undergraduate students, contributing to a 20% improvement in course pass rates" |

**How it chooses:**
- Does the `outcomes` field have numbers? → XYZ
- Does the `context` field describe a problem or challenge? → CAR
- Is the experience type `research`, `teaching`, `thesis`, or `editorial`? → Narrative
- No clear winner? → Defaults to Narrative with qualitative outcomes

### d. Keyword Translation

This is step 1g in the resume builder — one of the most important operations.

The builder compares the user's YAML language against the job description's language and looks for **same concept, different words**:

```
User's YAML Says             Job Description Says         Action
─────────────────            ────────────────────         ──────
"statistical modeling"   →   "predictive analytics"    →  SUBSTITUTE
"thesis research"        →   "independent research"    →  SUBSTITUTE
"peer tutoring"          →   "individual instruction"  →  SUBSTITUTE
"SPSS"                   →   "SPSS"                    →  KEEP (already matches)
"literature review"      →   "market research"         →  TRANSLATE with bridge phrase
```

The [Translation Guide](../reference/translation-guide.md) provides a lookup table for common academic-to-industry mappings. When it's uploaded alongside the YAML, the builder uses it to bridge gaps between how the user describes their work and how the employer describes the same skills.

**The keyword match threshold:** If fewer than 6 out of 10 top keywords match after translation, the builder raises a warning — the profile may not be a strong fit for the role.

### e. Gap Handling

When a job requirement has no match in the YAML, the builder has three strategies:

1. **Transferable skills** — Find an adjacent experience that demonstrates the underlying capability. "No SQL experience, but used SPSS for database queries — similar analytical thinking."

2. **Reframing** — Use the career pivot check (step 1f) to build a bridge narrative. "Philosophy thesis → analytical writing and stakeholder communication."

3. **Honest omission** — If there's no reasonable connection, the builder says so and doesn't fabricate one. It may suggest the user is underqualified and recommend a better-fitting role.

```
Gap Detected: "3+ years project management experience"
     │
     ├─→ Can a transferable skill bridge it?
     │       Yes → Reframe student org leadership as project management
     │       No  ↓
     │
     ├─→ Can the translation guide help?
     │       Yes → "Student organization leadership" → "Cross-functional
     │              team leadership; project management"
     │       No  ↓
     │
     └─→ Flag honestly: "This requirement is not met.
          Consider whether a coordinator role (rather than
          manager) might be a better current fit."
```

---

## 3. How the Cover Letter Builder Differs

The resume and cover letter pull from the **same YAML** but use different fields, apply different logic, and produce fundamentally different documents.

### Side-by-Side Comparison

```
                    RESUME                          COVER LETTER
                    ──────                          ────────────

Purpose:           Prove qualifications             Tell a story

Structure:         Bullet points, sections           Paragraphs, narrative

Primary fields     actions                          context
from YAML:         skills                           learnings
                   outcomes                         career_narrative
                   keywords                         values

Selection logic:   Pick BEST experiences             Pick MOST COMPELLING
                   for keyword match                 experiences for narrative arc

What it filters:   Context, learnings,              Keyword lists, full action
                   career motivation                 inventories, ATS formatting

Tone driver:       Job description language          Company culture + chosen
                                                     tone (professional,
                                                     conversational, academic,
                                                     mission-driven)

ATS matters?       Critical — keywords,              No — read by humans,
                   formatting, standard              not machines
                   headings

Repetition rule:   Can overlap with cover            Must ADD NEW INFORMATION
                   letter content                    not on the resume
```

### Why Different YAML Fields?

The YAML was designed with this split in mind:

- **`actions`** and **`outcomes`** are resume fuel — they answer "what did you do and what happened?"
- **`context`** and **`learnings`** are cover letter fuel — they answer "why did it matter and how did you grow?"
- **`career_narrative`** and **`values`** drive cover letter alignment — they answer "why this company, why this work?"
- **`keywords`** exist purely for ATS — the cover letter doesn't need them

### How the Same Experience Appears Differently

Take a single YAML entry and watch it transform:

**Raw YAML entry:**
```yaml
- title: "Research Assistant"
  organization: "University Behavioral Health Lab"
  type: research
  context: "Worked in a lab studying anxiety interventions for
            underserved adolescent populations. The lab was
            chronically understaffed, so I took on responsibilities
            beyond my role."
  actions:
    - "Recruited and screened 40+ study participants"
    - "Administered standardized anxiety assessments (GAD-7, PHQ-9)"
    - "Coded qualitative interview data using NVivo"
    - "Maintained IRB compliance documentation"
  skills:
    - "NVivo"
    - "SPSS"
    - "IRB protocols"
    - "qualitative coding"
    - "participant recruitment"
  outcomes:
    - "Contributed to dataset used in published paper"
    - "Improved screening efficiency by standardizing intake process"
  learnings:
    - "Learned to work independently when supervision was limited"
    - "Developed deep empathy for participants navigating the
       mental health system"
  keywords:
    - "behavioral research"
    - "data collection"
    - "qualitative analysis"
```

**In the resume** (selection-based — pick strongest actions + outcomes + keywords):
```
Research Assistant — University Behavioral Health Lab | Jan 2023 - Dec 2023
- Recruited and screened 40+ study participants for anxiety intervention
  research, ensuring IRB compliance throughout the enrollment process
- Conducted qualitative data analysis using NVivo, coding interview
  transcripts that contributed to a peer-reviewed publication
- Standardized the participant intake process, improving screening
  efficiency and reducing onboarding time for new research staff
```

**In the cover letter** (narrative-based — context + learnings + story):
```
My time in the University Behavioral Health Lab taught me what it means
to do research that matters. Working with adolescents navigating anxiety
in communities with limited mental health resources, I saw firsthand how
careful, participant-centered research can shape better interventions.
When staffing constraints required me to take on responsibilities beyond
my role — from recruitment to qualitative coding — I discovered that I
thrive in environments where initiative is valued and the work has
real-world stakes.
```

**Notice:**
- The resume uses `actions`, `outcomes`, and `keywords` → bullet points with metrics
- The cover letter uses `context` and `learnings` → a narrative paragraph with personal growth
- The resume says "what I did"; the cover letter says "why it mattered to me"
- Neither document lies — they just illuminate different facets of the same experience

---

## 4. Worked Example

Let's trace a complete example from YAML to final output for both documents.

### The persona

**Maya Torres** — Psychology graduate applying for a **Research Coordinator** position at a health tech company. The job description asks for: participant recruitment, data management, IRB compliance, team coordination, and familiarity with research databases.

### a. The Raw YAML Entry

```yaml
- title: "Research Assistant"
  organization: "University Behavioral Health Lab"
  type: research
  scope: multi_year
  start_date: "Aug 2022"
  end_date: "May 2024"
  location: "Austin, TX"
  context: "Supported a PI-led study examining the efficacy of a
            group-based CBT intervention for anxiety in adolescents
            from Title I school districts. The lab had 2 faculty
            and 4 student assistants."
  actions:
    - "Recruited and pre-screened 60+ study participants from 3 school sites"
    - "Administered standardized assessments (GAD-7, PHQ-9, SCARED)"
    - "Managed participant database in REDCap, ensuring data integrity"
    - "Coded qualitative interview transcripts using NVivo (200+ pages)"
    - "Coordinated scheduling across 3 school sites and 12 facilitators"
    - "Maintained IRB documentation and amendment submissions"
  skills:
    - "REDCap"
    - "NVivo"
    - "SPSS"
    - "IRB protocols"
    - "GAD-7 / PHQ-9 / SCARED administration"
    - "qualitative coding"
    - "participant recruitment"
    - "multi-site coordination"
  outcomes:
    - "Contributed to dataset supporting a paper published in
       Journal of Adolescent Health"
    - "Reduced participant no-show rate by 15% through systematic
       reminder protocol"
    - "Trained 2 incoming research assistants on REDCap and
       assessment procedures"
  learnings:
    - "Learned to manage competing priorities across multiple
       sites without direct authority"
    - "Developed a deep appreciation for participant-centered
       research practices"
    - "Discovered that I enjoy the operational side of research
       as much as the analytical side"
  keywords:
    - "clinical research"
    - "participant recruitment"
    - "data management"
    - "REDCap"
    - "IRB compliance"
    - "multi-site coordination"
    - "qualitative research"
```

### b. Resume Builder Transformation

**Step 1 — Analysis:**

```
Top 5 Job Requirements         Best Match from YAML           Keyword Status
─────────────────────          ────────────────────           ──────────────
Participant recruitment     →  "Recruited 60+ participants"   ✅ Direct match
Data management             →  "Managed database in REDCap"   ✅ Direct match
IRB compliance              →  "Maintained IRB documentation"  ✅ Direct match
Team coordination           →  "Coordinated 3 sites,          ✅ Reframe as
                                12 facilitators"                  "team coordination"
Research database famil.    →  "REDCap"                        ✅ Direct match
```

**Step 2 — Bullet formula decisions:**

| Action | Best Formula | Why |
|---|---|---|
| Recruited 60+ participants | XYZ | Has a number (60+) and a clear method |
| Managed REDCap database | Narrative | Process-oriented, no dramatic metric |
| Reduced no-show rate by 15% | XYZ | Clear quantitative outcome |
| Coordinated 3 sites | CAR | Implicit challenge (multiple sites, no authority) |

**Step 3 — Final resume bullets:**

```
Research Assistant — University Behavioral Health Lab | Aug 2022 - May 2024
- Recruited and pre-screened 60+ study participants across 3 school sites,
  maintaining IRB compliance throughout the multi-site enrollment process
- Managed participant database in REDCap, ensuring data integrity for a
  dataset that supported a peer-reviewed publication in the Journal of
  Adolescent Health
- Reduced participant no-show rate by 15% by designing and implementing
  a systematic reminder protocol across all study sites
- Coordinated scheduling and logistics for 12 facilitators across 3
  school sites, training 2 incoming research assistants on study procedures
```

### c. Cover Letter Builder Transformation

**Step 1 — Analysis:**

```
Story angle: "A researcher who discovered she loves the operational
              engine behind impactful research"

Company alignment: Health tech company values "participant-centered
                   design" and "scalable research operations" — Maya's
                   multi-site coordination and participant focus map
                   directly to these values.

Best narrative fields:
  context  → Sets the scene (understaffed lab, vulnerable population)
  learnings → "Enjoys operational side" = perfect for coordinator role
  values   → Participant-centered research aligns with company mission
```

**Step 2 — Final cover letter paragraph (body paragraph 1):**

```
As a research assistant in the University Behavioral Health Lab, I
supported a study examining group-based CBT interventions for
adolescents in Title I school districts — work that reinforced my
belief that rigorous research and genuine care for participants are
not at odds. Coordinating recruitment across three school sites and
managing logistics for twelve facilitators, I learned to navigate
complexity without direct authority, a skill I relied on daily. When
I designed a reminder protocol that reduced our no-show rate by 15%,
I realized that the operational side of research — the systems that
make studies actually run — is where I do my best work. It is this
same operational rigor that I would bring to the Research Coordinator
role at [Company Name].
```

### d. Side-by-Side: Same Experience, Two Documents

```
┌─────────────────────────────────┬──────────────────────────────────┐
│          RESUME                 │        COVER LETTER              │
├─────────────────────────────────┼──────────────────────────────────┤
│                                 │                                  │
│ Leads with: actions + outcomes  │ Leads with: context + learnings  │
│                                 │                                  │
│ "Recruited 60+ participants     │ "I supported a study examining   │
│  across 3 school sites"         │  CBT interventions for           │
│                                 │  adolescents in Title I          │
│                                 │  school districts"               │
│                                 │                                  │
│ Metric-forward:                 │ Reflection-forward:              │
│ "Reduced no-show rate by 15%"   │ "I realized the operational      │
│                                 │  side of research is where I     │
│                                 │  do my best work"                │
│                                 │                                  │
│ Format: bullet points           │ Format: narrative paragraph      │
│ Tone: professional, concise     │ Tone: personal, story-driven     │
│ Keywords: embedded naturally    │ Keywords: secondary concern      │
│                                 │                                  │
│ Goal: prove you can do the job  │ Goal: show why you want the job  │
│                                 │  and who you are                 │
└─────────────────────────────────┴──────────────────────────────────┘
```

---

## 5. When Translation Goes Wrong

These are the failure modes mentors should watch for. Each one is common, each one is fixable.

### Over-Translation

**What it looks like:** Making modest experiences sound like executive leadership.

```
❌  "Managed international logistics operations" (was a campus tour guide
     who sometimes hosted visiting international students)

❌  "Led cross-functional stakeholder engagement initiatives" (organized
     a bake sale for a student club)
```

**Why it happens:** The translation guide maps "student org leadership" to "cross-functional team leadership" — but the builder should scale the language to match the scope. A bake sale is not stakeholder engagement.

**How to catch it:** Read the bullet out loud. If you'd be embarrassed explaining it in an interview, it's over-translated. The test: "Could the user defend this phrasing in a 30-second follow-up question?"

### Under-Translation

**What it looks like:** Leaving academic jargon that recruiters outside academia won't understand.

```
❌  "Conducted IRB protocol amendments for a longitudinal CBT efficacy
     study using a quasi-experimental pre-post design"

✅  "Updated research compliance documentation for a multi-year study
     on anxiety interventions, ensuring adherence to federal research
     standards"
```

**Why it happens:** The user described their work in expert terms (because they ARE the expert), and the builder didn't translate enough for a non-academic audience.

**How to catch it:** Show the bullet to someone outside the field. If they can't understand what the person did, it's under-translated. Exception: if the job posting uses the same technical language, keep it.

### Keyword Stuffing

**What it looks like:** Forcing keywords into sentences where they don't naturally fit.

```
❌  "Utilized project management, data analysis, and cross-functional
     collaboration to deliver stakeholder-facing data-driven insights
     through strategic communication channels"

✅  "Coordinated data collection across three research sites, presenting
     weekly progress reports to the faculty team"
```

**Why it happens:** The builder's keyword match scoring (step 6b) incentivizes hitting 7+/10 keywords. If the profile is a weak match, the builder might force keywords in to improve the score.

**How to catch it:** Read the sentence out loud. If it sounds like a job posting instead of a description of what someone did, there are too many keywords. Every keyword should describe something the user actually did.

### Losing the Human Voice

**What it looks like:** Output that reads like it was generated by AI — generic, polished, and devoid of personality.

```
❌  "I am passionate about leveraging data-driven insights to drive
     meaningful impact in the healthcare space. My diverse experience
     has equipped me with a unique skill set that positions me to
     make immediate contributions to your dynamic team."

✅  "Working with anxious adolescents in under-resourced schools
     convinced me that good research needs good systems behind it.
     That's the work I want to do — and it's exactly what your
     Research Coordinator role asks for."
```

**Why it happens:** The builder prompt produces professional language, but without specific details from the `context` and `learnings` fields, it falls back on generic professional filler.

**How to catch it:** The specificity test — cross out the company name and role title. If the sentence could appear in ANY cover letter for ANY job, it's too generic. Good sentences contain details that only this person could have written.

### Inconsistency Between Resume and Cover Letter

**What it looks like:** The resume says one thing about an experience, and the cover letter says something different — or worse, contradictory.

```
Resume:  "Managed a team of 12 facilitators"
Letter:  "Coordinated scheduling for a small group of colleagues"

Resume:  "Reduced no-show rate by 15%"
Letter:  "Improved participant engagement" (where did the 15% go?)
```

**Why it happens:** The two builders run independently. They pull from the same YAML but make different selection and phrasing choices. If the user edits one document but not the other, they drift.

**How to catch it:** Read both documents together after generating them. Core facts (numbers, roles, outcomes) should be consistent even if the framing differs. The cover letter can add context the resume doesn't have, but it shouldn't contradict it.

---

## 6. Tips for Mentors

### How to Use This Knowledge During Sessions

1. **Start with the YAML, not the output.** If a resume doesn't look right, the first question is: "Is the experience profile complete and specific enough?" Garbage in, garbage out.

2. **Use the three-layer model to diagnose problems.** When something feels off:
   - Layer 1 problem → The YAML is vague, missing fields, or incomplete
   - Layer 2 problem → The translation is wrong (over, under, or stuffed)
   - Layer 3 problem → The formatting, tone, or structure needs adjustment

3. **Run the keyword match check.** After generating a resume, look at the keyword score (step 6b). Below 6/10 means the profile may not be a strong match — and that's okay to say out loud.

### When to Improve the YAML vs. the Output

```
Improve the YAML when...              Improve the output when...
─────────────────────────              ──────────────────────────

The experience section is vague        The phrasing feels over- or
("helped with stuff")                  under-translated

Actions are missing or generic         Keywords are being stuffed
("assisted the team")                  rather than naturally woven in

Outcomes are absent — no numbers,      The tone doesn't match the
no artifacts, no qualitative results   target company/industry

The context field is empty (cover      The bullet formula is wrong
letters will suffer most)              (using XYZ when there's no
                                       quantitative outcome)

Learnings are missing (the user        The story angle in the cover
hasn't reflected on growth)            letter is weak or generic

Keywords are missing or too broad      An experience that should be
                                       included was filtered out
```

**Rule of thumb:** If the problem is about *what* to say, fix the YAML. If the problem is about *how* it's being said, adjust the prompt output.

### How to Spot "Good Enough" vs. "Needs Another Pass"

A document is **good enough** when:

- [ ] Every bullet/paragraph connects to a specific job requirement
- [ ] Keywords appear naturally, not forced
- [ ] The user could defend every claim in an interview
- [ ] The cover letter tells a story the resume doesn't
- [ ] Reading it aloud doesn't make you cringe
- [ ] A hiring manager in the target industry would understand every line

A document **needs another pass** when:

- [ ] You spot any of the five failure modes from Section 5
- [ ] The keyword match score is below 6/10 and no gap was flagged
- [ ] The cover letter could work for any company with a name swap
- [ ] The resume includes experiences that aren't relevant to this role
- [ ] The user's actual strengths aren't the ones being highlighted
- [ ] The tone is wrong for the industry (e.g., academic tone for a startup)

### The Mentor's Diagnostic Flowchart

```
Generated document doesn't feel right
        │
        ▼
Is the YAML entry complete and specific?
        │
   No ──┤──→ Go back to Experience Capture.
        │    Coach the user to add specifics:
        │    context, numbers, learnings, keywords.
        │
   Yes ──┤
        │
        ▼
Is the right experience being selected?
        │
   No ──┤──→ The relevance filter missed something.
        │    Ask the builder to emphasize a different
        │    experience, or add keywords to the YAML
        │    entry to improve its match score.
        │
   Yes ──┤
        │
        ▼
Is the translation accurate?
        │
   No ──┤──→ Check the translation guide.
        │    Is the academic term being mapped to the
        │    right industry term? Is it over- or under-
        │    translated? Adjust the phrasing or add a
        │    bridge phrase.
        │
   Yes ──┤
        │
        ▼
Is the format/tone right for this job?
        │
   No ──┤──→ Adjust at Layer 3: change tone, swap
        │    bullet formulas, restructure sections.
        │
   Yes ──┤
        │
        ▼
The document is ready. Ship it.
```

---

> **Remember:** The system is designed so that the user builds their experience profile once and reuses it many times. The YAML is the investment; the generated documents are the returns. When in doubt, invest in the YAML.
