Below is a **concrete, repo‑ready answer to “How to get these”**, mapped exactly to each row in your table. I’ve prioritized **authoritative, reusable sources** (career centers, O\*NET, Indeed/LinkedIn) and called out **what to copy vs. what to synthesize** so this stays clean and non‑copyright‑problematic.

***

## 1. Action verb lists (by field)

### Best sources

*   **University career centers** publish curated verb lists broken down by function (research, teaching, communication, leadership).
    *   Example: UC Davis Career Center – Action Verb List  
        <https://careercenter.ucdavis.edu/resumes-and-materials/resumes/verb-list> [\[careercent...cdavis.edu\]](https://careercenter.ucdavis.edu/resumes-and-materials/resumes/verb-list)
    *   Indiana Tech (PDF, very comprehensive, categorized)  
        <https://careercenter.indianatech.edu/wp-content/uploads/sites/15/Action-Verb-List.pdf> [\[careercent...natech.edu\]](https://careercenter.indianatech.edu/wp-content/uploads/sites/15/Action-Verb-List.pdf)

*   **O\*NET** for occupation‑specific task language (more “what professionals say,” less “resume fluff”):
    *   O\*NET OnLine  
        <https://www.onetonline.org/> [\[onetonline.org\]](https://www.onetonline.org/)

### How to add to the repo

*   Create `/reference/action-verbs/`
    *   `research-verbs.md` (derived from O\*NET task statements)
    *   `teaching-verbs.md`
    *   `writing-communication-verbs.md`
*   **Do not copy verb lists wholesale**. Instead:
    *   Extract verbs
    *   De‑duplicate
    *   Tag by *use case* (analysis, facilitation, synthesis)

✅ This keeps it derivative, legal, and more useful for prompts.

***

## 2. ATS keyword glossary (per industry)

### Best sources

*   **Indeed job description libraries** (large, standardized corpus):
    *   Job description examples by industry  
        <https://www.indeed.com/hire/job-description-list> [\[indeed.com\]](https://www.indeed.com/hire/job-description-list)

*   **Jobscan / Rezi / Resume keyword aggregators** (explicitly analyze ATS patterns):
    *   Jobscan – Top resume keywords  
        <https://www.jobscan.co/blog/top-resume-keywords-boost-resume/> [\[jobscan.co\]](https://www.jobscan.co/blog/top-resume-keywords-boost-resume/)
    *   Rezi – ATS keywords by industry  
        <https://www.rezi.ai/posts/ats-resume-keywords> [\[rezi.ai\]](https://www.rezi.ai/posts/ats-resume-keywords)

### How to add to the repo

*   Create `/reference/ats-keywords/`
    *   `education.md`
    *   `nonprofit.md`
    *   `policy.md`
    *   `communications.md`

Each file should contain:

*   **Skill nouns** (e.g., “curriculum development”)
*   **Tool nouns** (e.g., “Qualtrics,” “SPSS”)
*   **Outcome nouns** (e.g., “stakeholder engagement”)

⚠️ Avoid copying proprietary lists verbatim. Instead:

*   Aggregate across sources
*   Keep only **high‑frequency, cross‑posting terms**

***

## 3. STAR / CAR example bank (non‑technical roles)

### Best sources

*   **Indeed career guides** (clear, non‑technical examples):
    *   STAR method resume examples  
        <https://www.indeed.com/career-advice/resumes-cover-letters/star-method-resume> [\[indeed.com\]](https://www.indeed.com/career-advice/resumes-cover-letters/star-method-resume)

*   **LinkedIn career coaching articles** (CAR/STAR comparisons):
    *   Transforming resume bullets with CAR/STAR  
        <https://www.linkedin.com/pulse/transforming-resume-bullets-car-star-par-models-scott-4dmwe> [\[linkedin.com\]](https://www.linkedin.com/pulse/transforming-resume-bullets-car-star-par-models-scott-4dmwe)

### How to add to the repo

*   Create `/reference/star-examples/`
    *   `tutoring.md`
    *   `fieldwork.md`
    *   `writing-editing.md`
    *   `program-coordination.md`

Each entry should be:

    Context:
    Action:
    Result:

✳️ **Author your own examples** based on common scenarios (this is safer and more prompt‑aligned than copying).

***

## 4. Job description samples (practice corpus)

### Best sources

*   **Indeed job description templates**  
    <https://www.indeed.com/hire/resources/job-description-examples> [\[indeed.com\]](https://www.indeed.com/hire/resources/job-description-examples)
*   **LinkedIn job descriptions** (for realism and tone)  
    <https://www.linkedin.com/showcase/job-descriptions> [\[linkedin.com\]](https://www.linkedin.com/showcase/job-descriptions)

### How to add to the repo

*   Create `/reference/job-descriptions/`
    *   3–5 **summarized** JDs per target field

Each summary should include:

*   Role title
*   Core responsibilities (bulleted)
*   Common keywords (tagged)

✅ Summaries + keyword tags avoid copyright issues and are prompt‑friendly.

***

## 5. Field‑to‑industry translation guide (the “pivot layer”)

### Best sources (conceptual grounding)

*   Academic → Industry translation guides:
    *   UseResume AI guide  
        <https://useresume.ai/blog/posts/academic-to-industry-resume-translation-a-complete-guide> [\[useresume.ai\]](https://useresume.ai/blog/posts/academic-to-industry-resume-translation-a-complete-guide)
    *   The Interview Guys – skill translation  
        <https://blog.theinterviewguys.com/converting-academic-achievements-to-workplace-skills/> [\[blog.thein...ewguys.com\]](https://blog.theinterviewguys.com/converting-academic-achievements-to-workplace-skills/)

### How to add to the repo (this one **must be authored**)

*   Create `/reference/translation-guide.md`

Structure it as a **mapping table**:

| Academic activity | Industry phrasing         |
| ----------------- | ------------------------- |
| Thesis defense    | Stakeholder presentation  |
| Literature review | Market / policy analysis  |
| Grant writing     | Business case development |

This becomes the **core intelligence layer** for your prompts.

***

## Recommended repo structure (final)

    /reference
      /action-verbs
      /ats-keywords
      /star-examples
      /job-descriptions
      translation-guide.md

This structure directly strengthens:

*   Resume prompts
*   Cover letter prompts
*   Career‑pivot prompts
*   ATS‑aware rewrite prompts

***

If you want, next we can:

*   Turn this into a **one‑page “reference ingestion prompt”** for Copilot, or
*   Auto‑generate **starter markdown files** for each folder using this sourcing strategy.
