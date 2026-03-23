# Memory Integration Guide

> How to leverage chat memory features across different AI platforms so your
> experience data persists between sessions.

---

## The hybrid approach

This project uses a **hybrid persistence model**:

| Layer | What | Where |
|-------|-------|-------|
| **Portable file** | Complete Experience Profile (YAML) | Saved locally, uploaded when needed |
| **Chat memory** | Key facts, preferences, and context | Stored in the AI platform's memory system |

The portable file is the **source of truth**. Chat memory is a convenience layer
that makes follow-up sessions smoother.

---

## Platform-specific guidance

### GitHub Copilot

**Memories:** Copilot can store memories that persist across conversations.

After completing an experience capture session, ask:
```
Please save the following to your memory:
- My name is [name]
- I'm an early-in-career [field] professional based in [location]
- My experience profile is saved as "my-experience-profile.yaml"
- My current focus is [job-seeking / grad school / career transition]
- Key skills: [top 3-5 skills]
```

**For follow-up sessions**, Copilot will recall this context automatically.
You still upload the YAML file for detailed work, but Copilot will already
know who you are and what you're working toward.

### Claude

**Projects:** Use Claude Projects to create a persistent workspace.

1. Create a Project named "Career Documents" (or similar)
2. Upload your `experience-profile.yaml` to the Project's knowledge base
3. Add Project instructions:
   ```
   This project helps me build and refine career documents (resumes, CVs,
   cover letters). My experience profile is uploaded as a knowledge file.
   Always reference it when generating documents. I am early-in-career.
   ```
4. All conversations within this Project will have access to your profile

**Memories (if available):** Same approach as Copilot — save key facts
after your first session.

### ChatGPT

**Memory:** ChatGPT automatically saves facts from conversations.

After your experience capture session, explicitly ask:
```
Please remember:
- My name is [name] and I'm based in [location]
- I'm early-in-career in [field]
- I have an experience profile YAML file that I'll upload for resume work
- My top skills are: [list]
- I'm currently targeting [type of roles/programs]
```

**Custom GPTs (optional):** For heavy users, you can create a Custom GPT
with your profile pre-loaded as a knowledge file and the resume-builder
prompt as instructions.

**File uploads:** Upload your YAML file at the start of each resume session.

---

## What to save to memory vs. what stays in the file

### Save to memory (key facts that avoid repetition)
- Your name, location, and field
- Current career goal (job-seeking, grad school, etc.)
- Target roles or industries
- Preferred resume style or format
- Any constraints (visa status, relocation preferences, etc.)

### Keep in the file only (too detailed for memory)
- Full experience descriptions
- Specific outcomes and metrics
- Complete skills inventory
- Education details

---

## Updating your profile

The easiest way to add new experiences is the
[Experience Update prompt](../prompts/experience-update.md) — it takes
5-10 minutes and produces a ready-to-paste YAML snippet.

If you prefer to edit the file manually:

1. Open your `experience-profile.yaml`
2. Add the new experience at the top of the `experiences` list
3. Update `skills_inventory` if you gained new skills
4. Update your `summary` if your professional identity has shifted
5. Re-upload the file in your next chat session

**Tip:** After a major update, ask the assistant:
```
I've updated my experience profile. Please review the new entries and suggest
any improvements to how I've described my actions, outcomes, or keywords.
```

---

## Cross-platform portability

The YAML file works identically across all platforms. If you switch from
ChatGPT to Copilot, or use multiple platforms:

1. Your YAML file goes with you — just upload it
2. Re-save key facts to the new platform's memory
3. The prompts are platform-agnostic — they work everywhere

This is why the file is the source of truth, not any single platform's memory.
