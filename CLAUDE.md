# Jennie — BD Lead Sourcing: Standing Instructions

I am Jennie, a BD manager for Bizkit. This is my recurring lead-sourcing task.

## Task

Visit these accelerator/VC portfolio sites and find portfolio companies:

- https://www.foundersfactory.com/
- https://seedcamp.com/
- https://www.joinef.com/
- https://www.bethnalgreenventures.com/portfolio

## Scope filter

- Only UK-based startups (Country = United Kingdom)
- Only Fintech or Edtech industries

## Fields to populate

For each company found, research and populate all fields:

1. **Company Name** — exact legal company name
2. **First Name** — of a target BD/design contact (founder, Product Lead,
   or Design Lead preferred)
3. **Last Name** — of that contact
4. **Job Title** — their current role/title
5. **LinkedIn URL** — direct link to their LinkedIn profile
6. **Email** — their work email (if publicly listed)
7. **Country** — must be `United Kingdom`
8. **City** — where the company is based
9. **Industry** — must be `Fintech` or `Edtech`
10. **Funded (Y/N)** — whether they have received funding

## Research methodology (in priority order)

1. **Company website** — About, Team, `/team`, `/leadership`, `/people`
   pages for names and titles
2. **Crunchbase** — founder names, funding info, location
3. **AngelList/Wellfound** — team profiles, founder bios
4. **WebSearch** — `'[Company Name]' + 'founder'`,
   `'[Company Name]' + 'funding'`, `'[Company Name]' + 'team'`
5. **GitHub** — company org profile for founder/team member names
6. **Twitter** — company or founder bio for full names
7. **Email inference** — if you have first name + company domain, suggest
   likely format (firstname@company.com) and flag as 'inferred' in
   Source Notes

**Rule:** Never guess or leave a field blank without noting why. If data
is unavailable, leave blank and note in Source Notes ('founder name not
public', 'email not published', 'industry unclear', etc.).

## Fallback research sources

If primary sources don't have enough data, use these:

- Startupbootcamp.org
- Techstars.com
- Plug-and-play.tech
- Crunchbase.com
- Beauhurst.com
- Seedtable.com
- Angel.co
- Wellfound.com
- Firmbase.co

## Output

Save results to `leads.csv` (append new rows on each run) with these
columns:

```
Company Name, First Name, Last Name, Job Title, LinkedIn URL, Email, Country, City, Industry, Funded (Y/N), Source Notes
```

- **Source Notes**: Where the data came from (company site, Crunchbase,
  WebSearch, inferred, etc.) + confidence level (direct/high-confidence,
  research-based, low-confidence).

## Weekly email (Sunday routine)

Send email to design@bizkitgroup.com with:

- GitHub commit link at the top
- Summary: # new companies added, # from each source, any blockers
- Breakdown by source (Founders Factory, Seedcamp, EF, BGV)
- Flagged issues (only if relevant)
- All bullets, max 1–2 lines each
- Attach leads.csv as a downloadable .csv file (not a link)
