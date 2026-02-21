# Avvo Lawyers Scraper

Extract comprehensive attorney profiles from Avvo with ratings, reviews, practice areas, contact information, and professional credentials at scale.

---

## Overview

The **Avvo Lawyers Scraper** extracts detailed information from Avvo.com, the leading online legal directory. Collect attorney profiles including practice areas, client ratings, phone numbers, email addresses, bar admissions, education, and professional experience to build comprehensive legal databases.

### Key Benefits

- **Legal Research** — Build attorney databases for market analysis and competitive intelligence
- **Lead Generation** — Find qualified attorneys by practice area and location  
- **Directory Services** — Power legal directory platforms with fresh, real-time attorney data
- **Credential Verification** — Verify bar admissions, licenses, and professional standing
- **Market Intelligence** — Track attorney ratings, review trends, and service offerings

---

## Features

- **Complete Attorney Profiles** — Name, ratings, contact info, practice areas, education, and credentials
- **Multiple Extraction Methods** — Reliable data extraction with automatic fallbacks
- **Pagination Handling** — Automatically collects results across multiple pages
- **Profile Enrichment** — Detailed enrichment from attorney profile pages
- **Contact Information** — Phone numbers, emails, and office addresses
- **Bar & License Data** — Years licensed, state bar admissions, certifications
- **Language Support** — Languages spoken by each attorney
- **Duplicate Removal** — Smart deduplication across pagination

---

## Use Cases

### Legal Research & Market Analysis

Analyze attorney demographics, practice area distribution, ratings, and geographic coverage for understanding the legal services market and competitive landscape.

### Lead Generation for Legal Services

Build targeted lists of attorneys by practice area and location for business development, partnerships, and referral networks.

### Attorney Directory Development

Power legal directory websites, attorney matching platforms, and client referral services with up-to-date data and profiles.

### Compliance & Background Checks

Verify attorney credentials, bar admissions, and professional qualifications for client vetting and compliance verification.

---

## Input Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `startUrl` | String | Yes | `https://www.avvo.com/bankruptcy-debt-lawyer/al.html` | Direct Avvo directory URL to scrape from |
| `maxLawyers` | Integer | No | `20` | Maximum lawyer profiles to extract (1-10000) |
| `maxListingPages` | Integer | No | `10` | Maximum pages to crawl (each page ~5 lawyers) |
| `includeReviews` | Boolean | No | `false` | Fetch additional review-related details from profile pages (slower) |
| `includeContactInfo` | Boolean | No | `false` | Fetch additional contact details from profile pages (email, phone, office address) (slower) |
| `proxyConfiguration` | Object | No | `{useApifyProxy: true}` | Proxy settings for reliable scraping |

---

## Output Data

Each lawyer profile contains:

| Field | Type | Description |
|-------|------|-------------|
| `name` | String | Attorney full name |
| 'firmName' | String | Attorney firm name |
| `avvoRating` | Number | Avvo rating (1-10 scale) |
| `clientRating` | Number | Client/user rating from reviews |
| `reviewCount` | Integer | Number of client reviews |
| `practiceAreas` | Array | Legal specializations and areas |
| `location` | String | Office address (city, state, ZIP) |
| `phone` | String | Contact phone number |
| `email` | String | Contact email address |
| `website` | String | Website URL |
| `licenseYear` | Integer | Year licensed to practice |
| `barAdmissions` | Array | State bars and court admissions |
| `languages` | Array | Languages spoken |
| `profileUrl` | String | Avvo profile URL |
| `bio` | String | Professional biography |
| `education` | Array | Law school and university education |
| `awards` | Array | Professional recognition and honors |
| `coordinates` | Object | Geographic coordinates (lat/lon) |
| `scrapedAt` | String | ISO timestamp of extraction |

---

## Sample Output

```json
{
  "name": "Ronald C. Sykstus",
  "avvoRating": 10,
  "clientRating": 5,
  "reviewCount": 255,
  "practiceAreas": ["Bankruptcy", "Debt Collection Defense", "Foreclosure Defense"],
  "location": "Birmingham, AL 35203",
  "phone": "(205) 555-0123",
  "email": "contact@example.com",
  "website": "https://www.example.com",
  "licenseYear": 1988,
  "barAdmissions": ["Alabama State Bar", "U.S. District Court"],
  "languages": ["English", "Spanish"],
  "profileUrl": "https://www.avvo.com/attorneys/12345-john-smith.html",
  "bio": "Experienced bankruptcy attorney serving Birmingham and surrounding areas.",
  "education": ["Harvard Law School, J.D., 2008"],
  "awards": ["Super Lawyers Rising Star 2022", "Avvo Client's Choice 2023"],
  "coordinates": {"lat": 33.5186, "lon": -86.8104},
  "scrapedAt": "2026-02-20T10:30:00.000Z"
}
```

---

## Usage Examples

### Basic Search (Bankruptcy Lawyers in Alabama)

Extract 20 bankruptcy lawyers from Alabama:

```json
{
  "startUrl": "https://www.avvo.com/bankruptcy-debt-lawyer/al.html",
  "maxLawyers": 20,
  "includeReviews": false,
  "includeContactInfo": false,
  "proxyConfiguration": {
    "useApifyProxy": true
  }
}
```

### Large Scale Collection

Collect 100+ lawyers across multiple pages:

```json
{
  "startUrl": "https://www.avvo.com/personal-injury-lawyer/ca.html",
  "maxLawyers": 100,
  "maxListingPages": 20,
  "includeReviews": true,
  "includeContactInfo": true,
  "proxyConfiguration": {
    "useApifyProxy": true,
    "apifyProxyGroups": ["RESIDENTIAL"]
  }
}
```

### Fast Testing (Minimal Data)

Quick run with minimal result count:

```json
{
  "startUrl": "https://www.avvo.com/family-lawyer/ny.html",
  "maxLawyers": 10,
  "maxListingPages": 2,
  "includeContactInfo": false
}
```

---

## Tips for Best Results

### Choose Working URLs

- Use Avvo directory URLs in the format: `https://www.avvo.com/[practice-area]/[state-code].html`
- Practice areas: `bankruptcy-debt`, `family`, `criminal-defense`, `personal-injury`, `real-estate`, `business`, etc.
- US state codes: `al`, `ca`, `ny`, `tx`, `fl`, etc.

### Optimize Collection Size

- Start with `maxLawyers: 20-50` to test quickly
- Increase for production runs to `100+`
- Typical page contains ~5 lawyers per page

### Enable Proxies for Reliability

- Always enable Apify Proxy for best results
- Residential proxies recommended for large-scale scraping
- Helps bypass rate limiting and access restrictions

### Performance Expectations

- **Small runs** (10-20 lawyers): ~1-2 minutes
- **Medium runs** (50-100 lawyers): ~3-5 minutes  
- **Large runs** (200+ lawyers): ~10-20 minutes

---

## Scheduling & Automation

### Automated Updates

Set up recurring scrapes to maintain fresh attorney data:

1. Open the Actor in Apify Console
2. Navigate to **Schedules**
3. Create daily or weekly schedule
4. Configure your search parameters
5. Enable email or Slack notifications

### Integration Options

- **Webhooks** — Trigger actions when run completes
- **Zapier/Make** — Automate workflows without coding
- **Google Sheets** — Auto-export results to spreadsheets
- **Slack/Discord** — Receive notifications with summaries
- **Custom API** — Integrate via HTTP requests

---

## Export Formats

Download your data in multiple formats:

- **JSON** — Structured format for applications and APIs
- **CSV** — Spreadsheet format for Excel/Google Sheets
- **Excel** — Native .xlsx with formatting
- **XML** — Enterprise system integration
- **HTML** — Ready-to-publish web format

---

## Frequently Asked Questions

### How many lawyers can I scrape?

You can collect all available lawyers by increasing `maxLawyers` (0 = unlimited). However, very large runs may take considerable time. Start with reasonable limits like 50-100 for testing.

### Do I need to use proxies?

Proxies are highly recommended for reliability. Avvo has anti-bot protection, and residential proxies provide the best success rate. Apify Proxy is included with your account.

### What practice areas are supported?

All practice areas available on Avvo are supported. Use the practice area slug from Avvo's URL structure (e.g., `bankruptcy-debt`, `personal-injury`, `criminal-defense`).

### How often is the data updated?

Data is extracted in real-time during each run, ensuring you always get the most current attorney information available.

### What if some fields are missing?

Not all attorneys provide complete information on Avvo. Missing fields will be returned as null or empty values. This is normal.

### Can I export to Google Sheets?

Yes, use Apify's native Google Sheets integration or download CSV and import manually into your spreadsheet.

### How long do runs typically take?

- 20 lawyers: ~1 minute
- 50 lawyers: ~2-3 minutes
- 100 lawyers: ~5-10 minutes

---

## Compliance & Ethics

### Responsible Use

This scraper extracts publicly available attorney information from Avvo's directory for legitimate business purposes including research, analysis, and directory development.

### Best Practices

- Use data in accordance with applicable laws and regulations
- Respect attorney privacy and professional information
- Implement reasonable rate limiting
- Use proxies responsibly
- Do not scrape for spamming, harassment, or illegal purposes
- Comply with data protection regulations (GDPR, CCPA, etc.)

---

## Support & Resources

### Need Help?

- **Documentation**: [Apify Docs](https://docs.apify.com)
- **Community**: [Discord Server](https://discord.com/invite/jyEM2PRvMU)
- **Issues**: Report problems via Actor feedback form
- **Contact**: Message through Apify Console

### Additional Resources

- [API Reference](https://docs.apify.com/api/v2)
- [Scheduling Runs](https://docs.apify.com/schedules)
- [Data Export Guide](https://docs.apify.com/storage/dataset)

---

## Legal Notice

This actor extracts publicly available information from Avvo.com for legitimate data collection purposes. Users are responsible for ensuring compliance with website terms of service, applicable laws, and data protection regulations. Use extracted data responsibly and respect all legal requirements.

---

**Keywords** — avvo scraper, lawyer scraper, attorney directory, legal data, attorney leads, bar directory, practice areas, lawyer profiles, legal services

---
