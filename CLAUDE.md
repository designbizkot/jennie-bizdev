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
First Name, Last Name, Job Title, LinkedIn URL, Email, Company Name, Company Website, Country, City, Industry, Has Designer (Y/N), Designer Titles Found, Funded (Y/N), Source, Notes, Design Score (1-10), Design Quality (Good/Fair/Poor), Design Notes, Screenshot URL
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
- **Design Score (1-10)** — rating of the company's website/product design
  (1 = poor, 10 = excellent), from the Design Analysis Step below
- **Design Quality (Good/Fair/Poor)** — bucketed version of the score
  (Good = 8-10, Fair = 5-7, Poor = 1-4)
- **Design Notes** — brief feedback (e.g. 'modern layout, good contrast',
  'outdated typography', 'mobile not optimized')
- **Screenshot URL** — GitHub link to the saved screenshot:
  `https://github.com/designbizkot/jennie-bizdev/blob/[branch]/screenshots/[company-slug].png`

## Design Analysis Step

For each company, after gathering contact/company info:

1. **Screenshot** the company's main homepage using thum.io (no signup/API
   key required, 1,000 free screenshots/month):
   ```bash
   curl -sS -L "https://image.thum.io/get/https://COMPANY-DOMAIN/" -o screenshots/company-slug.png
   ```
   - thum.io needs ~10-15s to render an uncached URL. A too-fast fetch
     returns an animated placeholder GIF instead of the real PNG — check
     the file (`file screenshots/company-slug.png` should say `PNG`, not
     `GIF`), and if it's a GIF, wait ~15s and re-fetch.
   - Verify the company's exact domain before requesting the screenshot
     (don't guess — confirm from prior research) to avoid capturing the
     wrong site.
   - Free tier renders at a fixed ~600x600 viewport with no full-page
     capture — that's expected, not a failure.
   - Some pages will be mostly obscured by a cookie-consent modal (no way
     to dismiss it without a real browser). Note this in Design Notes
     rather than treating it as a capture failure, and score only what's
     visible.
2. **Analyze** the screenshot using vision to assess:
   - Visual hierarchy & layout clarity
   - Typography & readability
   - Color scheme & contrast
   - Mobile responsiveness signals
   - Overall polish & professionalism
   - Modern design patterns vs. outdated aesthetics
3. **Rate** the design 1-10 and give brief feedback (Design Notes).
4. **Save** the screenshot to `screenshots/[company-slug].png`.
   - Naming: `company-slug.png` (e.g. `revolut.png`). If two companies
     share a slug, disambiguate: `fabric-fintech.png`, `fabric-fashion.png`.
5. **Link** the screenshot in the CSV's Screenshot URL column using the
   GitHub blob URL format above.

This step requires working outbound network access (confirmed working via
curl/WebFetch in this environment — Playwright/Chromium is not, due to a
proxy issue with the browser's connection pattern, so don't use it here).
If thum.io cannot reach a company's site, leave the Design
Score/Quality/Notes/Screenshot URL fields blank and note the failure
reason in Notes rather than fabricating a rating.

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
