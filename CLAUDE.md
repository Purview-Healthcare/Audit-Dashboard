# Audit Dashboard

Single-page QA dashboard for auditors (`index.html`, published with GitHub Pages from `main`).
It is a separate app from Sasha's Third Eye, which is for supervisors: keep this app's own name,
the Agent Quality report only, and its own saved data.

## AR and Payment Posting are separate processes

The app has two lines of business, switched at the top of the page: **AR** and **Payment Posting** (`LOB` is `'ar'` or `'pp'`).

- A change the user asks for in AR must **not** be made in Payment Posting, and the reverse.
  Apply it only to the line of business named. If the request doesn't say which one, ask.
- Guard line-specific behaviour with `LOB==='ar'` / `LOB==='pp'`, so the other line stays unchanged.
- Each line keeps its own saved data (storage prefix `qa_` for AR, `qapp_` for Payment Posting),
  uploads, RCA entries, exports and shared file. Never mix them.
- After any change, check both lines: the one changed shows the change, and the other is exactly as before.

## Sheets

- **AR QA sheet:** `Audit Data`, `Error Parameters` and `Validation` tabs. It has severities (Fatal / Major / Non-Fatal) and weights,
  and any fatal error scores the audit 0.
- **Payment Posting QA sheet:** `Total Data`, `Error Category & Descriptions` and `Validation Sheet` tabs. It is pass or fail: any error scores 0.
  There is no severity split in its report, and no Error Parameters in Use card.
- QA sheets contain patient details. Never commit them, and never put patient or claim details in commits, pull requests or screenshots.
