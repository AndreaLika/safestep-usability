# SafeStep — Usability Evaluation Questionnaire

A standalone bilingual (Greek / English) usability questionnaire for the **SafeStep** Industrial Safety Training Platform.

Built for the **5CM519 Team Project — Coursework 2** at Mediterranean College / University of Derby.

## What's inside

The questionnaire is a single self-contained `index.html` (no build step, no dependencies) and follows the structure recommended by the SafeStep team's evaluation protocol:

- **Part A — System Usability Scale (SUS)** — the 10 standard items from Brooke (1996). The page automatically computes the 0–100 SUS score after submission.
- **Part B — SafeStep-specific items** — 8 Likert-style items covering content quality, simulations, quizzes, certificates, bilingual switching, theme switching, role-based filtering, and the admin dashboard.
- **Part C — Open-ended questions** — 3 qualitative prompts on what worked well, what was hard, and what should be added next.

Additional features:

- Bilingual UI (Greek / English), matched to the SafeStep platform's bilingual layer
- Light / dark theme toggle, matched to SafeStep's design tokens
- Automatic SUS scoring with adjective band (per Bangor, Kortum & Miller, 2009)
- Copy-to-clipboard and download-as-`.txt` for the response summary
- LocalStorage persistence so a partially filled response is not lost on accidental refresh
- Mobile-responsive layout (5-column Likert collapses gracefully on phones)
- No external services, no tracking, no analytics

## How to deploy on GitHub Pages

1. Create a new public GitHub repository (for example `safestep-usability`).
2. Push the contents of this folder (just `index.html` and this `README.md`) to the `main` branch.
3. In the repository's **Settings → Pages**, set the source to `main` branch, `/ (root)`.
4. GitHub will publish the site at `https://<your-username>.github.io/<repo-name>/` within a minute or two.
5. Share the published URL with participants.

## Enable automatic email collection (recommended, ~1 minute setup)

Out of the box, the questionnaire works **locally only** — when a participant submits, they see their SUS score and a summary they can copy or download, and they need to send that to the team manually. This is fine for a small recruited study, but you can also turn on **automatic email submission** so every response lands in your inbox.

The page uses [Web3Forms](https://web3forms.com) — a free, GitHub-Pages-friendly service that just needs an access key (no account required to start; the key is generated from your email).

**Setup:**

1. Go to [web3forms.com](https://web3forms.com) and enter the email address you want responses sent to.
2. You will receive an **access key** (a UUID-like string).
3. In `index.html`, find this line near the top of the `<script>` block:
   ```js
   const WEB3FORMS_ACCESS_KEY = "YOUR_ACCESS_KEY_HERE";
   ```
   Replace `YOUR_ACCESS_KEY_HERE` with your actual key (keep the quotes).
4. Commit and push.

That's it. Every submission will now arrive in your inbox with:

- The participant's SUS score and band
- Each of the 10 SUS items as separate fields
- Each of the 8 SafeStep-specific items as separate fields
- All 3 open-ended answers in full
- The demographic fields
- A complete plain-text summary as the email body (easy to paste into a spreadsheet)

If the access key is left as the placeholder, the page continues to work in **local-only mode** — participants see the on-screen summary and can copy/download it. A small notice tells them this is the case.

## Aggregating into a spreadsheet

The simplest workflow once submissions start arriving by email:

1. Create a Google Sheet (or Excel) with one row per participant and columns for the SUS score, each SUS item, each SafeStep item, the open-ended answers, and the demographics.
2. For each incoming email, paste the values from the email into a new row.
3. Put `=AVERAGE(B2:B100)` (or similar) at the top to get the running mean SUS score across all participants.

For 6 participants this takes about 5 minutes total.

## How responses are handled

Each participant submits the form. The page then displays:

- Their computed SUS score and adjective band
- A plain-text summary of all responses (demographics, SUS, SafeStep-specific items, open-ended)

The participant can then **copy** the summary to clipboard or **download** it as a `.txt` file, and send it to the team. This intentionally avoids any backend, database, or third-party form service — the team aggregates the responses manually, which is appropriate for a six-participant academic study.

## References

- Brooke, J. (1996). *SUS: a "quick and dirty" usability scale*. In Usability Evaluation in Industry.
- Bangor, A., Kortum, P., & Miller, J. (2009). *Determining what individual SUS scores mean: adding an adjective rating scale*. Journal of Usability Studies, 4(3), 114–123.

## Licence

This questionnaire is part of an academic submission and is provided for educational reference.
