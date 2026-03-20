# Test Personas — Resume/CV Prompt Kit Evaluation

> **Purpose:** Standardized test inputs for automated review agents evaluating the
> [Experience Capture](../prompts/experience-capture.md) and
> [Resume Builder](../prompts/resume-builder.md) prompt kits.
>
> **How many:** 10 personas across 7 archetypes + 1 wildcard.
>
> **Design principles:** archetype coverage, realistic EIC profiles, varied friction
> points, diverse backgrounds, reusable structure.

---

## Coverage Matrix

| # | Name                  | Archetype                    | Major                  | Pivot Difficulty |
|---|-----------------------|------------------------------|------------------------|------------------|
| 1 | Andrés Villanueva     | STEM Quantitative            | Mechanical Engineering | Low              |
| 2 | Yumi Nakamura         | STEM Quantitative            | Applied Mathematics    | Medium           |
| 3 | Jasmine Carter        | Social Science Qualitative   | Psychology             | Low              |
| 4 | Ciarán O'Donovan      | Humanities                   | Philosophy             | High             |
| 5 | Priya Mehta           | Business / Applied           | Marketing              | Low              |
| 6 | Kofi Asante           | Social Science Quantitative  | Cultural Anthropology  | Medium           |
| 7 | Rosa Delgado-Peña     | STEM Applied                 | Biology (Pre-Med)      | Medium           |
| 8 | Thandiwe Nkosi        | STEM Applied                 | Nursing (BSN)          | Low              |
| 9 | Leo Fujimoto          | Creative / Design            | Graphic Design         | Medium           |
| 10| María Elena Ríos      | Education / Service (wildcard)| Elementary Education  | Low              |

---

## Friction Map

Each persona is designed to stress-test a **different** weakness in the prompt kits.

| # | Persona             | Primary Friction Point                                           | Prompt Phase Most Affected           |
|---|---------------------|------------------------------------------------------------------|--------------------------------------|
| 1 | Andrés Villanueva   | Quantifying capstone/project outcomes vs. industry work          | Experience Capture → outcomes        |
| 2 | Yumi Nakamura       | Translating theoretical/academic work into professional value    | Resume Builder → career pivot check  |
| 3 | Jasmine Carter      | IRB compliance, clinical hours, and qualitative methods framing  | Experience Capture → skills/type     |
| 4 | Ciarán O'Donovan    | Reframing abstract humanities skills; "irrelevant" retail work   | Resume Builder → pivot + reframing   |
| 5 | Priya Mehta         | Shallow depth on many tools; metrics without substance           | Resume Builder → bullet formulas     |
| 6 | Kofi Asante         | Fieldwork as professional experience; non-standard outcomes      | Experience Capture → type + outcomes |
| 7 | Rosa Delgado-Peña   | Dual-path candidate (med school OR industry); certification list | Resume Builder → tailoring           |
| 8 | Thandiwe Nkosi      | Clinical rotations as "experience"; licensure; shift-based work  | Experience Capture → structure       |
| 9 | Leo Fujimoto        | Portfolio-first field; freelance legitimacy; non-text deliverables| Resume Builder → ATS + sections      |
| 10| María Elena Ríos    | Practicum-heavy; first-gen framing; vulnerable populations       | Experience Capture → tone/coaching   |

---

## Usage Guide

### Running a full pipeline test

1. **Pick a persona** from the list below.
2. **Feed the persona to a review agent** with instructions like:

   > "You are role-playing as **[Persona Name]**. Walk through the
   > [Experience Capture prompt](../prompts/experience-capture.md) as this person,
   > answering each question based on the persona details below. Then take the
   > resulting YAML profile and run it through the
   > [Resume Builder prompt](../prompts/resume-builder.md) targeting the persona's
   > `target_job` in their `target_industry`."

3. **Evaluate the output** against the persona's `tests` field — does the resume
   capture the right experiences? Does it handle the friction point well?

### Quick single-prompt test

To test only the Resume Builder, convert a persona's data directly into a
`experience-profile.yaml` using the
[schema template](../schema/experience-profile-template.yaml), then feed it
with a realistic job description for the persona's `target_job`.

### Batch testing

Agents can iterate over all 10 personas programmatically. Each persona block
below is structured identically so it can be parsed or extracted by script.

### What to look for

- **Experience Capture:** Does the prompt elicit enough detail from this persona's
  background type? Does it handle non-traditional experience types (fieldwork,
  clinical rotations, freelance) without forcing them into "job" framing?
- **Resume Builder:** Does the career pivot check fire when it should? Are bullet
  points using the right formula (XYZ vs. CAR vs. Narrative)? Does ATS
  optimization work for portfolio/creative fields?

---

## Personas

---

### Persona 1: Andrés Villanueva

```yaml
archetype: "STEM Quantitative — Engineering"
major: "Mechanical Engineering"
tests: "Technical skills listing, project-based experience, quantifying capstone outcomes vs. industry outcomes, team leadership framing"
graduation: "2024"
gpa: "3.52"
background_notes: "First-generation college student from Tucson, AZ. Parents immigrated from Sonora, Mexico. Commuted to campus; worked part-time through college."

experiences:
  - title: "Capstone Team Lead"
    organization: "University of Arizona — Senior Design Program"
    type: "project"
    duration: "Aug 2023 – May 2024"
    key_details: "Led a 5-person team designing a solar-powered water desalination unit for rural communities. Managed project timeline using Gantt charts, conducted FEA simulations in ANSYS, and presented final prototype to a panel of industry judges. Prototype achieved 92% salt rejection rate in lab testing."

  - title: "Mechanical Engineering Intern"
    organization: "Raytheon Missiles & Defense, Tucson, AZ"
    type: "internship"
    duration: "May 2023 – Aug 2023"
    key_details: "Supported the thermal management team by running CFD simulations in STAR-CCM+ and updating legacy SolidWorks assemblies. Created 15+ engineering change orders (ECOs) and documented test procedures for environmental stress screening."

  - title: "Undergraduate Research Assistant"
    organization: "UArizona Renewable Energy Lab"
    type: "research"
    duration: "Jan 2022 – May 2023"
    key_details: "Assisted a PhD student with experimental testing of thermoelectric generators. Ran data acquisition using LabVIEW, maintained lab equipment, and co-authored a conference poster presented at ASME IMECE 2023."

  - title: "Math Tutor"
    organization: "Think Tank Tutoring Center, UArizona"
    type: "teaching"
    duration: "Sep 2021 – May 2023"
    key_details: "Tutored 10-15 students per week in Calculus I-III and Differential Equations. Developed supplemental worksheets for common sticking points. Received a 4.8/5.0 average student rating."

education:
  degree: "B.S. Mechanical Engineering"
  institution: "University of Arizona"
  highlights:
    - "Senior Design Showcase — 2nd Place"
    - "Dean's List (5 semesters)"
    - "Relevant coursework: Thermodynamics, Fluid Mechanics, Heat Transfer, FEA, Controls"

skills:
  technical:
    - "SolidWorks"
    - "ANSYS (FEA)"
    - "STAR-CCM+ (CFD)"
    - "MATLAB"
    - "LabVIEW"
    - "Python (NumPy, Matplotlib)"
    - "GD&T"
    - "3D Printing (FDM)"
  interpersonal:
    - "Team leadership"
    - "Technical presentation"
    - "Cross-functional collaboration"
    - "Mentoring"
  languages:
    - "English (native)"
    - "Spanish (native)"

target_job: "Mechanical Design Engineer I"
target_industry: "Aerospace & Defense"
pivot_difficulty: "low"
```

---

### Persona 2: Yumi Nakamura

```yaml
archetype: "STEM Quantitative — Mathematics"
major: "Applied Mathematics"
tests: "Translating theoretical/academic work into professional value, thin industry experience, research-heavy profile, math-as-skill-not-job framing"
graduation: "2024"
gpa: "3.88"
background_notes: "International student from Osaka, Japan, studying on an F-1 visa. Seeking OPT employment. Strong academic record but no traditional industry internship. Unsure how to market herself outside academia."

experiences:
  - title: "Research Assistant — Computational Modeling"
    organization: "Portland State University, Dept. of Mathematics & Statistics"
    type: "research"
    duration: "Sep 2022 – Jun 2024"
    key_details: "Developed numerical models for fluid-structure interaction problems using MATLAB and Python. Implemented finite element solvers from scratch and validated results against published benchmarks. Contributed to a journal manuscript (under review) on adaptive mesh refinement techniques."

  - title: "Calculus Tutor"
    organization: "PSU Learning Center"
    type: "teaching"
    duration: "Sep 2022 – Jun 2024"
    key_details: "Tutored 8-12 undergraduates per week in Calculus I-II and Linear Algebra. Created visual explainer handouts for abstract concepts like eigenvalue decomposition. Trained 3 new tutors on pedagogical best practices."

  - title: "Data Analysis Volunteer"
    organization: "Portland Homeless Family Solutions (nonprofit)"
    type: "volunteering"
    duration: "Jan 2024 – May 2024"
    key_details: "Cleaned and analyzed 2 years of shelter intake data using Python (Pandas) to identify seasonal demand patterns. Produced a report with visualizations that the nonprofit used in a grant application."

  - title: "Honors Thesis"
    organization: "Portland State University"
    type: "thesis"
    duration: "Sep 2023 – Jun 2024"
    key_details: "Wrote a 60-page thesis titled 'Convergence Analysis of Adaptive FEM for Elliptic PDEs.' Defended before a 3-member faculty committee. Received departmental honors distinction."

education:
  degree: "B.S. Applied Mathematics (Honors)"
  institution: "Portland State University"
  highlights:
    - "Summa Cum Laude"
    - "Departmental Honors in Mathematics"
    - "Relevant coursework: Numerical Analysis, PDEs, Probability Theory, Statistical Learning, Scientific Computing"
    - "Math Club Vice President"

skills:
  technical:
    - "MATLAB"
    - "Python (NumPy, SciPy, Pandas, Matplotlib)"
    - "LaTeX"
    - "Finite Element Methods"
    - "Statistical modeling"
    - "Data visualization"
    - "Git"
    - "Linux/Bash"
  interpersonal:
    - "Technical writing"
    - "Peer mentoring"
    - "Cross-cultural communication"
    - "Patience in teaching complex concepts"
  languages:
    - "Japanese (native)"
    - "English (fluent)"

target_job: "Data Analyst"
target_industry: "Technology / Analytics"
pivot_difficulty: "medium"
```

---

### Persona 3: Jasmine Carter

```yaml
archetype: "Social Science Qualitative"
major: "Psychology (Clinical Track)"
tests: "Clinical hours framing, IRB experience, qualitative methods, helping-profession language, SPSS/EEG as technical skills, peer counselor role legitimacy"
graduation: "2024"
gpa: "3.61"
background_notes: "Black woman from Atlanta, GA. Attended a large public research university on a merit scholarship. Considering clinical psychology PhD programs but also open to UX research or people operations roles."

experiences:
  - title: "Research Assistant — Emotion Regulation Lab"
    organization: "Georgia State University, Dept. of Psychology"
    type: "research"
    duration: "Jan 2022 – May 2024"
    key_details: "Collected EEG data from 80+ participants across two IRB-approved studies on emotional reactivity. Preprocessed EEG signals using EEGLAB/MATLAB, ran statistical analyses in SPSS, and coded qualitative interview transcripts using thematic analysis. Co-authored a poster presented at APS 2024."

  - title: "Practicum Student"
    organization: "Grady Memorial Hospital — Behavioral Health Unit"
    type: "practicum"
    duration: "Sep 2023 – Apr 2024"
    key_details: "Completed 200+ clinical contact hours under licensed psychologist supervision. Conducted structured intake interviews, administered and scored standardized assessments (PHQ-9, GAD-7, MMSE), and participated in treatment planning meetings for adult inpatients."

  - title: "Peer Counselor"
    organization: "GSU Counseling & Testing Center"
    type: "volunteering"
    duration: "Aug 2021 – May 2024"
    key_details: "Provided peer support and active listening to students experiencing academic stress, anxiety, and adjustment difficulties. Completed 40-hour training in QPR suicide prevention and motivational interviewing. Facilitated a weekly stress management support group (8-12 attendees)."

  - title: "Undergraduate Teaching Assistant"
    organization: "GSU — Introduction to Psychology (PSY 1101)"
    type: "teaching"
    duration: "Jan 2023 – May 2023"
    key_details: "Graded assignments and led two weekly review sessions for a 250-student section. Held office hours and provided one-on-one support to struggling students."

education:
  degree: "B.S. Psychology (Clinical Concentration)"
  institution: "Georgia State University"
  highlights:
    - "Merit Scholarship Recipient"
    - "Psi Chi International Honor Society"
    - "Relevant coursework: Abnormal Psych, Research Methods, Psychometrics, Developmental Psych, Cognitive Neuroscience"
    - "Thesis: 'Emotion Regulation Strategies and EEG Correlates in College Students'"

skills:
  technical:
    - "SPSS"
    - "EEGLAB / MATLAB"
    - "Qualtrics (survey design)"
    - "Thematic analysis"
    - "Psychometric assessment (PHQ-9, GAD-7, MMSE)"
    - "IRB protocol compliance"
    - "REDCap"
    - "Microsoft Office Suite"
  interpersonal:
    - "Active listening"
    - "Crisis de-escalation"
    - "Motivational interviewing"
    - "Group facilitation"
    - "Empathy"
    - "Cultural sensitivity"
  languages:
    - "English (native)"

target_job: "Clinical Research Coordinator"
target_industry: "Healthcare / Academic Research"
pivot_difficulty: "low"
```

---

### Persona 4: Ciarán O'Donovan

```yaml
archetype: "Humanities"
major: "Philosophy (Honors)"
tests: "Hardest pivot case — reframing abstract reasoning skills, 'irrelevant' retail work, non-obvious career paths, thesis-as-experience, debate team as leadership, freelance writing legitimacy"
graduation: "2024"
gpa: "3.74"
background_notes: "White, Irish-American from rural Vermont. First in his family to complete a four-year degree. Worked as a barista throughout college to pay rent. Uncertain about career direction but drawn to policy, compliance, or tech ethics roles."

experiences:
  - title: "Honors Thesis Author"
    organization: "University of Vermont, Dept. of Philosophy"
    type: "thesis"
    duration: "Sep 2023 – May 2024"
    key_details: "Wrote and defended a 75-page thesis titled 'Moral Agency in Autonomous Systems: A Kantian Framework for AI Governance.' Conducted a literature review spanning 60+ sources across philosophy, computer science, and law. Presented at the UVM Undergraduate Research Conference."

  - title: "Debate Team Captain"
    organization: "UVM Parliamentary Debate Society"
    type: "competition"
    duration: "Sep 2021 – May 2024"
    key_details: "Led a 12-member team to regional semifinals. Organized weekly practice sessions, recruited new members, and managed a $3,000 annual travel budget. Personally competed in 25+ tournaments and reached elimination rounds at 8."

  - title: "Freelance Blog Writer"
    organization: "Self-employed (various clients)"
    type: "freelance"
    duration: "Jun 2022 – Present"
    key_details: "Wrote 30+ articles on technology ethics, digital privacy, and responsible AI for 4 clients including a small tech policy newsletter (1,200 subscribers). Managed own editorial calendar, invoicing, and client communication."

  - title: "Shift Supervisor"
    organization: "Green Mountain Coffee Roasters Café, Burlington, VT"
    type: "work"
    duration: "Aug 2020 – May 2024"
    key_details: "Supervised 4-6 baristas per shift in a high-volume café. Managed cash handling and daily reconciliation ($2,000+ per shift). Trained 10+ new hires on POS systems, food safety protocols, and customer service standards. Promoted from barista to shift supervisor after 8 months."

education:
  degree: "B.A. Philosophy (Honors)"
  institution: "University of Vermont"
  highlights:
    - "Honors Thesis with Distinction"
    - "Phi Beta Kappa"
    - "Relevant coursework: Ethics, Logic, Philosophy of Mind, Political Philosophy, Philosophy of Law"
    - "Minor in Computer Science (Intro to CS, Data Structures, Algorithms)"

skills:
  technical:
    - "Argumentative writing"
    - "Policy analysis"
    - "Formal logic"
    - "Research synthesis"
    - "WordPress"
    - "Python (basic)"
    - "Google Workspace"
  interpersonal:
    - "Public speaking"
    - "Persuasion"
    - "Team leadership"
    - "Conflict resolution"
    - "Mentoring"
    - "Client communication"
  languages:
    - "English (native)"
    - "French (conversational)"

target_job: "Policy Analyst — Technology & AI"
target_industry: "Think Tank / Government / Tech Policy"
pivot_difficulty: "high"
```

---

### Persona 5: Priya Mehta

```yaml
archetype: "Business / Applied"
major: "Marketing"
tests: "Shallow depth across many tools, metrics without substance, portfolio-driven expectations, distinguishing tool proficiency from strategic thinking, startup internship framing"
graduation: "2024"
gpa: "3.35"
background_notes: "Indian-American woman from suburban New Jersey. Parents are both engineers; strong family pressure toward 'practical' careers. Active on social media personally and professionally. Confident communicator but sometimes oversells skills."

experiences:
  - title: "Social Media Marketing Intern"
    organization: "BrightLoop (Series A SaaS startup), New York, NY"
    type: "internship"
    duration: "Jun 2023 – Aug 2023"
    key_details: "Managed Instagram, Twitter/X, and LinkedIn accounts (combined 12K followers). Created 50+ posts using Canva and scheduled via Buffer. Grew Instagram engagement rate from 2.1% to 3.8% over 10 weeks. Assisted with two product launch campaigns."

  - title: "Ad Campaign Manager"
    organization: "Rutgers University Student Government Association"
    type: "project"
    duration: "Sep 2023 – Dec 2023"
    key_details: "Led a 3-person team to design and execute a campus-wide voter registration campaign. Created flyers, social media content, and a targeted email sequence. Campaign registered 430 students in 6 weeks, a 22% increase over the previous year."

  - title: "Marketing Club President"
    organization: "Rutgers American Marketing Association (AMA) Chapter"
    type: "volunteering"
    duration: "Sep 2022 – May 2024"
    key_details: "Grew chapter membership from 45 to 78 students. Organized 6 speaker events with industry professionals. Coordinated the chapter's entry in the AMA Collegiate Case Competition (team placed top 10 nationally)."

  - title: "Sales Associate"
    organization: "Nordstrom, Short Hills Mall, NJ"
    type: "work"
    duration: "May 2021 – May 2023"
    key_details: "Worked 15-20 hours/week in the women's contemporary department. Consistently exceeded monthly sales targets by 10-15%. Built repeat client relationships through personalized follow-ups."

education:
  degree: "B.S. Marketing"
  institution: "Rutgers University — New Brunswick"
  highlights:
    - "Dean's List (3 semesters)"
    - "AMA Collegiate Case Competition — Top 10 National"
    - "Relevant coursework: Consumer Behavior, Digital Marketing Analytics, Brand Management, Market Research"

skills:
  technical:
    - "Google Analytics (GA4 Certified)"
    - "Google Ads (Search Certified)"
    - "HubSpot (Inbound Marketing Certified)"
    - "Canva"
    - "Buffer / Hootsuite"
    - "Mailchimp"
    - "Basic HTML/CSS"
    - "Excel (pivot tables, VLOOKUP)"
    - "Tableau (beginner)"
  interpersonal:
    - "Persuasive communication"
    - "Client relationship management"
    - "Team leadership"
    - "Event planning"
    - "Cross-functional collaboration"
  languages:
    - "English (native)"
    - "Hindi (conversational)"
    - "Gujarati (conversational)"

target_job: "Digital Marketing Coordinator"
target_industry: "Tech / E-commerce"
pivot_difficulty: "low"
```

---

### Persona 6: Kofi Asante

```yaml
archetype: "Social Science Quantitative"
major: "Cultural Anthropology"
tests: "Fieldwork as professional experience, non-standard outcomes (ethnographic insight vs. metrics), cross-cultural competency, qualitative coding tools, volunteer tutoring legitimacy"
graduation: "2024"
gpa: "3.47"
background_notes: "Ghanaian international student who grew up in Accra before attending college in the U.S. on scholarship. Conducted ethnographic fieldwork in Ghana during a summer abroad program. Interested in international development and community-based research."

experiences:
  - title: "Ethnographic Field Researcher"
    organization: "University of Minnesota — Summer Field Program (Accra, Ghana)"
    type: "fieldwork"
    duration: "Jun 2023 – Aug 2023"
    key_details: "Conducted 8 weeks of ethnographic fieldwork examining market women's economic resilience strategies in Makola Market, Accra. Performed 22 semi-structured interviews in English and Twi, took detailed field notes, and coded transcripts using NVivo. Produced a 30-page field report and presented findings to faculty at the program symposium."

  - title: "Research Assistant — Migration Studies"
    organization: "UMN Dept. of Anthropology"
    type: "research"
    duration: "Sep 2022 – May 2024"
    key_details: "Supported a faculty-led study on West African diaspora communities in the Twin Cities. Transcribed and coded 40+ interview recordings, conducted literature reviews, and helped prepare an IRB renewal application. Contributed to a book chapter draft."

  - title: "GED Tutor"
    organization: "Minnesota Literacy Council (volunteer)"
    type: "volunteering"
    duration: "Sep 2021 – May 2023"
    key_details: "Tutored adult learners (primarily East African immigrants and refugees) preparing for the GED exam. Focused on math and social studies sections. Supported 15+ learners, 8 of whom passed the GED during the tutoring period."

  - title: "Resident Advisor"
    organization: "University of Minnesota Housing & Residential Life"
    type: "work"
    duration: "Aug 2022 – May 2024"
    key_details: "Managed a floor of 42 first-year residents in a culturally themed living-learning community. Organized monthly cultural exchange events (40+ attendees average). Mediated roommate conflicts and connected students to campus resources. Completed 30+ hours of training in crisis response and Title IX protocols."

education:
  degree: "B.A. Cultural Anthropology"
  institution: "University of Minnesota — Twin Cities"
  highlights:
    - "Study Abroad Fieldwork Grant Recipient"
    - "Anthropology Undergraduate Research Award"
    - "Relevant coursework: Ethnographic Methods, Political Economy, Medical Anthropology, Qualitative Research Design, GIS for Social Science"

skills:
  technical:
    - "NVivo (qualitative coding)"
    - "Semi-structured interviewing"
    - "Ethnographic field methods"
    - "ATLAS.ti"
    - "ArcGIS (basic)"
    - "Literature review methodology"
    - "IRB protocol preparation"
    - "Microsoft Office Suite"
  interpersonal:
    - "Cross-cultural communication"
    - "Active listening"
    - "Conflict mediation"
    - "Community building"
    - "Public speaking"
    - "Mentoring"
  languages:
    - "English (fluent)"
    - "Twi (native)"
    - "French (professional)"

target_job: "Research Associate — International Development"
target_industry: "International Development / NGO"
pivot_difficulty: "medium"
```

---

### Persona 7: Rosa Delgado-Peña

```yaml
archetype: "STEM Applied — Biology / Pre-Med"
major: "Biology"
tests: "Dual-path candidate (med school OR industry), certification and lab technique listing, shadowing as experience, strong GPA emphasis, volunteer EMT as clinical hours, pre-med vs. biotech resume divergence"
graduation: "2024"
gpa: "3.82"
background_notes: "Mexican-American woman from El Paso, TX. Bilingual household. Father is a paramedic; mother is a home health aide. Deciding between medical school applications and biotech industry jobs. Wants to keep both options open."

experiences:
  - title: "Undergraduate Research Assistant — Cancer Biology Lab"
    organization: "UT El Paso, Dept. of Biological Sciences"
    type: "research"
    duration: "Jan 2022 – May 2024"
    key_details: "Performed cell culture (HeLa, MCF-7 cell lines), PCR, gel electrophoresis, and Western blot assays under faculty supervision. Maintained lab notebooks per NIH standards. Contributed data to a manuscript on tumor suppressor gene expression (in preparation). Trained 2 incoming undergrad assistants on lab protocols."

  - title: "Volunteer EMT"
    organization: "El Paso Fire Department — Emergency Medical Services"
    type: "volunteering"
    duration: "May 2022 – Present"
    key_details: "Completed 300+ hours of volunteer emergency medical response. Provided pre-hospital patient assessment, wound care, and transport for medical and trauma emergencies. Maintained NREMT certification and completed continuing education requirements."

  - title: "Physician Shadowing"
    organization: "University Medical Center of El Paso — Internal Medicine"
    type: "practicum"
    duration: "Jun 2023 – Aug 2023"
    key_details: "Shadowed two attending physicians during inpatient rounds and outpatient clinic hours (80 hours total). Observed patient interviews, diagnostic reasoning, and multidisciplinary team meetings. Wrote reflective journal entries as part of a pre-med mentorship program."

  - title: "Biology Peer Mentor"
    organization: "UTEP STEM Success Center"
    type: "teaching"
    duration: "Sep 2022 – May 2024"
    key_details: "Mentored 10-12 first- and second-year biology students per semester through weekly study sessions. Focused on General Biology, Genetics, and Organic Chemistry. Students mentored had a 15% higher course pass rate than the departmental average."

education:
  degree: "B.S. Biology (Pre-Medical Concentration)"
  institution: "University of Texas at El Paso"
  highlights:
    - "Magna Cum Laude"
    - "Howard Hughes Medical Institute (HHMI) Undergraduate Research Scholar"
    - "Pre-Med Honor Society (Alpha Epsilon Delta)"
    - "Relevant coursework: Genetics, Cell Biology, Biochemistry, Organic Chemistry I-II, Human Anatomy & Physiology"

skills:
  technical:
    - "PCR / RT-qPCR"
    - "Cell culture (mammalian)"
    - "Western blot"
    - "Gel electrophoresis"
    - "Microscopy (fluorescence, confocal)"
    - "NREMT-B certified"
    - "BLS/CPR certified"
    - "GraphPad Prism"
    - "ImageJ"
    - "Microsoft Excel"
  interpersonal:
    - "Patient communication"
    - "Teaching and mentoring"
    - "Teamwork under pressure"
    - "Attention to detail"
    - "Empathy"
  languages:
    - "English (native)"
    - "Spanish (native)"

target_job: "Research Associate I — Cell Biology"
target_industry: "Biotechnology / Pharmaceutical"
pivot_difficulty: "medium"
```

---

### Persona 8: Thandiwe Nkosi

```yaml
archetype: "STEM Applied — Nursing / Health Sciences"
major: "Nursing (BSN)"
tests: "Clinical rotations as structured experience, licensure dependencies, shift-based work framing, patient education as skill, certification-heavy resume, practicum hours quantification"
graduation: "2024"
gpa: "3.55"
background_notes: "South African-born, naturalized U.S. citizen, raised in Minneapolis, MN. Zulu-speaking household. Mother is a certified nursing assistant. Thandiwe is the first in her family to earn a BSN. Passed NCLEX-RN in Jul 2024."

experiences:
  - title: "Clinical Rotation — ICU"
    organization: "Hennepin Healthcare, Minneapolis, MN"
    type: "practicum"
    duration: "Jan 2024 – Apr 2024"
    key_details: "Completed 180 clinical hours in a 20-bed medical ICU. Managed care for 1-2 critically ill patients per shift under preceptor supervision. Performed medication administration, ventilator monitoring, hemodynamic assessments, and collaborated with interdisciplinary teams during daily rounds."

  - title: "Clinical Rotation — Pediatrics"
    organization: "Children's Minnesota Hospital, Minneapolis, MN"
    type: "practicum"
    duration: "Sep 2023 – Dec 2023"
    key_details: "Completed 150 clinical hours in inpatient pediatrics. Provided age-appropriate patient education to families, administered pediatric medications, and performed developmental assessments. Developed a patient education handout on childhood asthma management adopted by the unit."

  - title: "Clinical Rotation — Community Health"
    organization: "Hennepin County Public Health Department"
    type: "practicum"
    duration: "May 2023 – Aug 2023"
    key_details: "Completed 120 clinical hours conducting home visits, community health assessments, and vaccination clinics in underserved neighborhoods. Screened 60+ individuals for hypertension and diabetes risk. Created culturally adapted health education materials in English and Somali."

  - title: "Certified Nursing Assistant (CNA)"
    organization: "Augustana Care, Minneapolis, MN"
    type: "work"
    duration: "Jun 2021 – Aug 2023"
    key_details: "Provided direct patient care for 8-12 residents per shift in a long-term care facility. Assisted with ADLs, vital signs, and mobility. Documented care in Epic EHR. Received 'Employee of the Quarter' recognition (Q1 2023)."

  - title: "Student Nurses Association — Community Outreach Chair"
    organization: "Minnesota State University — Mankato SNA Chapter"
    type: "volunteering"
    duration: "Sep 2022 – May 2024"
    key_details: "Organized 4 annual health screening events at community centers serving immigrant populations. Coordinated 20+ student nurse volunteers per event. Partnered with local clinics to provide blood pressure and glucose screenings to 200+ community members."

education:
  degree: "B.S. Nursing (BSN)"
  institution: "Minnesota State University — Mankato"
  highlights:
    - "NCLEX-RN Licensed (Jul 2024)"
    - "Dean's List (4 semesters)"
    - "Sigma Theta Tau International Honor Society of Nursing"
    - "Relevant coursework: Pharmacology, Pathophysiology, Health Assessment, Evidence-Based Practice, Community Health Nursing"

skills:
  technical:
    - "Patient assessment (head-to-toe)"
    - "Medication administration"
    - "IV therapy"
    - "Ventilator management"
    - "Hemodynamic monitoring"
    - "Epic EHR"
    - "BLS certified"
    - "ACLS certified"
    - "Wound care"
    - "Patient education"
  interpersonal:
    - "Therapeutic communication"
    - "Interdisciplinary collaboration"
    - "Cultural humility"
    - "Time management under pressure"
    - "Patient advocacy"
    - "Mentoring"
  languages:
    - "English (native)"
    - "Zulu (native)"
    - "Somali (basic)"

target_job: "Registered Nurse — Medical ICU"
target_industry: "Hospital / Healthcare System"
pivot_difficulty: "low"
```

---

### Persona 9: Leo Fujimoto

```yaml
archetype: "Creative / Design"
major: "Graphic Design (BFA)"
tests: "Portfolio-first field, non-traditional deliverables, freelance as legitimate experience, ATS challenges for visual fields, art direction as leadership, balancing creative identity with corporate resume norms"
graduation: "2024"
gpa: "3.40"
background_notes: "Japanese-American, non-binary (they/them), from Portland, OR. Self-taught in motion graphics before college. Strong online portfolio but limited traditional corporate experience. Concerned that resume format can't capture their visual work."

experiences:
  - title: "Art Director"
    organization: "The Vanguard (campus magazine), Portland State University"
    type: "editorial"
    duration: "Sep 2022 – Jun 2024"
    key_details: "Led the visual identity for a biannual student arts and culture magazine (print + digital). Directed a team of 6 designers and illustrators. Redesigned the magazine layout and brand system, increasing print distribution requests from campus orgs by 40%. Managed production timelines from concept through print-ready files."

  - title: "Freelance Graphic Designer"
    organization: "Self-employed (5+ clients)"
    type: "freelance"
    duration: "Jan 2022 – Present"
    key_details: "Designed brand identities, social media assets, and marketing collateral for local small businesses and nonprofits. Notable clients include a Portland food co-op (full rebrand), a music venue (event poster series), and a youth mentoring nonprofit (annual report design). Managed client relationships, revisions, and invoicing independently."

  - title: "Senior Exhibition — 'Signal / Noise'"
    organization: "Portland State University, School of Art + Design"
    type: "project"
    duration: "Jan 2024 – May 2024"
    key_details: "Conceived and produced a 12-piece multimedia exhibition exploring information overload in digital culture. Combined print design, motion graphics, and interactive web elements. Exhibited in PSU's Littman Gallery for 3 weeks. Wrote an artist statement and presented the conceptual framework to a faculty review panel."

  - title: "Design Intern"
    organization: "Instrument (design agency), Portland, OR"
    type: "internship"
    duration: "Jun 2023 – Sep 2023"
    key_details: "Supported senior designers on UI/UX projects for two Fortune 500 clients. Created wireframes and high-fidelity mockups in Figma. Contributed to a design system component library. Participated in client presentations and design critiques."

education:
  degree: "B.F.A. Graphic Design"
  institution: "Portland State University"
  highlights:
    - "Senior Exhibition — Littman Gallery"
    - "AIGA Student Portfolio Review — Selected Participant"
    - "Relevant coursework: Typography, Brand Identity, UI/UX Design, Motion Graphics, Design Thinking, Web Design"

skills:
  technical:
    - "Adobe Creative Suite (Photoshop, Illustrator, InDesign, After Effects, Premiere Pro)"
    - "Figma"
    - "Sketch"
    - "HTML/CSS"
    - "WordPress"
    - "Webflow"
    - "Cinema 4D (basic)"
    - "Print production (prepress, color management)"
  interpersonal:
    - "Art direction"
    - "Client communication"
    - "Creative team leadership"
    - "Visual storytelling"
    - "Constructive critique"
    - "Project management"
  languages:
    - "English (native)"
    - "Japanese (conversational)"

target_job: "Junior Visual Designer"
target_industry: "Design Agency / Tech"
pivot_difficulty: "medium"
```

---

### Persona 10: María Elena Ríos

```yaml
archetype: "Education / Service (wildcard)"
major: "Elementary Education"
tests: "Practicum-heavy profile, first-gen student framing, working with vulnerable populations, licensure requirements, IEP/special education experience, service-oriented language, after-school program coordination as leadership"
graduation: "2024"
gpa: "3.48"
background_notes: "Latina, first-generation college student from rural New Mexico. Grew up in a farming community where she helped translate for Spanish-speaking parents at school meetings. Deeply motivated by educational equity. Completed all student teaching requirements for NM teaching license."

experiences:
  - title: "Student Teacher (Full Semester)"
    organization: "Cesar Chavez Elementary School, Las Cruces, NM"
    type: "practicum"
    duration: "Jan 2024 – May 2024"
    key_details: "Served as lead teacher for a 3rd-grade bilingual classroom (24 students, 80% English Language Learners). Planned and delivered daily lessons across all core subjects aligned to NM Common Core standards. Managed classroom behavior using PBIS strategies. Administered and analyzed formative assessments to differentiate instruction. Participated in 6 IEP meetings for students with learning disabilities."

  - title: "After-School Program Coordinator"
    organization: "Boys & Girls Club of Las Cruces"
    type: "work"
    duration: "Sep 2022 – Dec 2023"
    key_details: "Coordinated academic enrichment and recreation programming for 35-50 K-5 students daily. Supervised 4 part-time staff and 6 volunteers. Designed a literacy intervention program that improved participating students' reading levels by an average of 1.2 grade levels over one academic year. Communicated with parents (primarily in Spanish) about student progress."

  - title: "Tutor — TRIO Upward Bound"
    organization: "New Mexico State University — TRIO Programs"
    type: "teaching"
    duration: "Sep 2021 – May 2023"
    key_details: "Tutored first-generation, low-income high school students in math and English Language Arts through the federal TRIO Upward Bound program. Supported 12-15 students per semester with homework help, test preparation, and college application guidance. 90% of tutored seniors were accepted to college."

  - title: "Community Interpreter (Volunteer)"
    organization: "La Clinica de Familia, Las Cruces, NM"
    type: "volunteering"
    duration: "Jun 2021 – Aug 2023"
    key_details: "Provided Spanish-English interpretation for monolingual Spanish-speaking patients at a community health center during medical appointments. Interpreted for approximately 5-8 patients per shift, ensuring accurate communication of diagnoses, medication instructions, and follow-up care. Completed medical interpreter ethics training."

education:
  degree: "B.A. Elementary Education (Bilingual Endorsement)"
  institution: "New Mexico State University"
  highlights:
    - "New Mexico Level 1 Teaching License (pending completion)"
    - "Bilingual Education Endorsement (Spanish)"
    - "TESOL Certificate"
    - "Relevant coursework: Foundations of Bilingual Education, Educational Psychology, Classroom Management, Assessment & Differentiation, Special Education Law"
    - "Kappa Delta Pi International Honor Society in Education"

skills:
  technical:
    - "Lesson planning (backwards design / UbD)"
    - "Formative and summative assessment"
    - "PBIS (Positive Behavioral Interventions and Supports)"
    - "IEP participation and documentation"
    - "Google Classroom"
    - "Seesaw"
    - "SMART Board"
    - "Sheltered Instruction Observation Protocol (SIOP)"
    - "Microsoft Office Suite"
  interpersonal:
    - "Classroom management"
    - "Parent communication"
    - "Cultural responsiveness"
    - "Patience"
    - "Advocacy for students with disabilities"
    - "Team collaboration"
    - "Conflict resolution"
  languages:
    - "Spanish (native)"
    - "English (native)"

target_job: "Bilingual Elementary Teacher (3rd-5th Grade)"
target_industry: "K-12 Public Education"
pivot_difficulty: "low"
```

---

## Appendix: Prompt Weakness Checklist

Use this checklist when reviewing pipeline outputs for each persona:

- [ ] **Experience type coverage** — Did the prompt handle non-standard types (fieldwork, practicum, editorial, thesis)?
- [ ] **Outcome elicitation** — Did the prompt coach qualitative outcomes as effectively as quantitative ones?
- [ ] **Skill extraction** — Were domain-specific skills (lab techniques, clinical tools, design software) captured with appropriate granularity?
- [ ] **Career pivot** — Did the resume builder detect when a pivot was needed and suggest bridge narratives?
- [ ] **ATS optimization** — Did the resume use standard headings and avoid formatting that breaks ATS parsing?
- [ ] **EIC coaching tone** — Did the prompt avoid jargon and gently explore undervalued experiences?
- [ ] **Bullet formula selection** — Did the resume builder choose XYZ/CAR/Narrative appropriately per experience type?
- [ ] **Certification handling** — Were licensures and certifications surfaced correctly for regulated fields?
- [ ] **Portfolio integration** — For creative/design personas, did the resume reference portfolio work effectively within ATS constraints?
- [ ] **Dual-path tailoring** — For personas with multiple career directions, did the resume correctly tailor to the specified target?
