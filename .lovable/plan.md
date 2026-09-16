# Rebuild "Orbis" AI research workspace here

The GitHub project is an AI academic research workspace called Orbis, built on the same
technology as this project. So it can be brought over almost file-for-file rather than
rewritten.

## What the app does

- **Chat workspace (home page)** — an AI assistant for academic questions, with a collapsible
  sidebar, chat history, engine picker (Flash, Pro, Expert, Deep Research, Journal Focus),
  light/dark mode and accent-colour theming.
- **Search page** — literature search across OpenAlex, Crossref, Semantic Scholar, PubMed and
  DOAJ; results can be saved to a personal library.
- **Write page** — a manuscript editor with AI writing presets (draft, literature review,
  systematic review, reviewer critique, report), inline actions (rephrase, summarize, polish,
  fix grammar), maths rendering, citation handling, and export to Word/PDF.
- Saved papers and drafts live in the browser (no accounts or database in the original).

## What I'll do

1. Copy over the three pages, shared layout, and all supporting logic: search sources, the
   library, citation/export helpers, maths rendering, theming and engine settings.
2. Copy the visual design (fonts Manrope + Newsreader, colour scheme, dark mode) and the extra
   interface building blocks the pages use.
3. Add the missing packages the original relies on: Word/PDF export, maths rendering, the AI
   streaming toolkit, and a few interface libraries.
4. Wire the AI assistant to Lovable AI, exactly as the original does, and keep each page's own
   title and social preview text.
5. Check the app builds and open each page to confirm chat, search and writing all work.

## Technical notes

- Both projects are TanStack Start + Tailwind v4 + shadcn/ui, so this is a port, not a rewrite:
  `src/routes/{index,search,write}.tsx`, `src/routes/api/assist.ts`, `src/routes/__root.tsx`,
  `src/styles.css`, and `src/lib/{engine,theme,library,latex,exporters,assist-client,ai-gateway.server,search.functions}.ts`.
- New dependencies: `ai`, `@ai-sdk/openai-compatible`, `docx`, `jspdf`, `katex`, plus the
  Radix/shadcn packages the copied components import.
- The assist endpoint streams from `ai.gateway.lovable.dev` using `LOVABLE_API_KEY` from the
  server environment; no user-supplied keys needed.
- Literature search runs server-side against public APIs (OpenAlex, Crossref, Semantic Scholar,
  PubMed E-utilities, DOAJ) — no keys required.
- No database or login is involved; storage stays in the browser. Say the word if you'd like
  accounts and cloud-saved libraries added on top.
