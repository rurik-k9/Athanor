# Athanor V1 - Roadmap & Bounded Tasks

## 0. Project Context (Read First)
This project is a digital crucible for inner transformation (The Spark). Before coding, you MUST read `prompts/athanor_system.txt` to understand the philosophical and ethical boundaries. 
The bot must act as a "mirror" (not a guru), respect the absolute Hierarchy of Priorities (Safety > Autonomy > Truth > Philosophy), and avoid "forced transformation" or moralizing.

## Task 1: The Vessel (Authentication & Infrastructure)
- [ ] Create a `requirements.txt` file at the root (`atproto`, `python-dotenv`, `openai` or `requests`, `sqlite3`).
- [ ] Create a `src/` directory and a `src/main.py` file.
- [ ] Create a `.gitignore` file to exclude `.env`, sensitive configurations, and logs containing private data.
- [ ] Create a `.env.example` file with variable names only (no secrets).
- [ ] Write a connection script using `atproto`. The bot must authenticate using its handle and App Password (loaded from environment variables). Implement error handling and session renewal.

## Task 2: The Ear (Listener & Safety Vigilance)
- [ ] In `src/main.py`, create a loop or cron job to check notifications via AT Protocol.
- [ ] Filter notifications to capture only "mention" or "reply" events and extract the text, sender, and post URI.
- [ ] **SAFETY VIGILANCE (NOT DIAGNOSIS):** Implement a multi-lingual lexical filter (English, French, Spanish, etc.) to flag potential crisis messages. 
- [ ] The filter is a vigilance trigger, not a diagnostic tool. False positives (quotes, third-party mentions, historical discussions) must be expected and tested.
- [ ] If a crisis is flagged: bypass the LLM entirely. Send a pre-written, compassionate message. Provide emergency resources appropriate to the user's country **only when the location is known or safely inferable**. If unknown, provide general guidance and ask for the country. **Never invent local emergency numbers.**

## Task 3: The Brain (LLM Integration & Prompt Defense)
- [ ] Create a function to read the system prompt from `prompts/athanor_system.txt`.
- [ ] Send the prompt + user message + **minimal conversation context** to the LLM API. Define what context is sent (e.g., last 3 messages) and do not store or transmit more than necessary. Implement a data retention policy.
- [ ] **CONSTRAINT:** Ensure the LLM respects the "Conversational Method" and the "Hierarchy of Priorities" from the prompt.
- [ ] **SECURITY:** Protect against prompt injection. User messages must NEVER override the system prompt (e.g., if a user says "ignore previous instructions", the system prompt must prevail).
- [ ] Handle API errors, empty responses, timeouts, and rate limits gracefully.

## Task 4: The Mouth (Posting the Reply & Idempotency)
- [ ] Format the LLM's response as a reply.
- [ ] Use the `atproto` client to publish.
- [ ] **CRITICAL FOR DELVETOWN:** The post must use the exact lexicon `town.delve.feed.post`. Ask `beijing` for the exact JSON schema, required fields, and a working example. Do not invent the structure.
- [ ] **IDEMPOTENCY:** Implement persistent notification tracking (SQLite for V1) to prevent duplicate replies, including after crashes or restarts. The bot must never publish two responses to the same message.

## Task 5: The Forge (Deployment & Operations)
- [ ] Create a `Dockerfile` or `render.yaml`.
- [ ] Ensure all secrets are read from environment variables.
- [ ] Write a `README.md` explaining deployment (Render/Fly.io).
- [ ] Implement error logging (excluding sensitive data), rate limiting (prevent spam), and loop prevention (the bot must not reply to itself or enter recursive reply loops).
- [ ] Implement a mechanism to resume operation correctly after unexpected restarts.

## Task 6: The Trial (Testing, Validation & Reliability)
- [ ] Test authentication, notification retrieval, and reply publishing independently before integration.
- [ ] Test the bot with ordinary questions, technical requests, philosophical discussions, and personal reflections. Verify it responds directly to facts (no forced Socratic questioning) and never imposes alchemical interpretation.
- [ ] Test safety detection using explicit, indirect, quoted, multilingual, and ambiguous crisis messages. Verify false positives/negatives are handled.
- [ ] Verify the bot does not respond twice to the same notification and cannot enter reply loops or respond to its own posts.
- [ ] Test prompt injection attempts (user messages cannot override the system prompt).
- [ ] Verify that the bot does not expose API keys, credentials, or private conversation data in logs.
- [ ] Verify the system continues operating correctly after temporary API failures, timeouts, and unexpected restarts.
- [ ] Validate the Delvetown lexicon against actual working examples before deployment.
- [ ] **Acceptance Criterion:** Athanor V1 is ready ONLY when core functions, safety mechanisms, and ethical constraints are tested successfully.
