You are a senior full-stack engineer. Build a production-ready web application that replicates core Anki-style flashcards and includes an exam-question practice + AI marking area (similar in concept to “MarkMyAI”), with a future marketplace in mind.

TECH REQUIREMENTS
- Deliver as a complete, runnable, functional website (no pseudo-code).
- Use a modern stack that runs locally immediately:
  - Frontend: Next.js (App Router) + TypeScript + Tailwind CSS
  - Backend: Next.js API routes (or a small Express server if needed)
  - Database: SQLite (via Prisma ORM) for easy local setup
- Include a .env.example and clear setup steps in a README.
- Use clean architecture: separate modules for auth, flashcards, importing, exam questions, AI marking, and admin utilities.
- Provide basic seed data for demo use.

CORE FEATURES (MVP)
1) Authentication + Accounts
- Email/password authentication (secure hashing, sessions/JWT).
- Users can create/edit/delete their content.
- Admin-ready structure (roles field in DB).

2) Flashcards (Anki-like)
- Create decks.
- Create flashcards (Front, Back, optional tags).
- Study mode:
  - Show front → reveal back
  - User selects: Again / Hard / Good / Easy
  - Implement a simplified spaced repetition algorithm (SM-2 style acceptable).
  - Track next review date, interval, ease factor, and review history.
- Deck view: due cards count, total cards, progress.

3) CSV Import / Export
- Import flashcards from CSV via upload in the UI.
- CSV format support:
  - Required columns: deck_name, front, back
  - Optional: tags (comma-separated)
- Validate rows and show a clean import summary (success count, failed rows with reasons).
- Export decks to CSV.

4) Exam Questions Section
- A section where users can:
  - Create question sets (subject, topic, exam board optional fields).
  - Paste multiple exam questions into a text area (bulk add).
  - Each question supports: question text, marks available, optional mark scheme text, optional keywords/rubric.
- User answering UI:
  - Show a question
  - Provide an answer text area
  - Save attempts with timestamps and scores

5) AI Marking (Mark Scheme Matching Concept)
- Implement an AI-powered marker endpoint:
  - Input: question text, student answer, mark scheme text (if provided), marks available.
  - Output: score (0..marks), justification, and improvement points.
- Must be safe and transparent:
  - Show a disclaimer: “AI marking is guidance; not official.”
  - If mark scheme text is missing, grade using a rubric and give a confidence rating.
- Include an abstraction layer so the “AI provider” can be swapped later.
- Provide a “mock AI” fallback mode that works without any paid API key (rule-based keyword matching + partial credit).
- If OPENAI_API_KEY is present, use OpenAI via server-side call; if not present, automatically use the fallback marker.

FUTURE-PROOFING (Marketplace-ready, but do not fully build it yet)
- Build data structures and routes in a way that can support:
  - Public decks (publish/unpublish)
  - Deck metadata: title, description, subject, exam board, tags, difficulty, author
  - Ratings/download count fields (can be stubbed)
- Add a “Marketplace” page placeholder that currently shows: “Coming soon”
  - But make sure the DB schema supports publishing.

UI/UX REQUIREMENTS
- Clean, modern layout.
- Pages:
  - Landing
  - Dashboard
  - Decks list + create/edit
  - Study mode
  - Import/export page
  - Exam questions page
  - AI marking page (integrated with exam questions)
  - Settings
  - Marketplace placeholder
- Provide good empty states and error messages.
- All forms must have validation.

SECURITY + QUALITY
- Server-side validation for every write.
- Sanitize text inputs.
- No secrets exposed to the client.
- Rate-limit AI marking endpoint.
- Use ESLint/TypeScript strict settings.
- Add basic tests for:
  - CSV import parser
  - spaced repetition scheduling function
  - AI fallback marker scoring

DELIVERABLES
- Full source code with folder structure.
- Prisma schema + migrations.
- README with setup + run commands.
- Example CSV file to test import.
- Seed script that creates:
  - 1 demo user
  - 2 demo decks
  - ~20 demo flashcards
  - 1 demo exam question set + 5 questions + sample mark schemes

IMPORTANT BEHAVIOR
- Do not leave TODOs for core features. Everything above must be fully working.
- If any feature has tradeoffs, implement the simplest reliable version and explain briefly in README.
- The final output must be directly runnable after installing dependencies and running migrations.
