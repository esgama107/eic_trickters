# TODO — Baseline Test Insights

> Generated from the 10-persona baseline test (2026-03-20).
> Overall score: **3.85 / 5.00** — strong for direct-fit personas, weaker for
> STEM Applied, Creative, and career-pivot cases.

---

## High Priority (scored ≤ 3.50 or blocked ATS/callback)

### Add licensure section to schema
- **Source:** Personas 7 (Biology), 8 (Nursing), 10 (Education)
- **Problem:** Licensure (NCLEX-RN, NREMT, teaching license) is legally
  required for employment but is buried under certifications alongside
  optional courses. Licensure ≠ certification.
- **Fix:** Add a dedicated `licensure` section to the YAML schema with
  fields: name, issuing_body, status (active/pending/expected), date,
  license_number (optional).

### Add clinical/supervised hours field
- **Source:** Personas 3 (Psychology), 7 (Biology), 8 (Nursing)
- **Problem:** Clinical hours, practicum hours, and supervised field hours
  are critical hiring criteria in health/education but have no structured
  capture. The interview prompt doesn't probe for them.
- **Fix:** Add `supervised_hours` to experiences (type, total_hours,
  supervisor_title) and add a dedicated probe in Phase 2 for clinical/
  practicum experience types.

### Expand translation guide — missing archetypes
- **Source:** Personas 7-10 (Biology, Nursing, Design, Education)
- **Problem:** The translation guide has zero entries for Biology, Nursing,
  Health Sciences, Design, or Education. These archetypes had the lowest
  baseline scores (3.25-3.75).
- **Fix:** Add major-specific translation sections for: Biology/Pre-Med,
  Nursing/Health Sciences, Graphic Design/Visual Arts, Education/Teaching.

### Fix portfolio phase — not optional for creative fields
- **Source:** Persona 9 (Graphic Design)
- **Problem:** The portfolio capture phase is marked "optional" but for
  design, art, and UX roles the portfolio IS the primary hiring artifact.
  Treating it as optional signals it's unimportant.
- **Fix:** Make portfolio phase conditional: if experience type includes
  design/creative/freelance, portfolio becomes a required phase. Add
  `exhibition` as an experience type. Add `client` field for freelance work.

### Improve career-pivot keyword matching
- **Source:** Personas 2 (Math→Data Analyst), 7 (Biology→Research)
- **Problem:** Yumi scored 5/10 keywords, Rosa scored 4/10. Both are
  career-pivot cases where academic skills don't map directly to industry
  keywords. The prompt's gap analysis suggests reframing but doesn't help
  enough with the actual keyword translation.
- **Fix:** Enhance the resume builder's gap analysis to suggest SPECIFIC
  keyword substitutions (e.g., "statistical modeling" → "predictive
  analytics") and flag when keyword match is below 6/10 as a warning.

---

## Medium Priority (friction but functional)

### Add work authorization capture
- **Source:** Persona 2 (Yumi — international student)
- **Problem:** Work authorization status (visa type, OPT/CPT, sponsorship
  needs) is critical for international students but not captured anywhere.
  Recruiters screen for this early.
- **Fix:** Add optional `work_authorization` field to profile section.

### Add proficiency levels to technical skills
- **Source:** Personas 4 (Philosophy), 6 (Anthropology)
- **Problem:** Listing "R" or "Python" without proficiency level is
  misleading when the user only has basic exposure. Recruiters expect
  competency, not just awareness.
- **Fix:** Add optional proficiency tag to technical skills:
  `- skill: "R" proficiency: "basic"` (basic/intermediate/advanced/expert).

### Improve keyword brainstorming for non-industry personas
- **Source:** Personas 4 (Philosophy), 6 (Anthropology)
- **Problem:** When the capture prompt asks "what keywords would a recruiter
  search for?", humanities and social science students don't know — they've
  never used ATS systems or industry job boards.
- **Fix:** Add field-specific keyword suggestions or examples in the prompt.
  E.g., "For research-heavy roles, think: data analysis, literature review,
  qualitative methods, IRB compliance, report writing."

### Add populations_served field for service roles
- **Source:** Personas 8 (Nursing), 10 (Education)
- **Problem:** "Who did you serve?" is a key differentiator in education,
  social work, nursing, and nonprofit roles. The schema doesn't capture it.
- **Fix:** Add optional `populations_served` to experiences (e.g.,
  "pediatric patients", "Title I students", "adults with disabilities").

---

## Low Priority (nice to have)

### Add experience sub-type for academic roles
- **Source:** Multiple personas
- **Problem:** "Research" covers everything from a 2-week class project to a
  2-year funded lab position. Sub-types would help the resume builder
  prioritize.
- **Fix:** Consider adding optional `scope` field: course_project | semester
  | multi_year | funded | independent.

### Add "confidence nudges" per field in capture prompt
- **Source:** EIC major review (all 6 original majors)
- **Problem:** Philosophy and anthropology students undervalue their
  experiences more than engineering students. Generic encouragement isn't
  enough.
- **Fix:** Add field-aware encouragement. E.g., when type is "thesis",
  prompt could say: "A thesis shows you can do independent research, manage
  a long-term project, and present complex ideas — all valuable to employers."

---

## Baseline Scores (reference)

| # | Name | Major | Archetype | Score | Keywords | ATS | Callback |
|---|------|-------|-----------|-------|----------|-----|----------|
| 1 | Andrés | Mech. Engineering | STEM Quant | 4.75 | 10/10 | ✅ | ✅ |
| 5 | Priya | Marketing | Business | 4.75 | 8/10 | ✅ | ✅ |
| 3 | Jasmine | Psychology | Soc Sci Qual | 4.25 | 8/10 | ✅ | ⚠️ |
| 4 | Ciarán | Philosophy | Humanities | 3.75 | 8/10 | ⚠️ | ⚠️ |
| 6 | Kofi | Anthropology | Soc Sci Quant | 3.75 | 9/10 | ✅ | ⚠️ |
| 10 | María Elena | Education | Edu/Service | 3.75 | 10/10 | ✅ | ✅ |
| 2 | Yumi | Applied Math | STEM Quant | 3.50 | 5/10 | ❌ | ❌ |
| 9 | Leo | Graphic Design | Creative | 3.50 | 10/10 | ✅ | ⚠️ |
| 7 | Rosa | Biology | STEM Applied | 3.25 | 4/10 | ❌ | ❌ |
| 8 | Thandiwe | Nursing | STEM Applied | 3.25 | 10/10 | ✅ | ⚠️ |
