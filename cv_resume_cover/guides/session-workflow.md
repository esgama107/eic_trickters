# Mentorship Session Workflow Guide

> A practical facilitator's guide for running the CV/Resume/Cover Letter prompt kit across mentorship sessions. Designed for GMI mentors and mentees.

---

## How this guide works

The prompt kit has four tools:

| Tool | What it does | Time |
|------|-------------|------|
| [Experience Capture](../prompts/experience-capture.md) | Interview-style profile builder (8 phases) | 45-60 min |
| [Experience Update](../prompts/experience-update.md) | Add or change one thing in your profile | 5-10 min |
| [Resume Builder](../prompts/resume-builder.md) | Generate a tailored resume optimized for ATS (Applicant Tracking Systems — software that filters resumes) | 20-30 min |
| [Cover Letter Builder](../prompts/cover-letter-builder.md) | Generate a narrative cover letter | 20-30 min |

This guide maps those tools to a **3-session model** — roughly 60 minutes each — that takes a mentee from zero to a complete application package. You can compress or expand this model (see [Adapting the 3-session model](#adapting-the-3-session-model) below).

**What you'll produce:**
- Session 1 → Completed `experience-profile.yaml`
- Session 2 → Tailored resume (v1)
- Session 3 → Cover letter (v1) + iteration plan

---

## Session 1: Capture & Explore

**Goal:** Build a complete experience profile the mentee can use for every future application.

**Time:** ~60 minutes

### Before the session

**Mentor:**
- Read the [Experience Capture prompt](../prompts/experience-capture.md) so you know what the interview covers
- Have the [experience profile template](../schema/experience-profile-template.yaml) open for reference
- Decide which chat platform you'll use (Copilot, Claude, ChatGPT — any works)

**Mentee:**
- Think about your experiences — jobs, internships, projects, volunteering, research, teaching, thesis work, competitions. Write a rough list if it helps.
- Have your LinkedIn or existing resume open for reference (not required, but useful for jogging memory)

### Quick reference — the 8 interview phases

| Phase | Topic | What happens |
|-------|-------|-------------|
| 1 | Basics | Name, contact, location, professional summary |
| 2 | Career Direction | Interests, target industries, values, goals |
| 3 | Experiences | For each: type, actions, outcomes, challenges, learnings (longest phase) |
| 4 | Education | Degrees, institutions, highlights |
| 5 | Skills | Technical, interpersonal, languages |
| 6 | Publications & Portfolio | Papers, creative work, portfolio pieces |
| 7 | Awards & Certifications | Honors, licenses, professional certifications |
| 8 | Wrap-Up | Review, confirm, output YAML file |

### Running the session

**~45 minutes — Experience capture interview**

1. **Open your chat assistant** and paste the Experience Capture prompt
2. **The mentor coaches, the AI interviews.** The AI asks one question at a time. The mentor's job is to:
   - Help the mentee articulate what they actually did ("You mentioned you helped with the project — what specifically was YOUR contribution?")
   - Push for specifics when answers are vague ("Can you estimate how many people used it? Even a rough number helps.")
   - Catch things the mentee dismisses ("That tutoring experience absolutely counts — let's capture it")
   - Validate that nothing important is missing ("Did you do anything outside of school — volunteering, freelance, side projects?")
3. **Watch for the checkpoint.** After all experiences are captured (end of Phase 3), the AI offers to save a partial YAML. Take this checkpoint — it's a good moment to pause, stretch, and review what's been captured so far.
4. **Continue through Phases 4-8** (education, skills, publications, awards, wrap-up). These go faster.

**~15 minutes — Review and setup**

5. **Review the output together.** Read through the completed YAML. Look for:
   - Missing experiences (things the mentee forgot)
   - Weak outcomes ("helped with the project" → needs more detail)
   - Skills that were mentioned in experiences but not in the skills inventory
   - Anything that feels wrong or incomplete
6. **Save the file.** The mentee saves it as `my-experience-profile.yaml` (or whatever name they prefer). This is their portable career record.
7. **Set up chat memory.** Follow the [Memory Integration Guide](memory-integration.md) to save key facts to the platform's memory. This makes future sessions smoother.

### What the mentor should watch for

- **The mentee saying "that doesn't count."** It almost always counts. Tutoring, thesis work, volunteering, class projects — the prompt kit treats all of these as valid experiences. Gently push back.
- **Vague outcomes.** "I helped the team" is not an outcome. "I designed the survey instrument used to collect data from 150 participants" is. Coach the mentee to be specific.
- **The mentee rushing.** This is the foundation for everything else. It's worth spending the full 45 minutes. A thin profile produces thin resumes.
- **Missing the career narrative.** Phase 2 (career direction) matters a lot for cover letters later. Make sure the mentee gives real answers, not "I don't know" to every question.

### Session 1 output

✅ Completed `experience-profile.yaml`
✅ Chat memory set up (optional but recommended)

---

## Between Session 1 and Session 2 — Checklist

The mentee should complete these before Session 2:

- [ ] Save `experience-profile.yaml` securely (cloud drive, USB, wherever you keep important files)
- [ ] Re-read the profile — add anything you forgot (use the [Experience Update prompt](../prompts/experience-update.md) if needed)
- [ ] Find 2-3 job descriptions you're genuinely interested in
- [ ] Research the companies behind those JDs (About page, mission statement, recent news)
- [ ] Set up chat memory per the [Memory Integration Guide](memory-integration.md) if you didn't do it in Session 1
- [ ] (Optional) If you remembered a new experience or outcome, run the [Experience Update prompt](../prompts/experience-update.md) to add it — it takes 5-10 minutes

**Why this matters:** Session 2 is about targeting a specific role. If the mentee shows up without job descriptions, you'll spend 20 minutes finding one instead of building a resume.

---

## Session 2: Resume & Target

**Goal:** Produce a tailored resume for a specific job the mentee wants.

**Time:** ~60 minutes

### Before the session

**Mentor:**
- Read the [Resume Builder prompt](../prompts/resume-builder.md), especially the analysis phase
- Glance at the [translation guide](../reference/translation-guide.md) if your mentee is pivoting between fields

**Mentee:**
- Bring 2-3 job descriptions (pasted or as links)
- Bring your `experience-profile.yaml`
- Have notes on what attracted you to each role

### Running the session

**~10 minutes — JD review and selection**

1. **Review the job descriptions together.** For each one, quickly discuss:
   - Does the mentee meet at least 60-70% of the requirements?
   - Is this a realistic target or a stretch?
   - Which one is the strongest fit?
2. **Pick one JD** to build the resume around. Save the others for later iterations.

**~20 minutes — Resume generation and analysis**

3. **Upload the YAML + JD** to the chat assistant and paste the Resume Builder prompt.
4. **Read the analysis phase together.** The AI produces an analysis before the resume. This is a teaching moment:
   - **Top 5 requirements:** Does the mentee understand what the employer actually wants?
   - **Best matches:** Does the mentee see how their experiences connect to the role?
   - **Keyword translation:** This is where the magic happens. The AI maps the mentee's language to the employer's language. Talk through why "thesis research" becomes "independent research project" and "tutoring" becomes "individualized instruction."
   - **Gaps:** Discuss honestly. A gap isn't a dealbreaker — it's information. What can be reframed? What should be left alone?
   - **Keyword match score:** Aim for 7+/10. If it's below 6, this might not be the right role.

**~30 minutes — Iteration and coaching**

5. **Review the generated resume line by line.** Look for:
   - Bullet points that are too vague ("Assisted with data analysis" → "Analyzed survey responses from 150 participants using SPSS, identifying three statistically significant trends")
   - Missing keywords the JD emphasizes
   - Experiences that should be swapped in or out
   - Summary that doesn't match the target role
   - Formatting issues that would trip up ATS
6. **Iterate.** Ask the AI to revise specific sections. Common asks:
   - "Rewrite the third bullet under [experience] to emphasize [keyword]"
   - "Swap out [experience A] for [experience B] — it's a better fit"
   - "Make the summary more specific to data analytics roles"
7. **Check the keyword match score again** after revisions. Did coverage improve?

### What the mentor should watch for

- **Padding.** The mentee (or the AI) may stretch the truth. "Assisted with" doesn't become "Led." Honesty is non-negotiable — it falls apart in interviews.
- **Kitchen-sink resumes.** A focused resume beats a comprehensive one. If an experience isn't relevant to this role, it doesn't belong on this resume. (It's safe in the YAML file — nothing is lost.)
- **Generic summaries.** "Results-driven professional seeking opportunities" is useless. The summary should name the field, the key skills, and why this role.
- **Ignoring the analysis.** The analysis phase teaches the mentee how to think about job applications. Don't skip it to save time — it's the most valuable part.

### Session 2 output

✅ Tailored resume v1
✅ Mentee understands keyword matching and ATS basics

---

## Between Session 2 and Session 3 — Checklist

The mentee should complete these before Session 3:

- [ ] Re-read the resume — note anything that feels wrong, weak, or off
- [ ] Apply any immediate feedback from your mentor (fix bullet points, adjust summary, etc.)
- [ ] Pick ONE job + company for the cover letter (can be the same one from Session 2 or a different one)
- [ ] Research that company deeply: About page, mission, values, recent news, team, products
- [ ] Write 3-5 bullet points about why you're interested in THIS specific company
- [ ] Review the [translation guide](../reference/translation-guide.md) for your field (if applicable)

**Why this matters:** The cover letter lives or dies on company-specific detail. If the mentee shows up saying "I don't know much about them," the letter will be generic — and generic cover letters fail the differentiation check.

---

## Session 3: Cover Letter & Polish

**Goal:** Complete the application package and set up a plan for iterating on future applications.

**Time:** ~60 minutes

### Before the session

**Mentor:**
- Read the [Cover Letter Builder prompt](../prompts/cover-letter-builder.md), especially the tone options and narrative rules
- Review the mentee's resume from Session 2

**Mentee:**
- Bring your `experience-profile.yaml`
- Bring the target JD and your company research notes
- Bring the resume from Session 2 (for consistency checking)

### Running the session

**~15 minutes — Company research review**

1. **Review the mentee's company research.** Ask:
   - "Why this company specifically — not just this role?"
   - "What do they do that excites you?"
   - "What values do they talk about? Do any of yours align?"
2. **Identify the story angle.** This is the single narrative thread that ties the mentee to the role. Examples:
   - "A researcher who wants to move from studying problems to solving them"
   - "A community volunteer who wants to bring grassroots empathy to healthcare tech"
   - "A career changer whose teaching skills are exactly what this training role needs"
3. **Pick a tone.** The Cover Letter Builder offers four: Professional, Conversational, Academic, Mission-driven. Help the mentee choose based on the company culture.

**~20 minutes — Cover letter generation**

4. **Upload the YAML + JD + company info** and paste the Cover Letter Builder prompt.
5. **Read the analysis together**, just like Session 2:
   - **Top 3 requirements:** Are these the same as the resume, or different?
   - **Company alignment points:** Does the AI connect the mentee's values/narrative to the company?
   - **The story angle:** Does it feel right? If not, suggest a different angle.
   - **Gaps:** The cover letter should NOT try to cover gaps by making things up. Better to focus on strengths.
6. **Read the generated letter aloud.** Seriously — reading it aloud catches awkward phrasing, robotic tone, and sentences that don't flow.

**~25 minutes — Polish and planning**

7. **Compare resume + cover letter.** Check:
   - Does the cover letter repeat the resume? (It shouldn't — it should tell the story BEHIND the bullet points)
   - Are they consistent? (Same dates, same job titles, same framing)
   - Does the cover letter add context the resume can't? (Motivation, learning, values)
8. **Check the company alignment and differentiation scores.** The AI outputs these. If the letter would work for any company with a name swap, it's too generic. Fix it.
9. **Iterate.** Common tweaks:
   - "Strengthen the opening — start with a specific moment instead of a statement"
   - "Add a reference to their recent product launch"
   - "Try the mission-driven tone instead of professional"
10. **Set up the iteration plan.** Discuss:
    - How will the mentee generate variants for other applications?
    - When should they update their experience profile?
    - Do they need a follow-up session?

### What the mentor should watch for

- **Resume rehash.** The cover letter should NOT be "my resume, but in paragraphs." It should add motivation, context, and story. If the mentee is just restating bullet points, push them to use the "learnings" and "career_narrative" fields from their YAML.
- **Generic company references.** "I admire your company's mission" means nothing. "Your recent expansion of telehealth services into rural communities aligns with my fieldwork experience in underserved areas" means everything.
- **Dishonest framing.** If the mentee doesn't meet a requirement, the letter shouldn't pretend they do. Frame growth potential honestly.
- **The opening line.** "I am writing to apply for the position of..." is banned. The prompt explicitly forbids it. If the AI generates it anyway, ask for a rewrite.

### Session 3 output

✅ Cover letter v1
✅ Resume + cover letter consistency verified
✅ Iteration plan for future applications

---

## After Session 3 — Ongoing Checklist

- [ ] Finalize resume and cover letter formatting (PDF export, clean layout)
- [ ] Generate resume variants for other job applications (re-run the Resume Builder with different JDs)
- [ ] Generate cover letter variants for other companies (re-run the Cover Letter Builder)
- [ ] Update your experience profile when you gain new experiences (use the [Experience Update prompt](../prompts/experience-update.md))
- [ ] Every 3 months, re-read your profile and refresh your career narrative
- [ ] Schedule a follow-up session with your mentor if you need help iterating

---

## For mentors: Coaching tips

### Coach, don't do

Your job is to help the mentee build the skill, not to build the document for them. That means:

- **Ask questions, don't dictate answers.** Instead of "Change this bullet to say X," try "What was the actual impact of that work? Let's make this bullet show it."
- **Let the mentee interact with the AI.** They need to learn how to prompt, iterate, and evaluate output. If you're typing everything, they won't be able to do this on their own.
- **Teach the "why."** Don't just say "this bullet is weak." Explain WHY — "A recruiter scanning this in 6 seconds won't understand what you actually did. Can we make it more concrete?"

### When to push back

- **Vague descriptions.** "Helped with the project" isn't a resume bullet. Push for the specific contribution.
- **Inflated claims.** If the mentee "led" a team they were a member of, correct it. Honesty survives interviews; exaggeration doesn't.
- **Skipping company research.** If the mentee hasn't researched the company for the cover letter, pause and do it together. A generic letter wastes everyone's time.
- **Dismissing experiences.** EIC (early-in-career) mentees routinely undervalue class projects, tutoring, volunteering, and thesis work. These are real experiences. Help them see that.

### What to look for in generated output

- **Keyword coverage.** The resume builder shows a keyword match score. Aim for 7+/10.
- **ATS formatting.** No tables, no columns, no graphics, standard section headers. The prompt handles this, but verify.
- **Action verbs.** Every bullet should start with a strong verb. "Responsible for" is not an action verb.
- **Outcome specificity.** Quantitative is great ("reduced processing time by 30%"), but qualitative outcomes are valid too ("published peer-reviewed paper," "improved onboarding process").
- **Cover letter differentiation.** Remove the company name — does the letter still make sense for any company? If yes, it's too generic.

### Red flags in resumes

- Bullets that start with "Responsible for" or "Duties included"
- No outcomes — just lists of tasks
- Keyword stuffing (cramming in terms that don't match actual experience)
- Inconsistent dates or gaps that aren't addressed
- Skills listed that can't be backed up by any experience in the profile
- Generic professional summary that could apply to anyone

### Red flags in cover letters

- Opens with "I am writing to apply for..."
- Reads like the resume in paragraph form
- Mentions the company name once (in the address) and never again
- Claims skills or experiences not present in the profile
- Tone mismatch (conversational letter for a government role, or academic letter for a startup)
- Could be sent to any company with a name swap

---

## Adapting the 3-session model

### What if you only have 1 session?

Compress to 60 minutes:

| Block | Time | Activity |
|-------|------|----------|
| Capture (abbreviated) | 30 min | Run experience capture, focus on 2-3 strongest experiences + education + skills. Skip portfolio/awards unless critical. |
| Resume | 20 min | Pick one JD, generate resume, do one round of iteration. |
| Wrap-up | 10 min | Review output, set up the mentee to run the cover letter builder on their own. |

**Trade-offs:** The experience profile will be thinner. The mentee should go back and run the full capture on their own to fill in gaps. Send them the [Experience Update prompt](../prompts/experience-update.md) for adding what was missed.

### What if you have 2 sessions?

| Session | Time | Focus |
|---------|------|-------|
| Session 1 | 60 min | Full experience capture (all 8 phases) |
| Session 2 | 60 min | Resume (30 min) + Cover letter (30 min) — pick one JD/company, generate both, iterate together |

**Trade-offs:** Less iteration time on each document. The mentee can continue iterating async between sessions.

### What if the mentee needs 4+ sessions?

Common reasons to extend:

- **Many experiences to capture** (career changers, people with 5+ roles) — Split Session 1 into two capture sessions. Use the checkpoint feature at the end of Phase 3.
- **Multiple target roles** (different industries or functions) — Add sessions to generate resume/cover letter variants for each target. Each variant takes 30-40 minutes.
- **Weak writing or self-awareness** — Add a session between capture and resume to review and strengthen the profile. Use the Experience Update prompt to refine outcomes and keywords.
- **Interview prep** — The profile and resume are excellent prep for behavioral interviews. Add a session to practice STAR-format answers using the captured experiences.

### Session-count guide

| Mentee situation | Recommended sessions |
|-----------------|---------------------|
| EIC, 1-2 experiences, one target role | 2 sessions |
| EIC, 3-5 experiences, one target role | 3 sessions (standard model) |
| Career changer, many experiences | 4 sessions (2 capture + 1 resume + 1 cover letter) |
| Multiple target roles or industries | 3 + 1 per additional target |
| Mentee who can work independently | 1-2 sessions + async iteration |

---

## Using the tools asynchronously

The mentee doesn't have to wait for a session to use the prompt kit. In fact, **async use is encouraged** — it makes live sessions more productive.

### What the mentee can do on their own

| Task | Tool | When |
|------|------|------|
| Add a forgotten experience | [Experience Update](../prompts/experience-update.md) | Any time — the sooner the better while details are fresh |
| Generate a resume draft | [Resume Builder](../prompts/resume-builder.md) | After Session 1, with any JD |
| Generate a cover letter draft | [Cover Letter Builder](../prompts/cover-letter-builder.md) | After Session 2, with any JD + company info |
| Update skills or summary | [Experience Update](../prompts/experience-update.md) | After gaining new skills or shifting focus |

### The async-then-review pattern

This is the most efficient way to use mentor time:

1. **Mentee runs the prompt on their own** — generates a resume or cover letter draft
2. **Mentee brings the output to the next session** — along with the JD and any questions
3. **Mentor reviews and coaches** — focuses on quality, framing, and strategy instead of running the tool together

This works especially well after the first session, when the mentee has seen how the process works and can drive it independently.

### Tips for async success

- **Always upload the full YAML.** Don't try to describe your experiences from memory — that defeats the purpose of the system.
- **Save every version.** Name files clearly: `resume-google-analyst-v1.md`, `cover-letter-msft-pm-v2.md`. You'll want to compare across iterations.
- **Note your questions.** If the AI generates something you're unsure about, write down the question and bring it to your mentor. Don't just accept output that feels wrong.
- **Update your profile first.** If you've gained new experiences since Session 1, run the Experience Update prompt BEFORE generating new documents. Stale profiles produce stale output.

---

## Quick reference: The full workflow

```
SESSION 1                    BETWEEN 1→2                SESSION 2
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│ Experience      │     │ ☐ Save YAML      │     │ Review JDs      │
│ Capture         │     │ ☐ Review profile  │     │ together        │
│ (8 phases)      │────▶│ ☐ Find 2-3 JDs   │────▶│                 │
│                 │     │ ☐ Research cos    │     │ Generate resume │
│ Review + save   │     │ ☐ Set up memory   │     │ + analysis      │
│ Set up memory   │     │ ☐ Update profile? │     │                 │
└─────────────────┘     └──────────────────┘     │ Iterate + coach │
                                                  └────────┬────────┘
                                                           │
                         BETWEEN 2→3                       │
                    ┌──────────────────┐                    │
                    │ ☐ Review resume   │                    │
                    │ ☐ Apply feedback  │◀───────────────────┘
                    │ ☐ Pick 1 company  │
                    │ ☐ Deep research   │
                    │ ☐ Write "why us"  │
                    └───────┬──────────┘
                            │
                     SESSION 3                    ONGOING
                ┌─────────────────┐     ┌──────────────────┐
                │ Review company  │     │ ☐ Finalize format │
                │ research        │     │ ☐ Generate more   │
                │                 │────▶│   variants        │
                │ Generate cover  │     │ ☐ Update profile  │
                │ letter          │     │ ☐ Quarterly review│
                │                 │     │ ☐ Follow-up?      │
                │ Polish + plan   │     └──────────────────┘
                └─────────────────┘
```

---

*This guide is part of the [GMI Mentorships](../../README.md) project. For setup, see the [Memory Integration Guide](memory-integration.md). For the prompt kit itself, see the [prompts](../prompts/) directory.*
