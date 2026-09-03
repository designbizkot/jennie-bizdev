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
2. Check the team/about page for job titles containing "Product Designer",
   "UX Designer", "UI Designer", "UX/UI Designer", or similar design titles.
3. Try to find a screenshot-able view of their product UI (app screenshot,
   dashboard preview, product demo page, etc.) on their site and save it as
   an image file in `screenshots/` (filename: `<company-slug>.png`).
4. Record a row in the output CSV.

## Output

Save results to `leads.csv` (append new findings on each run rather than
overwriting past results, unless asked to start fresh) with these columns:

```
Company, Website, Source, Has Designer (Y/N), Designer Titles Found, Screenshot Saved (Y/N), Notes, Date Found, Founded, Funded (Y/N), Funding Date, Design Quality, Product Image
```

- `Source`: which of the 4 sites the lead was found on.
- `Has Designer`: Y/N based on whether a Product/UX/UI Designer title was
  found on the team/about page.
- `Designer Titles Found`: semicolon-separated list of exact titles found
  (empty if none).
- `Screenshot Saved`: Y/N — Y only if a screenshot file was actually saved
  to `screenshots/`.
- `Notes`: anything relevant — e.g. "no team page found", "site down",
  "team page requires login", etc.
- `Date Found`: date the row was researched (YYYY-MM-DD).
- `Founded`: the year (or full date, if known) the company was founded.
  Leave blank rather than guessing if not findable.
- `Funded`: Y/N — whether the company has received any funding (per its
  site, Crunchbase, press, etc.).
- `Funding Date`: when they received (most recent) funding, if known.
  Leave blank if unknown or if `Funded` is N.
- `Design Quality`: your own judgment on whether the product/website UI
  looks weak — e.g. "outdated, cluttered layout, no real product
  screenshots". Leave blank if the UI looks solid or you couldn't assess it;
  only fill this in to flag a weakness (this is a lead-quality signal for
  BD, not a full design critique).
- `Product Image`: a direct URL to a product screenshot/image found on the
  company's site — something that can be pasted straight into a browser to
  view the image itself (not a page URL, not a local file path). Leave
  blank if no direct image URL is available; never guess or construct one.

## Tools / approach

- Use WebFetch to pull page content and identify team/about pages and
  product screenshots.
- Use a headless browser (Playwright via Bash, Chromium is pre-installed at
  `/opt/pw-browsers/chromium`) to capture actual screenshots when WebFetch
  alone isn't enough (e.g. to render and screenshot a product page).
- Don't spend excessive time on any single company — if a team page or
  product screenshot isn't findable in a reasonable effort, note that in
  `Notes` and move on.
- This is a recurring task — re-run periodically to catch new portfolio
  additions. Avoid duplicate rows for companies already logged in
  `leads.csv` (check first, only add new companies or updates).
