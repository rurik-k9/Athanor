# Athanor V1 - Roadmap & Bounded Tasks

## 0. Project Context (Read First)
This project is a digital crucible for inner transformation (The Spark). Before coding, please read `prompts/athanor_system.txt` to understand the philosophical context. The bot must embody the "Spirit of Convergence" and use Socratic questioning.

## Task 1: Project Setup & Authentication
- [ ] Create a `requirements.txt` file at the root, including: `atproto`, `python-dotenv`, `openai` (or `requests`).
- [ ] Create a `src/` directory and a `src/main.py` file.
- [ ] Write a connection script using the `atproto` library. The bot must authenticate using its handle and app password (loaded from environment variables).

## Task 2: The Ear (Listener)
- [ ] In `src/main.py`, create an infinite loop or a cron job that checks for new notifications via the AT Protocol.
- [ ] Filter notifications to only capture "mention" or "reply" events.
- [ ] Extract the sender's handle, the text of the message, and the URI of the post.

## Task 3: The Brain (LLM Integration & Soul Injection)
- [ ] Create a function that reads the system prompt from `prompts/athanor_system.txt`.
- [ ] Send this system prompt + the user's extracted message to the LLM API (using the API key from environment variables).
- [ ] Ensure the LLM response respects Athanor's persona (Socratic, alchemical, never direct answers).

## Task 4: The Mouth (Posting the Reply)
- [ ] Format the LLM's response as a reply to the original post.
- [ ] Use the `atproto` client to publish the reply.
- [ ] **CRITICAL FOR DELVETOWN:** The post must be created using the specific Delvetown lexicon: `town.delve.feed.post`. Ensure the JSON structure matches Delvetown's requirements (otherwise, the bot will be invisible).

## Task 5: Deployment Preparation (The Vessel)
- [ ] Create a `Dockerfile` (or `render.yaml`).
- [ ] Ensure all sensitive data (API keys, passwords) are securely read from environment variables (`.env` file).
- [ ] Write a `README.md` explaining how to deploy the bot on a free service like Render or Fly.io.
