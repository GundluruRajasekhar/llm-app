# Requirements

## 1. Core platform (internship Task 4)
- F1 Register, log in, log out; dashboard and other pages need a signed-in user.
- F2 Dashboard: project overview, task counts (total, to do, in progress, done, overdue), progress per project, recent activity.
- F3 Projects: create, list, view details, delete (deleting removes its tasks, with confirmation).
- F4 Tasks: create, assign, set status, priority and due date, delete; search by text; filter by status and priority.
- F5 At least one AI feature: the agent panel below.

## 2. AI design rule
**Every AI task goes through the LLM, is grounded by RAG, and is executed by the agent.** No feature may skip a step.
- A1 LLM understands the message and returns an intent with arguments.
- A2 RAG retrieves top-k chunks (projects, tasks, recent activity) for that message.
- A3 LLM plans tool calls using the retrieved context; it may only use listed tools.
- A4 Agent runs the tools and reports what changed.
- A5 LLM writes the reply from tool results and cites retrieved chunks.
- A6 Destructive tools (delete) require explicit user approval.
- A7 Every agent action is written to the activity log.
- A8 If retrieval finds nothing, the agent says so instead of guessing.
- A9 The reply exposes a trace: intent, chunks with scores, plan, tool result.

## 3. Agent tools
`create_project`, `create_task`, `update_task`, `delete_task` (approval), `list_overdue`, `summarize`, `answer` (question answering only).

## 4. Data model
- User: id, name, email, password hash
- Project: id, owner, name, description
- Task: id, project, title, description, status, priority, assignee, due date
- Activity: timestamp, text
- Chunk (derived): type, ref id, text, embedding, updated time

## 5. Production architecture
Frontend (this page) → REST API → database → retrieval service (embeddings + vector search) → LLM service → tool executor. Re-index chunks whenever a project or task changes.

## 6. Non-functional
- Users only retrieve and change their own data; enforce this in the API, not only in the UI.
- Never expose LLM keys to the browser; validate model output before running tools.
- Keep it usable on phones and by keyboard.
- Log failures and model outputs for review; cap tool calls per request.

## 7. Known limits of the demo
Rule-based LLM stand-in, keyword retrieval, local storage, plaintext demo passwords, single user per browser profile.
