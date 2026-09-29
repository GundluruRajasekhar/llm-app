# Tasks

## Phase 1: Core platform
- [x] Auth screens, dashboard, projects, tasks, search and filters (prototype in `index.html`)
- [ ] Move data to an API and database; add hashed passwords and real sessions
- [ ] Add roles and per-user data checks

## Phase 2: RAG
- [x] Build chunks from projects, tasks and activity; keyword retrieval with scores
- [ ] Replace with embeddings and a vector store; re-index on every change
- [ ] Test: 20 questions with known answers; check the right chunk ranks in the top 3

## Phase 3: LLM
- [ ] Add a server endpoint that calls the model; keep the key on the server
- [ ] Prompt for JSON: `intent`, `steps[]` with `tool` and `args`
- [ ] Validate JSON against the tool list; reject unknown tools or bad arguments
- [ ] Fall back to "I could not do that" when validation fails

## Phase 4: Agent
- [x] Tools: create project/task, update, delete with approval, overdue, summarize
- [ ] Cap tool calls per request; log every call with user and time
- [ ] Add undo for the last agent change

## Phase 5: Testing
- [ ] Create, update, and delete by chat; confirm data and dashboard update
- [ ] Ask about a task that does not exist; expect a clear "not found"
- [ ] Decline a delete; confirm nothing changed
- [ ] Try prompts that ask the agent to ignore the rules; confirm it stays inside the tools
- [ ] Check with two accounts that data never mixes

## Phase 6: Demo video and GitHub
- [ ] Record with audio: register, dashboard, create project and task, filters, then the AI panel
- [ ] Show the "How the agent got there" trace on one create and one delete with approval
- [ ] Say plainly what is demo-mode and what production would change
- [ ] Push files and README to GitHub; add the video link
