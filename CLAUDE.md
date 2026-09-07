# Jennie — BD Lead Sourcing: Standing Instructions

I am Jennie, a BD manager for Bizkit. This is my recurring lead-sourcing task.

## Task

Visit these accelerator/VC portfolio sites, find companies that look like
potential leads, and research each one:

- https://www.joinef.com/
- https://foundersfactory.com/
- https://www.bethnalgreenventures.com/portfolio
- https://seedcamp.com/

For each portfolio company found:

1. Visit the company's website.
2. Check the team/about page for a design-related role — job titles
   containing "Product Designer", "UX Designer", "UI Designer",
   "UX/UI Designer", "Head of Design", or similar. This is the target
   contact for BD outreach; if no such role is identifiable, fall back to
   the most senior design-adjacent contact you can find (e.g. a
   Founder/CEO at a very early-stage company).
3. For that contact, try to find: First Name, Last Name, Job Title,
   LinkedIn URL, Email (only if publicly listed — never guess or
   construct one from a name/domain pattern).
4. For the company, try to find: Country, City (HQ location), Industry,
   and Funded (Y/N) status (per its site, Crunchbase, press, etc.).
5. Record a row in the output CSV. Leave any field blank rather than
   guessing if reliable info isn't found — log the company anyway with
   what you do have, noting the gap in `Source Notes`.

## Output

Save results to `leads.csv` (append new findings on each run rather than
overwriting past results, unless asked to start fresh) with exactly these
columns:

```
Company Name, First Name, Last Name, Job Title, LinkedIn URL, Email, Country, City, Industry, Funded (Y/N), Source Notes
```

- `Company Name`: the company name.
- `First Name` / `Last Name`: name of the target contact identified in
  step 2 above. Leave both blank if no reliable person can be identified.
- `Job Title`: that contact's job title, as found.
- `LinkedIn URL`: that contact's LinkedIn profile URL, if found.
- `Email`: that contact's email address, only if found directly (e.g.
  listed on the company site) — never guess or construct an email from a
  name/domain pattern.
- `Country` / `City`: the contact's location if known, otherwise the
  company's HQ location.
- `Industry`: a brief descriptor (e.g. "Fintech", "HealthTech", "AI/ML").
- `Funded (Y/N)`: whether the company has received any funding.
- `Source Notes`: where this row's data came from and how confident it
  is — e.g. "direct site research", "WebSearch fallback (site
  unreachable)", "low confidence — ambiguous name match", "no design
  contact identifiable". Always fill this in; it's the main way to judge
  data quality at a glance since there's no separate confidence column.

Do not include any other columns (no Website, Source, Has Designer,
Screenshot Saved, Notes, Date Found, Founded, Funding Date, Design
Quality, or Product Image — this schema replaced all of those).

## Tools / approach

- Use WebFetch to pull page content and identify team/about pages.
- Use WebSearch as a fallback when direct site access fails (this has
  happened before — some company domains get blocked by network egress
  policy in this environment) to find designer-title and contact signals.
  Note the fallback explicitly in `Source Notes` when used.
- Don't spend excessive time on any single company — if a contact isn't
  findable in a reasonable effort, log the company with blank contact
  fields and a note in `Source Notes`, then move on.
- This is a recurring task — re-run periodically to catch new portfolio
  additions. Avoid duplicate rows for companies already logged in
  `leads.csv` (check `Company Name` first, only add new companies or
  updates to existing ones).

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
