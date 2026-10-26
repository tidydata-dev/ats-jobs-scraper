# Workday, Greenhouse, Lever & Ashby Jobs Scraper — Python, Node.js & cURL examples

Get **job postings straight from company career sites** — **Workday, Greenhouse, Lever, Ashby, Workable, SmartRecruiters, Recruitee, Personio and Breezy** — with title, location, department, **salary** (when published), posting date, description and apply link. Filter by keyword, location, remote and date; **only new jobs** since the last run for daily alerts. **$1 per 1,000 jobs**.

Hosted on Apify: **[Workday, Greenhouse, Lever & Ashby Jobs Scraper](https://apify.com/tidydata/ats-jobs-scraper?fpr=wtg6qt)**. These examples show how to call it from your code; the Actor runs in the cloud, no API key for the source site, no proxies to manage.

## Python

```bash
pip install apify-client
export APIFY_TOKEN=...   # free account at apify.com → Settings → API & Integrations
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("tidydata/ats-jobs-scraper").call(run_input={
    "companies": [
        "https://boards.greenhouse.io/figma",
        "https://jobs.ashbyhq.com/ramp",
        "https://nvidia.wd5.myworkdayjobs.com/NVIDIAExternalCareerSite"
    ],
    "keywords": [
        "engineer"
    ],
    "postedWithinDays": 14
})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print({k: item.get(k) for k in ['company', 'ats', 'title', 'location', 'postedAt', 'url']})
```

## Node.js

```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('tidydata/ats-jobs-scraper').call({"companies": ["https://jobs.lever.co/palantir"], "remoteOnly": true, "onlyNewJobs": true});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items.length, items[0]);
```

## cURL (one call, results as JSON)

```bash
curl -s -X POST "https://api.apify.com/v2/acts/tidydata~ats-jobs-scraper/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"companies": ["https://jobs.lever.co/palantir"], "remoteOnly": true, "onlyNewJobs": true}'
```

## More TidyData Actors

[YouTube Transcript](https://apify.com/tidydata/youtube-transcript-scraper?fpr=wtg6qt) · [YouTube Comments](https://apify.com/tidydata/youtube-comments-scraper?fpr=wtg6qt) · [YouTube Scraper](https://apify.com/tidydata/youtube-channel-scraper?fpr=wtg6qt) · [Website Contacts](https://apify.com/tidydata/website-contact-extractor?fpr=wtg6qt) · [Google News](https://apify.com/tidydata/google-news-scraper?fpr=wtg6qt) · [App Reviews](https://apify.com/tidydata/app-reviews-scraper?fpr=wtg6qt) · [Merge & Dedupe](https://apify.com/tidydata/merge-dedupe-datasets?fpr=wtg6qt) · [all of them](https://github.com/tidydata-dev)

Examples are MIT-licensed.

---
<sub>Links to apify.com include our affiliate ID: if you start a paid Apify plan through them, Apify pays TidyData a commission at no extra cost to you.</sub>
