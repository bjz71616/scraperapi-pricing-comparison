# Apify alternative: what ScraperAPI costs per 1,000 pages, which plan fits, and when Octoparse or Bright Data is the better buy

ScraperAPI starts at **$49/month** ($44.10/month billed annually) for 100,000 credits, runs a 7-day trial with 5,000 credits and no credit card, and bills per successful request. It does not replace the whole Apify platform: there is no Actor marketplace and no point-and-click builder. What it takes over is the layer that makes Apify invoices hard to forecast, namely proxies, IP rotation, CAPTCHA and JavaScript rendering, and it leaves the parsing to code you already have.

This guide covers where Apify's money actually goes, what 100,000 credits buy once the per-domain multipliers apply, which ScraperAPI plan maps to which workload, and the cases where Octoparse, Bright Data or Firecrawl is the better purchase.

> **Quick pick:** if you already have a parser and the only problem is getting blocked, **Hobby at $49/month** (100,000 credits, 20 threads) covers most single-site jobs. Move to **Business at $299** when you need country-level geotargeting outside the US and EU, and to **Scaling at $475** when you want pay-as-you-go rather than a hard stop at your credit limit.
> 👉 [Check the current ScraperAPI plan lineup](https://www.scraperapi.com/pricing/?fp_ref=coupons)

## All ScraperAPI plans

Prices below were checked against the vendor's pricing documentation in October 2026. Annual billing takes exactly 10% off the monthly rate, and the annual figure shown is the effective monthly cost.

| Plan | Credits per month | Concurrent threads | Price (monthly / annual per month) | Start |
| --- | --- | --- | --- | --- |
| Free | 1,000 | 5 | $0 | [Open a free account](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Hobby | 100,000 | 20 | $49 / $44.10 | [Start with Hobby](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Startup | 1,000,000 | 50 | $149 / $134.10 | [Start with Startup](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Business | 3,000,000 | 100 | $299 / $269.10 | [Start with Business](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Scaling | 5,000,000 | 200 | $475 / $427.50 | [Start with Scaling](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Professional | 10,500,000 | 300 | $975 / $877.50 | [Start with Professional](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Advanced | 21,500,000 | 500 | $1,975 / $1,777.50 | [Start with Advanced](https://www.scraperapi.com/pricing/?fp_ref=coupons) |
| Enterprise | 22,000,000+ | 500+ | Custom | [Request an Enterprise quote](https://www.scraperapi.com/pricing/?fp_ref=coupons) |

Four differences matter more than the credit numbers:

- **Geotargeting splits the tiers.** Hobby and Startup are limited to US and EU locations. Country-level geotargeting anywhere in the world starts at Business.
- **Pay-as-you-go starts at Scaling.** On Hobby, Startup and Business, running out of credits returns a 429 and scraping pauses until renewal. No overage charge, but no data either. PAYG on Scaling and above comes with a monthly spending cap you set yourself.
- **Credits reset monthly and do not roll over.** Annual plans hand you the full year's credits upfront, so you can front-load a big crawl, but unused credits still expire with the billing period.
- **Every plan includes the same core stack**: JavaScript rendering, residential and mobile IPs, anti-bot bypass, JSON autoparsing, CAPTCHA handling, custom headers, automatic retries and unlimited bandwidth, plus a stated 99.9% uptime guarantee.

## What 100,000 credits actually cost per page

The headline number is not a page count. ScraperAPI prices by domain and by what the request needs, and the multipliers stack on the base cost of one credit:

| Request type | Credits | Pages per 100,000 credits |
| --- | --- | --- |
| Standard page | 1 | 100,000 |
| Amazon, Walmart, eBay | 5 | 20,000 |
| Google or Bing SERP (incl. subdomains) | 25 | 4,000 |
| LinkedIn | 30 | 3,333 |
| Bot-protection bypass (Cloudflare, DataDome, PerimeterX/HUMAN, Akamai) | +10 | ~9,090 |
| JS rendering (`render=true`) | +10 | ~9,090 |
| Premium proxies plus JS rendering | 25 | 4,000 |
| Ultra premium plus JS rendering | 75 | 1,333 |

Geotargeting, sessions, device type, output format and autoparse cost nothing extra. The bypass surcharge is applied automatically when ScraperAPI decides to activate bypass logic, so a site that adds Cloudflare halfway through the month quietly changes your effective page price.

Do the arithmetic before picking a tier. A team scraping 40,000 Amazon product pages a month needs 200,000 credits, which is Startup, not Hobby. A team monitoring 5,000 Google keyword sets weekly needs 500,000 credits for the month, comfortably inside Startup's 1M. Someone pulling 100,000 plain article pages fits in Hobby with nothing left over.

The dashboard includes a Domain Cost Estimator that prices any URL before you send it, and `max_cost` caps what a single request is allowed to spend. Both are worth five minutes on day one of the trial.
👉 [Price your own target sites on the $49 Hobby plan](https://www.scraperapi.com/pricing/?fp_ref=coupons)

## Where the Apify bill comes from

Apify's published plans are **Starter at $19, Scale at $199 and Business at $999 per month**, and those are platform subscriptions rather than the whole bill. Two layers sit on top of each other:

1. **Actor fees.** Most Store Actors bill per result or per event, for example a fixed amount per 1,000 records.
2. **Platform usage.** Compute units run $0.20 each on the Free and Starter tiers, residential proxies run around $8 per GB, and storage is billed separately.

So the same 100,000 records can produce very different invoices depending on which Actor you picked, and a generic Actor that avoids per-result pricing instead bills by compute unit, which moves with runtime and memory. A JavaScript-heavy target that needs longer browser sessions pushes both numbers up at once.

This is the complaint that shows up in reviews. A web designer on G2 in January 2026 put it as "the pricing can become expensive when you run scrapers at scale." Vendor comparisons of teams that switch away tend to land on the same two reasons: cost that cannot be budgeted per quarter, and the absence of a clear SLA.

None of that makes Apify a bad platform. It rates around 4.7 on G2, ships 40,000+ community and official Actors, offers the Crawlee SDK for JavaScript and Python, and runs residential, datacenter and mobile proxy rotation. It also sells end-to-end managed scraping, so leaving the self-service platform is not the same decision as outsourcing.

The question worth asking is narrower: how much of your monthly spend goes to Actor logic you could write yourself, and how much goes to the unblocking layer underneath. If the split is mostly the second, a dedicated unblocking API removes a layer of billing.

## What ScraperAPI takes over, and what stays with you

**Handled for you:** proxy pools and IP rotation, CAPTCHA solving, bot-protection bypass, JavaScript rendering through `render=true`, automatic retries, an async endpoint for large batches, DataPipeline for scheduled jobs, structured data endpoints that return clean records for Amazon, Google and Walmart instead of raw HTML, and SDKs for Python, Node, PHP, Java, Ruby and Go.

**Still yours:** the parser, the schema, the storage, the deduplication and any orchestration beyond a schedule. There is no Actor library, no visual builder and no hosted dataset product.

That boundary decides whether the swap makes sense. If your current Apify usage is one Store Actor on a schedule and you have never opened the code, ScraperAPI will feel like a demotion: you would be rebuilding the Actor yourself. If you already maintain a parser and keep fighting bans, the reverse is true, since you would be paying twice for logic you own.

The trial is the cheapest way to find out which camp you are in: 7 days, 5,000 credits, no credit card, and a 7-day no-questions-asked refund on a paid plan if the success rate on your targets disappoints.
👉 [Start the 7-day trial with 5,000 credits, no card required](https://www.scraperapi.com/pricing/?fp_ref=coupons)

## How it stacks up against the other names on every list

| Tool | Best for | Entry price | How much code you write |
| --- | --- | --- | --- |
| ScraperAPI | Developers with a parser already in place | $49/mo ($44.10 annual) for 100,000 credits | Parsing only, unless you use the structured endpoints |
| Octoparse | Non-technical teams and long-tail sites | $83/mo monthly, $69/mo annual (checked Sept 2026) | None, point-and-click with 680+ templates |
| Bright Data | Enterprise proxy scale and ready-made datasets | $1.50 per 1,000 records, plans around $499/mo, 5,000 free records/mo | Low if a prebuilt scraper exists |
| Oxylabs | Protected targets and compliance-heavy teams | Web Scraper API from about $49/mo, residential from about $99/mo | Low to medium |
| Firecrawl | RAG and LLM pipelines that want Markdown | Free 1,000 credits/mo, paid from $19/mo | Minimal, one credit per page |
| Scrapy / Crawlee | Full control at zero licence cost | Free, open source | All of it |

A few notes the tables elsewhere skip. Octoparse's free plan lets you export up to 10,000 records and its paid tiers are desktop plus cloud, so it suits someone who wants a scheduled job without a codebase. Bright Data's strength is the owned network (400M+ IPs across 195 countries) and a catalogue of over 1,000 ready scrapers; its pricing is usage-based, so the $499 figure is a plan level, not a flat rate. Oxylabs reports 175M+ owned IPs and a 99.95% success rate, which is what you are paying for when targets are aggressive. Firecrawl's pitch is different in kind: clean LLM-ready Markdown at one credit per page, open source and self-hostable, which matters if your output feeds a vector store rather than a database. Scrapy and Crawlee cost nothing in licence fees and everything in engineering time, and Crawlee is the same SDK Apify builds on, so a Crawlee migration keeps your code.

Published entry prices for these tools disagree across sources, often because one is annual and one is monthly, or because a page has not been updated. The numbers above are the ones I could tie to a dated check.

## Which one to pick

- **You have a parser, the site blocks you, nothing else is broken.** ScraperAPI Hobby at $49. Check your real credit cost per URL first, since a JS-rendered Amazon page is 15 credits rather than 1.
- **You want nothing to do with code.** Octoparse at $69/mo annual, or stay on Apify and use its Store Actors. ScraperAPI is the wrong tool here.
- **You need a large owned proxy network and contractual delivery.** Bright Data or Oxylabs, both priced by usage with enterprise support attached.
- **Your output is going into a RAG pipeline or an AI agent.** Firecrawl's Markdown output saves a parsing step that ScraperAPI will not do for you.
- **You want zero vendor lock-in and have the engineering time.** Scrapy or Crawlee, both free.
- **You want someone else to own the whole pipeline.** Zyte, whose commitments start around $100/mo, or a fully managed provider with accuracy and delivery SLAs. ScraperAPI sits below that line: it unblocks requests, it does not guarantee a dataset.

## FAQ

**Is ScraperAPI cheaper than Apify?**
The entry prices point in opposite directions. Apify Starter is $19/mo for the platform, before Actor and proxy usage; ScraperAPI Hobby is $49/mo covering 100,000 credits. For a small job on a single site with no rendering, Apify can come out cheaper. Once you are running frequent jobs against protected targets and paying both per-result Actor fees and compute units, flat credits usually win on predictability. Run your own numbers on 100,000 pages of your actual target.

**Does the free trial require a credit card?**
No. The trial gives you 5,000 credits across 7 days without a card. Afterwards you drop to the free plan with 1,000 credits and 5 concurrent threads, which is enough to keep a small monitor alive.

**Can it scrape JavaScript-rendered pages?**
Yes, with `render=true`, at 10 extra credits per request on top of the base cost. Combined with premium proxies the published rate is 25 credits, and premium plus rendering is priced at 75. Some sites need rendering and bypass together; the Domain Cost Estimator gives you the exact figure before you commit.

**Are failed requests billed?**
The model is per successful request, and a request refused for exceeding your concurrency limit returns a 429 without a charge. What you should still watch is the bypass surcharge: it fires automatically when ScraperAPI activates bypass logic, so harder targets consume credits faster even when the request succeeds.

**What happens when credits run out mid-month?**
On Hobby, Startup and Business, scraping pauses until your renewal date unless you enable auto-upgrade to the next plan. On Scaling and above you can turn on pay-as-you-go at a fixed per-credit rate, capped at a monthly limit you set, so a surprise bill is not possible unless you raise the cap yourself.

## Before you order

Two things to settle first. Price your ten most important URLs with the Domain Cost Estimator, because the $49 Hobby plan covers 100,000 standard pages but only 4,000 Google SERPs, and the gap decides whether you need Startup. Second, decide between monthly and annual deliberately: annual saves exactly 10% and delivers the year's credits upfront, but the credits expire with the billing period, so an annual plan only pays off if your monthly volume is steady.

If both answers point to the developer-with-a-parser case, the entry tier is enough to test the success rate on your hardest targets, and the 7-day refund means a bad fit costs you a support ticket rather than a month's fee.
👉 [Compare all ScraperAPI plans and start the free trial](https://www.scraperapi.com/pricing/?fp_ref=coupons)
