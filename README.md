### `zsk-chat-summarize` — README

#### What it does

Turns any conversation into a compact, copy-pasteable **resume prompt** you can paste into a new chat to continue exactly where you left off — no re-explaining, no lost context.

***

#### Installation

1. Download `zsk-chat-summarize.skill`
2. In Claude.ai: **Settings → Skills → Install skill** → drop the file in

***

#### Usage

Type any of these at any point in a conversation:

| Trigger          | Example                                            |
| :--------------- | :------------------------------------------------- |
| Slash command    | `/zsk-chat-summarize`                              |
| Natural language | `"This chat is getting long, summarize it"`        |
| Planning ahead   | `"I want to continue this tomorrow in a new chat"` |
| Wrapping up      | `"Give me a resume prompt"`                        |

***

#### Output structure

You get one fenced code block with these sections (empty ones are omitted):

```
## Context Resume — [Topic]

### Who I am
### What we were doing
### What we decided / established
### Current state / progress
### Active files / artefacts
### Open questions / TODO
### Important constraints
### Exact continuation request   ← always present, always actionable
```

Below the block: a note about any **files you'll need to re-attach** (uploaded files don't transfer between chats).

***

#### How to continue in a new chat

1. Copy the entire code block
2. Open a new Claude chat
3. Paste it as your **first message**
4. Claude picks up from the "Exact continuation request" — no extra setup needed

***

#### Tips

* **Use it early** — you don't have to wait until the chat is maxed out. Mid-session snapshots work great too.
* **Re-attach files** — if you uploaded PDFs, images, or code files, the skill will remind you to bring them along.
* **Stack with other skills** — if you're mid-resume-edit using `zsk-jd`, the resume prompt will preserve your LaTeX state, flags used, and where the draft stood.

