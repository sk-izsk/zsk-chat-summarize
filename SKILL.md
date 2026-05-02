---
name: zsk-chat-summarize
description: Summarizes the current conversation into a compact, copy-pasteable resume prompt so the user can start a fresh chat and continue exactly where they left off. Trigger on /zsk-chat-summarize, "summarize this chat", "give me a resume prompt", "start a new chat", or "chat is getting long".
---

# zsk-chat-summarize

Produce a **dense, self-contained resume prompt** the user can paste into a brand-new chat to pick up exactly where they left off — zero re-explanation needed.

---

## Output Format

Emit a single fenced code block (` ```text `) containing the full resume prompt.
Below the code block, add a short plain-English note listing anything you could NOT capture (e.g. uploaded files the user will need to re-attach).

### Resume Prompt Structure (inside the code block)

```
## Context Resume — [Topic / Project Name]
*Generated [today's date]. Paste this at the start of a new chat.*

### Who I am
<1–2 sentences about the user if their role/background was established in the chat. Omit if nothing relevant was shared.>

### What we were doing
<1–3 sentences: the main goal or task being worked on.>

### What we decided / established
<Bullet list of key decisions, chosen approaches, constraints, or facts that must carry over. Include specific values, names, paths, configs, or code snippets only if they materially affect future work. Skip trivia.>

### Current state / progress
<Where exactly things stand. What's done. What's in-progress. What's next.>

### Active files / artefacts
<List file names, artifact titles, or URLs that were created or modified. Note if the user needs to re-upload any files.>

### Open questions / TODO
<Unresolved items, pending decisions, or explicit next steps the user mentioned.>

### Important constraints
<Tone preferences, formatting rules, tech stack requirements, things Claude must NOT do, or any standing instructions the user gave during this chat.>

### Exact continuation request
<One clear, imperative sentence telling the new Claude exactly what to do first. E.g.: "Continue drafting Section 3 of the cover letter using the tone guidelines above.">
```

---

## Rules

1. **Be dense, not exhaustive.** Omit pleasantries, failed attempts, and tangents. Keep only what affects future work.
2. **Preserve specifics.** Exact model names, variable names, file paths, numeric values, chosen phrasings — if they matter, include them verbatim.
3. **Code snippets.** If a code block was the last working version of something important, include it inline (collapsed to the essential parts if long).
4. **Omit sections that are empty.** Don't include section headers with nothing under them.
5. **Never summarize into prose paragraphs** when a bullet or snippet is clearer.
6. **Flag re-attachments.** If the conversation involved uploaded files (PDFs, images, etc.), explicitly tell the user after the code block that they'll need to re-attach them.
7. **Length.** The resume prompt should be as short as possible while being complete. Typical length: 150–400 words inside the block. Very long technical sessions may go higher.
8. **The "Exact continuation request" is mandatory.** It must be actionable and specific — not "continue helping me" but a real first instruction.

---

## Example Triggers

- `/zsk-chat-summarize`
- "This chat is getting long, summarize it for me"
- "Give me a prompt I can paste into a new chat"
- "I want to continue this tomorrow in a fresh chat"
- "Wrap up this session for me"

---

## After Emitting the Resume Prompt

Say exactly one sentence: what the user should do next (e.g. "Copy the block above, open a new chat, and paste it as your first message — you're good to go.").
Do not add padding, encouragement, or offers to help further.