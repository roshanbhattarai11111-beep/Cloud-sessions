# AI Marketing Agent Team — Veritas Advisory (veritasadvisory.com.np)

Goal: build an AI agent team that grows inbound leads for a Chartered Accountancy firm in Nepal through **LinkedIn**, **Google Search (via Search Console data)**, and a steady flow of **articles and posts**.

> **Assumptions** (change them if they're wrong): small firm (1–5 partners), services cover tax (Income Tax, VAT, TDS), audit, accounting/bookkeeping, company registration with OCR, FDI/compliance advisory, and payroll. The audience is SMEs, startups, NRNs and foreign investors in Nepal. Budget is low (≈ USD 20–60/month). You have no coding background, so the setup is no-code first.

---

## 1. Executive Summary

- **Four agents and one human gate.** A Strategist plans the work, an SEO Analyst reads Search Console data, a Writer drafts articles and LinkedIn posts, and a Compliance & Accuracy Reviewer checks everything. **You approve before anything is published.**
- **The edge is search demand you can prove.** Search Console shows which queries already show your site but don't get clicks. Those queries drive the content plan. Nepal's tax calendar (budget in Jestha, fiscal year ending Ashadh, monthly VAT and TDS deadlines, annual return deadlines) drives the timing.
- **Professional ethics come first.** ICAN's Code of Ethics restricts how CAs can advertise and solicit. Content must be **educational, factual and not self-laudatory**: no "best CA in Nepal", no fee comparisons, no testimonials and no guaranteed outcomes. One agent exists only to enforce this.
- **Expected output per month:** 4 SEO articles, 12–16 LinkedIn posts, 1 Search Console report and a refreshed content calendar. This takes about 2–3 hours of your time, almost all of it reviewing.

---

## 2. Recommended Agent Team

| # | Agent | Model | Why it exists | What breaks without it |
|---|-------|-------|---------------|------------------------|
| 1 | **Strategist** (orchestrator) | Claude Opus 5.5 | Turns goals, the tax calendar and SEO data into a weekly plan | Random posting with no link to demand or deadlines |
| 2 | **SEO Analyst** | Claude Sonnet 5.5 | Reads Search Console exports and finds quick wins and content gaps | You'd write about topics nobody searches for |
| 3 | **Content Writer** | Claude Opus 5.5 | Drafts articles plus a LinkedIn post set from each article | No content gets produced |
| 4 | **Compliance & Accuracy Reviewer** | Claude Opus 5.5 | Checks law and rate accuracy and ICAN ethics, and catches hallucinations | Outdated tax rates or unethical claims get published, risking reputation and ICAN problems |
| 👤 | **You (CA)** | — | Final technical sign-off and publishing | — |

The team leaves out a separate "LinkedIn agent" because the Writer produces posts from each article (one source, many formats), which removes duplicated work. It also leaves out an auto-poster: publishing stays manual until quality is proven.

---

## 3. Agent Blueprints

### Agent 1 — Strategist
- **Purpose:** decide *what* to publish *when* and *why*.
- **Inputs:** the SEO Analyst's report, the Nepal compliance calendar, a list of firm services, and the last 30 days of LinkedIn post performance (impressions, comments, profile visits).
- **Outputs:** a weekly plan with 1 article brief and 3–4 post briefs. Each brief has a topic, target keyword, audience, angle, CTA and deadline-relevance.
- **Tools:** Google Sheet (content calendar) and the SEO report.
- **Success criteria:** at least 70% of planned topics map to a real Search Console query or a real deadline.
- **Guardrails:** never plans content about a law change without a source link (IRD, OCR, Ministry of Finance, NRB or the Finance Act). It marks such topics `NEEDS SOURCE`.

### Agent 2 — SEO Analyst
- **Purpose:** turn Search Console data into decisions.
- **Inputs:** a Search Console Performance export (Queries + Pages, last 3 months, CSV) and the Pages indexing report.
- **Outputs:**
  1. **Quick wins:** queries ranked at positions 5–20 with ≥ 50 impressions. Fix: update the existing page or write a dedicated article.
  2. **CTR fixes:** pages with high impressions and CTR below 2%. Fix: rewrite the title tag and meta description (gives 3 options).
  3. **Content gaps:** service + location queries with no matching page (e.g. "VAT registration Nepal", "audit firm Kathmandu").
  4. **Technical flags:** pages that aren't indexed, crawl errors, or Core Web Vitals warnings.
- **Guardrails:** uses only numbers present in the export and never invents search volumes. When it estimates, it labels the figure `ESTIMATE`.

### Agent 3 — Content Writer
- **Purpose:** produce publish-ready drafts.
- **Inputs:** a brief from the Strategist, the firm voice guide, and source links.
- **Outputs:**
  - **Article** (1,000–1,600 words): H1/H2 structure, a 2–3 sentence answer at the top (helps get featured snippets), worked examples in NPR, an FAQ section (4–6 questions), a meta title (≤ 60 characters), a meta description (≤ 155 characters), a URL slug, 2–3 internal link suggestions, and a factual "how we can help" closing line.
  - **LinkedIn set from each article:** 1 text post (hook, 3–5 insights, question), 1 carousel outline (6–8 slides), and 1 short "deadline reminder" post.
- **Guardrails:** every rate, threshold, date and section number is wrapped as `[VERIFY: …]` with its source. The writer uses no superlatives about the firm and invents no client stories.

### Agent 4 — Compliance & Accuracy Reviewer
- **Purpose:** catch errors before you see the draft.
- **Checks:**
  1. **Accuracy:** flags every figure, deadline and legal reference not backed by a cited source. It flags anything that may have changed in the latest Finance Act.
  2. **Ethics:** no solicitation, self-praise, comparison with other firms, fee advertising, testimonials or guaranteed results.
  3. **Advice risk:** adds a disclaimer ("general information, not professional advice for your specific situation").
  4. **Quality:** answers the target query, reads naturally and isn't keyword-stuffed.
- **Output:** `PASS` / `REVISE` with a numbered issue list. After 2 failed revisions, the draft goes to you.

---

## 4. Workflow Diagram

```
 Monthly (1st week)                       Weekly (every Monday)
 ┌──────────────────────┐                 ┌──────────────────────┐
 │ You export GSC CSV   │                 │ Strategist: weekly   │
 │ → SEO Analyst report │───────────────▶ │ plan + briefs        │
 └──────────────────────┘                 └─────────┬────────────┘
                                                    ▼
                                          ┌──────────────────────┐
                                          │ Writer: article +    │
                                          │ LinkedIn set         │
                                          └─────────┬────────────┘
                                                    ▼
                                          ┌──────────────────────┐   REVISE (max 2)
                                          │ Reviewer: accuracy + │──────────┐
                                          │ ICAN ethics check    │◀─────────┘ back to Writer
                                          └─────────┬────────────┘
                                                    ▼ PASS
                                          ┌──────────────────────┐
                                          │ 👤 YOU: verify every │
                                          │ [VERIFY] tag, approve│
                                          └─────────┬────────────┘
                                                    ▼
                         Publish article on site → request indexing in GSC
                         Schedule LinkedIn posts (personal profile + company page)
                                                    ▼
                         Log results in Google Sheet → feeds next month's Strategist run
```

**Memory and storage:** keep one Google Sheet with tabs `Calendar`, `Briefs`, `Published` (URL, date, keyword) and `Results` (GSC clicks/position and LinkedIn impressions). Keep one Google Doc as the **Firm Voice & Facts** file: services, team credentials, an approved disclaimer, and a list of current tax rates *you* have verified. Every agent reads it, so facts are written down once and checked once.

---

## 5. Prompt Pack (copy-paste)

Paste the **Firm Context block** at the top of every agent's prompt. A Claude Project with the Voice & Facts doc uploaded does this automatically.

### Firm Context block
```
FIRM: Veritas Advisory (veritasadvisory.com.np), a Chartered Accountancy firm in Nepal.
SERVICES: [list your exact services]
AUDIENCE: SME owners, startups, NRNs, foreign investors, finance managers in Nepal.
VOICE: clear, practical, calm authority; plain English (optionally a Nepali summary); NPR examples.
ETHICS (non-negotiable, per ICAN Code of Ethics): educational only. No self-praise
("best", "No.1", "leading"), no comparisons with other firms, no fee advertising,
no testimonials, no guaranteed outcomes, no solicitation of specific clients.
FACTS: Use only figures in the attached "Verified Facts" list. For anything else,
write [VERIFY: claim — suggested source]. Never invent rates, dates, section numbers,
or statistics.
FISCAL CONTEXT: Nepal fiscal year runs Shrawan 1 – Ashadh end (mid-July to mid-July).
Use Bikram Sambat dates alongside AD dates where relevant.
```

### Prompt — Strategist
```
ROLE: You are the content strategist for a Nepali CA firm.
INPUTS: (1) SEO report below, (2) compliance calendar for the next 30 days,
(3) last month's results.
TASK: Produce next week's plan:
- 1 article brief + 3-4 LinkedIn post briefs.
- Each brief: Title | Target keyword (from SEO report, or "none – deadline-driven") |
  Audience | Search intent | Angle (what's genuinely useful) | Key points (5) |
  Sources needed | CTA (soft, e.g. "Questions? Our contact page") | Publish date.
RULES: Prioritise (a) deadlines within 21 days, (b) SEO quick wins, (c) evergreen
service pages. No two briefs on the same keyword. Mark law-change topics NEEDS SOURCE.
OUTPUT: a Markdown table, then the briefs.
```

### Prompt — SEO Analyst
```
ROLE: You are an SEO analyst for veritasadvisory.com.np.
INPUT: Google Search Console exports (Queries.csv, Pages.csv), last 3 months.
TASK:
1. QUICK WINS: queries with position 5–20 and ≥50 impressions. For each:
   query, page, impressions, CTR, position, recommended action.
2. CTR FIXES: pages with ≥200 impressions and CTR <2%. Give 3 new title tags
   (≤60 chars) and 2 meta descriptions (≤155 chars) each.
3. CONTENT GAPS: relevant CA/tax/compliance queries with no dedicated page.
4. BRAND vs NON-BRAND: % of clicks from queries containing "veritas".
5. TOP 5 ACTIONS this month, ranked by expected impact.
RULES: Use only numbers present in the data. Label any estimate ESTIMATE.
Ignore irrelevant queries. If data is too thin (<100 total impressions), say so
and recommend foundational pages instead.
```

### Prompt — Content Writer
```
ROLE: You are a senior writer for a Nepali CA firm, writing for business owners.
INPUT: one brief + Firm Context + Verified Facts.
PRODUCE:
A) ARTICLE (1,000–1,600 words)
   - H1 containing the target keyword naturally
   - "Quick answer" box: 2–3 sentences answering the query directly
   - H2 sections; at least one worked example in NPR; a checklist or table
   - Common mistakes section
   - FAQ (4–6 Q&As phrased like real searches)
   - Closing: one factual line on how Veritas Advisory helps + link to contact page
   - Disclaimer line
   - SEO: meta title, meta description, slug, 3 internal-link suggestions
B) LINKEDIN SET
   - Post 1 (≤1,300 chars): hook line (no clickbait), 3–5 numbered insights,
     closing question, 3–5 hashtags (#NepalTax #VAT #Nepal #Startups etc.)
   - Post 2: carousel outline, 6–8 slides, ≤25 words per slide
   - Post 3: deadline reminder (≤600 chars) if relevant, else a myth-vs-fact post
RULES: Every rate/threshold/date/section → [VERIFY: … | source]. No superlatives
about the firm. No invented clients or statistics. Short sentences.
```

### Prompt — Compliance & Accuracy Reviewer
```
ROLE: You are a strict reviewer combining a tax technical partner and an ICAN
ethics officer.
INPUT: draft article + LinkedIn set + Verified Facts.
CHECK and report:
1. ACCURACY: list every factual claim. Mark each SOURCED / VERIFY / LIKELY WRONG.
   Flag anything that may have changed in the latest Finance Act or budget.
2. ETHICS: quote any phrase that is self-laudatory, comparative, solicitous,
   mentions fees, implies guaranteed results, or uses testimonials. Suggest rewrites.
3. ADVICE RISK: is the disclaimer present? Is anything phrased as personal advice?
4. QUALITY: does it answer the target query in the first 100 words? Any keyword
   stuffing, filler or repetition?
OUTPUT: VERDICT: PASS or REVISE, then a numbered issue list with fixes.
Be conservative: if unsure, REVISE.
```

---

## 6. Starter Content Ideas (verify every specific figure before publishing)

**Articles (SEO)**
1. VAT Registration in Nepal: Who Must Register, Thresholds and Step-by-Step Process
2. TDS in Nepal: Rates Table, Deposit Deadlines and Common Mistakes
3. How to Register a Private Limited Company in Nepal (OCR Process, Documents, Timeline)
4. Income Tax Return Filing for Businesses in Nepal: Deadlines and Checklist
5. Statutory Audit in Nepal: What SMEs Should Prepare Before the Auditor Arrives
6. Foreign Investment (FDI) in Nepal: Approval, Repatriation and Compliance Basics
7. Presumptive / Turnover-Based Tax for Small Businesses in Nepal: Am I Eligible?
8. Budget [FY] Highlights: Key Tax Changes for Businesses (publish within 48 hours of Jestha 15)
9. Bookkeeping for Startups in Nepal: Minimum Records the Law Requires
10. Advance Tax Installments in Nepal: Due Dates and How to Calculate

**LinkedIn post formats that work for CAs**
- "3 mistakes I see in VAT returns every month" (educational, no client names)
- A deadline countdown ("VAT/TDS for the month due in 5 days. Checklist ↓")
- Myth vs fact ("Myth: a new company needn't file tax returns until it profits")
- Budget-day carousels ("What changed for SMEs, 7 slides")
- Behind the profession ("What an audit actually checks", which builds trust without self-praise)
- Post from your **personal profile** first, then reshare on the company page. Personal profiles get far more reach.

---

## 7. Tools & Stack

| Need | Tool | Cost |
|------|------|------|
| Reasoning, writing, review | Claude (Pro plan, using **Projects** with the Facts doc uploaded) | ~USD 20/mo |
| Cheaper bulk tasks (hashtags, title variants) | Claude Haiku 4.5 or Sonnet 5.5 via API (optional) | <USD 5/mo |
| SEO data | Google Search Console (free) + GA4 (free) | 0 |
| Calendar and memory | Google Sheets + Google Docs | 0 |
| Carousel/visual design | Canva (connected here) | Free/Pro |
| Scheduling LinkedIn | LinkedIn native scheduler (free) or Buffer | 0–6 |
| Later automation | Zapier (connected here): new "Approved" row in the Sheet → reminder or scheduled post draft | Free tier |

**Search Console setup:** verify the domain property for `veritasadvisory.com.np`, submit `sitemap.xml`, and use URL Inspection → "Request indexing" for each new article.

---

## 8. 7-Day Implementation Plan

| Day | Task | Time |
|-----|------|------|
| 1 | Verify Search Console and submit the sitemap. Optimise your LinkedIn profile (headline: "Chartered Accountant · Tax, Audit & Compliance for Nepali businesses"). Create the company page if missing. | 1.5 h |
| 2 | Write the **Firm Voice & Facts** doc: services, disclaimer, and current verified rates/thresholds/deadlines with source links. | 1.5 h |
| 3 | Create a Claude Project with the doc uploaded. Save the 4 prompts. Build the Google Sheet (4 tabs). | 1 h |
| 4 | Export Search Console data (thin data is fine) → run the SEO Analyst → run the Strategist for week 1. | 45 min |
| 5 | Writer drafts Article #1 and its LinkedIn set → Reviewer → you verify every `[VERIFY]` tag. | 1.5 h |
| 6 | Publish the article and request indexing. Publish LinkedIn Post 1. Build the carousel in Canva. | 1 h |
| 7 | Schedule the remaining posts. Log everything in the Sheet. Note what slowed you down and adjust the prompts. | 30 min |

---

## 9. Common Mistakes to Avoid

1. **Publishing AI tax figures unverified.** Nepal's rates and thresholds change with each Finance Act. *Prevention:* the `[VERIFY]` tags plus your sign-off, with no exceptions.
2. **Breaching CA advertising ethics.** *Prevention:* the Reviewer agent, plus no "best/leading/No.1" language anywhere.
3. **Writing for other accountants instead of clients.** *Prevention:* every brief names a business-owner audience and the question they'd search.
4. **Generic content that ranks nowhere.** *Prevention:* topics come from GSC queries and Nepal-specific detail (NPR examples, IRD procedures, BS dates).
5. **Posting only on the company page.** Reach is low there. Post from your personal profile.
6. **Over-automating early.** Keep publishing manual for the first 60 days.
7. **Ignoring old pages.** Updating a page sitting at positions 8–15 often beats writing a new one.

---

## 10. Measuring Success & Final Recommendations

**KPIs (tracked monthly in the Sheet)**
- Search Console: non-brand clicks, total impressions, average position of target keywords, and the number of queries in the top 10
- LinkedIn: impressions, followers, profile views, and inbound DMs or connection requests from business owners
- Business: enquiries via the website contact form or WhatsApp and calls, plus **where they said they found you**
- Efficiency: hours per article (target under 1 hour of your time)

**90-day realistic targets:** 12 articles and about 45 posts published, and non-brand impressions up 2–3×. Your first enquiries should be traceable to content. SEO usually needs 3–6 months to compound.

**ROI:** ROI = (new clients × average annual fee) ÷ (tools + your hours × hourly rate). One retained client usually pays for a year of this system.

**Scaling after 60 days:**
- Add Nepali-language versions of the top 5 articles (less competition)
- Turn each article into a short video or reel script
- Add a Zapier flow: Sheet status "Approved" → Buffer draft
- Write a free downloadable "Nepal Compliance Calendar" PDF as a lead magnet

**Where humans stay in control:** every published word, every tax figure, any reply to a prospect, and any mention of fees or engagement terms.
