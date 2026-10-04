# CLAUDE.md — interview-refresher

My interview refresher pages, served by GitHub Pages at
https://prompath.github.io/interview-refresher/. This repository is public.

- The CV these pages refer to is in `~/Projects/jeerawat-cv` (private). Its
  `INTERVIEW_PREP_TOPICS.md` maps each topic to a CV line; its `CLAUDE.md` has the writing
  rules. When the CV changes, update the "On my CV" section of the matching pages here.
- Every topic page keeps the same parts: In one minute, Key ideas, On my CV, Likely
  questions, Pitfalls, Sources. A new page also needs a row in `index.md`.
- Formulas go in code blocks; the site does not render maths.
- Nothing about my employers beyond what the CV itself says: no vendor or consultant
  names, no absolute numbers (customer counts, conversions, revenue), no internal table,
  job or repository names. Uplift percentages are fine. My own interview stories stay as
  prompts in `i-stories/`; never write the answers here.
- Pushing to `main` republishes the site. Commit messages: one short imperative sentence.
- The remote uses SSH. If a push is denied, set `SSH_AUTH_SOCK` to the agent socket under
  `~/.ssh/agent/`.
