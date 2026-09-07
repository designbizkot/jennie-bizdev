# Jennie — BD Lead Sourcing: Standing Instructions

I am Jennie, a BD manager for Bizkit. This is my recurring lead-sourcing task.

## Scope filter (applies to every run, including backfills)

Only research and log companies that meet **both** of these:

1. **UK-based** — `Country` must be exactly `United Kingdom`.
2. **Industry** — `Industry` must be `Fintech` or `Edtech` (a closely
   related sub-category like Insurtech/RegTech/Proptech-fintech is fine to
   log as e.g. "Fintech (Insurtech)", but the row must clearly belong to
   one of these two verticals — not just "financial software used by
   fintechs" or "used mostly by schools").

Apply this filter to every portfolio company found across all four
sources below. If a company doesn't match — wrong country, or an industry
outside Fintech/Edtech — **do not add it to `leads.csv`**. This applies
to new runs and to any backfill/cleanup of existing rows.

## Sources: two-tier approach

**Tier 1 — Primary sources.** Work these first, every run:

- https://www.joinef.com/ (Entrepreneur First)
- https://foundersfactory.com/ (Founders Factory)
- https://www.bethnalgreenventures.com/portfolio (Bethnal Green Ventures)
- https://seedcamp.com/ (Seedcamp)

Find portfolio companies here, apply the scope filter, and try to fill
the 8 required fields directly from what these sources surface (portfolio
descriptions, linked company sites, etc.).

**Tier 2 — Fallback sources.** Use these when a company passes the scope
filter but Tier 1 didn't yield full contact info (no named person, no
LinkedIn/email, industry/location unclear). Only 9 fallback sources are
currently confirmed/approved — do not invent additional ones:

- *Accelerators & Incubators*: startupbootcamp.org, techstars.com,
  plug-and-play.tech — check if the company also appears in one of these
  programs' own portfolio/alumni listings (sometimes surfaces a founder
  bio or team page Tier 1 didn't have).
- *VC firms & investment platforms*: crunchbase.com, beauhurst.com,
  seedtable.com, angel.co, wellfound.com — company profile pages here
  often list founders, funding rounds, HQ location, and industry tags
  directly.
- *Startup directories & company lists*: firmbase.co — curated UK company
  listings, sometimes with contact/industry data Tier 1 lacks.

**How this actually works technically:** this environment's network
egress is restricted, and in practice almost all direct site fetches
(Tier 1 and Tier 2 domains alike) get blocked except the Tier 1 portfolio
root pages. The real mechanism that works is **WebSearch** — searching
`"[Company Name]" founder`, `"[Company Name]" funding`, etc. surfaces
indexed results *from* Crunchbase, Wellfound, press coverage, and the
other Tier 2 sources without needing a direct fetch to succeed. So "use
Crunchbase as a fallback" in practice means "WebSearch queries that
surface Crunchbase's indexed company data," not necessarily a direct
crunchbase.com fetch. Note in `Source Notes` which underlying source the
information actually came from (e.g. "via WebSearch, Crunchbase listing"),
since that's what determines confidence, not which tier it's nominally
from.

## The 8 required fields

For every company that passes the scope filter, collect and populate:

1. **Company Name**
2. **First Name** (of a target contact — prefer a founder, CEO, or a
   Product/Design lead; see methodology below)
3. **Last Name**
4. **Job Title**
5. **Country** — must be `United Kingdom` (this is the scope filter, not
   optional)
6. **City** — HQ location (or the contact's location if more specific and
   known)
7. **Industry** — `Fintech` or `Edtech` (see scope filter above)
8. **Email or LinkedIn URL** — at least one of these two is required

Why these matter: this is a contact-enrichment list for BD outreach, not
just a company list — Bizkit needs a named person and a way to reach or
verify them (LinkedIn if not email), plus enough company context (country,
city, industry, funding) to prioritize and qualify the lead.

A ninth field, **Funded (Y/N)**, is also collected (see schema below) but
is not one of the 8 required-for-inclusion fields — log it as best-effort
and leave blank if genuinely unknown.

**Never guess or fabricate a name, email, or LinkedIn URL.** If a field is
still blank after working through the methodology below, leave it blank
and explain the gap in `Source Notes` (e.g. "founder name not publicly
available", "email not published", "industry unclear from available
sources") — do not skip the row entirely just because it's incomplete;
log what you have and note what's missing (see "Incomplete rows" below).

## Research methodology (priority order)

Work through these in order for each company; stop as soon as you have
enough to fill the 8 fields, but don't stop after step 1 if fields are
still missing — keep going down the list. Steps 1 is Tier 1; steps 2-6 are
Tier 2 fallback, used via WebSearch as described above.

1. **Company's own website** (Tier 1 first) — About, Team, `/team`,
   `/leadership`, `/people` pages. Look for names + titles of founders or
   Product/Design leads.
2. **Crunchbase** (Tier 2) — search by company name; pull founder names,
   funding info, HQ location. Example: `"Acme Ltd" site:crunchbase.com`
   or `"Acme Ltd" crunchbase founder`.
3. **AngelList / Wellfound** (Tier 2) — team profiles, founder bios.
   Example: `"Acme Ltd" wellfound team` — often surfaces a founder's job
   title directly from their team-page listing.
4. **News/press** (Tier 2, plus general web) — WebSearch
   `"[Company Name]" founder`, `"[Company Name]" funding`, TechCrunch,
   UKTN, sector press (e.g. FinTech Wales, EdTech coverage), and
   beauhurst.com / seedtable.com / firmbase.co rankings and curated lists.
   Extract names and titles from funding announcements — these are
   usually the richest source for founder names on early-stage companies.
5. **GitHub** — search for the company's GitHub org; find founder/team
   member profiles with real names (most useful for more technical
   fintech/edtech products).
6. **Twitter/X** — search `"[Company Name]"` or `"[Founder Name]"`, check
   company/founder bios for full names and location hints.
7. **Job postings** (Tier 2, via startupbootcamp.org / techstars.com /
   plug-and-play.tech alumni listings, or general job-board WebSearch) —
   a current job ad ("reporting to our Head of Design, Jane Smith...")
   can reveal team structure and titles even when there's no formal team
   page. Example: `"Acme Ltd" hiring job description` to surface listings
   that name existing team members.
8. **Email inference** — if you have a first name and a confirmed company
   domain, you may suggest a likely-format email (`firstname@company.com`,
   `first.last@company.com`, etc.), but you **must** flag it explicitly as
   `inferred` in `Source Notes` (e.g. "Email inferred from name + domain
   pattern, not verified"). Never present an inferred email as confirmed.
9. **LinkedIn URLs surfaced in search results** — if a LinkedIn profile
   URL appears in WebSearch results or on the company's own pages, capture
   it directly rather than re-deriving it.

If, after working through this list, a required field is still blank, do
not guess — leave it blank and say why in `Source Notes`.

## Incomplete rows

Rows with incomplete data should be **noted, not skipped**. If a company
clearly passes the scope filter (confirmed UK + Fintech/Edtech) but a
contact or some fields can't be found within reasonable effort, still add
the row with what you have, and use `Source Notes` to say exactly what's
missing and why (e.g. "no named contact found - team page lists no
individuals", "Country confirmed UK but City not found"). The scope filter
itself is not optional — a company failing the UK or Fintech/Edtech check
should not be added at all — but once a company passes that filter, don't
let missing contact details cause you to drop it.

## Output

Save results to `leads.csv` (append new findings on each run rather than
overwriting past results, unless asked to start fresh) with exactly these
columns:

```
Company Name, First Name, Last Name, Job Title, LinkedIn URL, Email, Country, City, Industry, Funded (Y/N), Source Notes
```

- `Company Name`: the company name.
- `First Name` / `Last Name`: name of the target contact. Prefer a
  Product/UX/UI Designer or Head of Design; if none is identifiable,
  fall back to a Founder/CEO or other senior contact found via the
  methodology above. Leave both blank (per "Incomplete rows" above) if no
  reliable person can be identified.
- `Job Title`: that contact's job title, as found.
- `LinkedIn URL`: that contact's LinkedIn profile URL, if found.
- `Email`: that contact's email address, only if found directly, or
  explicitly flagged `inferred` per methodology step 7 above.
- `Country`: must be `United Kingdom` (scope filter).
- `City`: the company's HQ location, or the contact's location if more
  specific and known.
- `Industry`: `Fintech` or `Edtech` (scope filter); a bracketed
  sub-category is fine, e.g. `Fintech (Insurtech)`.
- `Funded (Y/N)`: whether the company has received any funding. Best
  effort — leave blank if genuinely unknown.
- `Source Notes`: where this row's data came from and how confident it
  is — e.g. "direct site research", "WebSearch fallback (site
  unreachable)", "low confidence — ambiguous name match", "email
  inferred, not verified", "no named contact found". Always fill this in;
  it's the main way to judge data quality at a glance since there's no
  separate confidence column.

Do not include any other columns (no Website, Source, Has Designer,
Screenshot Saved, Notes, Date Found, Founded, Funding Date, Design
Quality, or Product Image — this schema replaced all of those).

## Tools / approach

- Use WebFetch first on Tier 1 portfolio pages to identify companies and
  team/about pages.
- For contact enrichment, use WebSearch as the primary mechanism — it
  reaches Crunchbase, Wellfound, news/press, and the other Tier 2 sources
  via indexed search results even when a direct fetch to that domain
  would be blocked. GitHub and Twitter/X search are also fair game.
- Direct site access (Tier 1 or Tier 2) can be blocked by network egress
  policy in this environment (has happened repeatedly) — when that
  happens, rely on WebSearch and note the fallback explicitly in
  `Source Notes`, including which underlying source (e.g. Crunchbase,
  a press article) the WebSearch result actually came from.
- Only use the 9 confirmed Tier 2 fallback sources listed above — don't
  invent or assume additional "approved" sources beyond these plus
  WebSearch/GitHub/Twitter.
- This is a recurring task — re-run periodically to catch new portfolio
  additions. Avoid duplicate rows for companies already logged in
  `leads.csv` (check `Company Name` first, only add new companies or
  updates to existing ones).
- Apply the scope filter (UK + Fintech/Edtech) before spending research
  time on a company's contact details — filter first, then research.

## Weekly email (Sunday routine)

After committing and pushing `leads.csv` (and any other changes), send an
email to design@bizkitgroup.com via the Gmail connector, structured exactly
like this:

```
Subject: Bizkit BD Lead Sourcing — <date>

GitHub Commit
[Link to branch] | Commit: [short commit hash]

Summary
• X new companies added (Y total)
• Z with confirmed contact info
• [Any major blockers or gaps this run]

Breakdown by Source
• Founders Factory: X companies
• Seedcamp: X companies
• Entrepreneur First: X companies
• Bethnal Green Ventures: X companies

Flagged Issues (if any — only include this section if there are problems)
• [Issue 1: brief explanation]
• [Issue 2: brief explanation]

Attachment: leads.csv (the actual file)
```

- Keep every bullet to 1–2 lines — no long explanations in the body.
- The branch link is
  `https://github.com/designbizkot/jennie-bizdev/tree/claude/bizkit-designer-leads-ggcih0`;
  prefer linking the specific commit just pushed
  (`https://github.com/designbizkot/jennie-bizdev/commit/<sha>`) when you
  have the SHA.
- **Attach the actual current `leads.csv` file** (full file, all rows, not
  just this run's new ones) as a real CSV attachment on the email — not a
  pasted table, not a link only. The recipient needs to download and open
  it directly from the email.
- Omit the "Flagged Issues" section entirely if there's nothing to flag.
