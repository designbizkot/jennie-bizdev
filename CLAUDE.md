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

For each company found, research and populate all fields listed in the
Output section below.

## Research methodology (in priority order)

1. **Company website** — About, Team, `/team`, `/leadership`, `/people`
   pages for:
   - First/Last Name of founder, CEO, or Design/Product lead
   - Job Title of that person
   - LinkedIn URL (check if linked from their bio/profile)
   - Work Email (if publicly listed)
   - Company name, website, location (country/city)
   - Industry classification
   - Any design titles on team page (Product Designer, UX/UI Designer,
     etc.)
2. **Crunchbase** — search company name for:
   - Founder names and titles
   - Funding status and date
   - Company location
3. **AngelList/Wellfound** — team profiles, founder bios, funding info
4. **WebSearch** — `'[Company Name]' + 'founder'`,
   `'[Company Name]' + 'funding'`, `'[Company Name]' + 'team'`
   - Extract founder/leader names from news, press releases,
     announcements
5. **GitHub** — company org or founder GitHub profile for names
6. **Twitter** — company or founder Twitter/X bio for full names and
   titles
7. **LinkedIn search** — if you find a LinkedIn profile URL in search
   results, use it
8. **Email inference** — if you have first name + company domain, suggest
   format (firstname@company.com, first.last@company.com) and flag as
   'inferred' in Notes

**Rule:** Never guess or fabricate a name, email, or LinkedIn URL. If a
field cannot be found, leave it blank and note the reason in Notes
('email not public', 'founder name not listed', etc.).

## Output

Save results to `leads.csv` (append new rows on each run) with these
columns:

```
First Name, Last Name, Job Title, LinkedIn URL, Email, Company Name, Company Website, Country, City, Industry, Has Designer (Y/N), Designer Titles Found, Funded (Y/N), Source, Notes
```

Field definitions:

- **First Name** — first name of target contact (founder, CEO, Product
  Lead, Design Lead)
- **Last Name** — last name of that contact
- **Job Title** — their role/title (e.g. CEO, CTO, Head of Product,
  Product Designer)
- **LinkedIn URL** — direct link to their LinkedIn profile
- **Email** — their work email
- **Company Name** — exact company name
- **Company Website** — company's main website
- **Country** — `United Kingdom`
- **City** — company location
- **Industry** — `Fintech` or `Edtech`
- **Has Designer (Y/N)** — Y if Product/UX/UI/Design title found on team
  page; N if not
- **Designer Titles Found** — semicolon-separated list of exact design
  titles (empty if none)
- **Funded (Y/N)** — Y/N based on research
- **Source** — which portfolio site (Founders Factory, Seedcamp, EF, BGV)
- **Notes** — anything relevant (e.g. 'no designer', 'email not public',
  'source: WebSearch', etc.)

### Weekly email (every run — manual test or scheduled Sunday routine)

After every run, send an email to design@bizkitgroup.com with:

- **Subject**: Bizkit Weekly BD Leads — [Date of run]
- **Email body**:
  - GitHub commit link and hash at top
  - Summary: X new companies added, breakdown by source (Founders
    Factory, Seedcamp, EF, BGV)
  - Any blockers or flagged issues (only if relevant)
  - All text as bullets, max 1–2 lines per point
- **Attachment**: Attach the `leads.csv` file as an actual downloadable
  .csv file attachment (not a link, not pasted text). The Gmail
  connector supports file attachments — attach it directly.
