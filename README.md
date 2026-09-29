# TaskMind: an AI project and task manager (RAG + LLM + agent)

Every request to the AI panel follows one path:

```
User message
  1. LLM  understands the request (intent + details)
  2. RAG  retrieves the most relevant projects, tasks and activity
  3. LLM  plans the tool calls, grounded in what was retrieved
  4. Agent runs the tools (create, update, delete, list, summarize)
  5. LLM  writes the answer from tool results and retrieved chunks
```

Deletes never run on their own: the agent shows an **Approve** button first.

## Run it
Open `index.html` in a browser. Register any email and password (4+ characters); sample projects and tasks are created for you. No install, no server.

## Try these in the AI agent tab
- `add task Fix checkout bug in Website high priority assign to Sam due tomorrow`
- `What is overdue?`
- `Summarize project Website`
- `Mark login bug as done`
- `Delete task login bug` (then approve)
- `Who is working on design?`

Open "How the agent got there" under each reply to see the 5 steps and the retrieved chunks with scores.

## What is real and what is a stand-in
| Part | In this demo | For production |
|---|---|---|
| Dashboard, projects, tasks, search, filters | Working, saved in browser localStorage | REST API + database (PostgreSQL) |
| Auth | Demo only, password stored as typed | Hashed passwords, JWT or session cookies, protected routes |
| RAG | Real keyword retrieval (TF-IDF style) over your data | Embeddings + vector store (pgvector), re-index on every change |
| LLM | Rule-based stand-in in `llmUnderstand`, `llmPlan`, `llmAnswer` | Call a hosted model from your **server**, never from the browser with a key |
| Agent tools | Real, act on local data | Same tool names, run server-side with per-user permissions |

## Swapping in a real LLM
Replace the three `llm*` functions with calls to your backend, for example `POST /api/agent` with `{message, retrievedChunks}`. Ask the model for JSON (`intent`, `steps[]` with `tool` and `args`), validate that JSON against the tool list, then run the tools. Keep the approval step for anything destructive.

## Files
- `index.html` - the app
- `requirements.md` - what it must do and how it is built
- `tasks.md` - build order, tests, demo checklist
