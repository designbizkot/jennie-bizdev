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

## Sources

Visit these accelerator/VC portfolio sites, find companies that look like
potential leads:

- https://www.joinef.com/
- https://foundersfactory.com/
- https://www.bethnalgreenventures.com/portfolio
- https://seedcamp.com/

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
still missing — keep going down the list.

1. **Company's own website** — About, Team, `/team`, `/leadership`,
   `/people` pages. Look for names + titles of founders or Product/Design
   leads.
2. **Crunchbase** — search by company name; pull founder names, funding
   info, HQ location.
3. **AngelList / Wellfound** — team profiles, founder bios.
4. **News/press** — WebSearch `"[Company Name]" founder`,
   `"[Company Name]" funding`, TechCrunch, UKTN, sector press (e.g.
   FinTech Wales, EdTech coverage). Extract names and titles from
   announcements.
5. **GitHub** — search for the company's GitHub org; find founder/team
   member profiles with real names (most useful for more technical
   fintech/edtech products).
6. **Twitter/X** — search `"[Company Name]"` or `"[Founder Name]"`, check
   company/founder bios for full names and location hints.
7. **Email inference** — if you have a first name and a confirmed company
   domain, you may suggest a likely-format email (`firstname@company.com`,
   `first.last@company.com`, etc.), but you **must** flag it explicitly as
   `inferred` in `Source Notes` (e.g. "Email inferred from name + domain
   pattern, not verified"). Never present an inferred email as confirmed.
8. **LinkedIn URLs surfaced in search results** — if a LinkedIn profile
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

- Use WebFetch to pull page content and identify team/about pages.
- Use WebSearch, Crunchbase, AngelList/Wellfound, GitHub, and Twitter/X
  as primary research sources (not just the company's own website) — this
  has become the default approach, not just a fallback, per the
  methodology above.
- Direct site access can be blocked by network egress policy in this
  environment (has happened before) — when that happens, rely on
  WebSearch and the other sources above, and note the fallback explicitly
  in `Source Notes`.
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
