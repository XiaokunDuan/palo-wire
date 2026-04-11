# Palo Wire

<p align="center">
  <strong>Palo Wire</strong> is an agent-native source layer for Silicon Valley intelligence.
  It continuously refreshes a curated set of high-signal public sources and exposes lightweight JSON documents that downstream agents can read, rank, summarize, and synthesize.
</p>

<p align="center">
  <a href="https://silicon.yulu34.top">Live Site</a>
  ·
  <a href="https://silicon.yulu34.top/api/documents">Documents API</a>
  ·
  <a href="https://silicon.yulu34.top/api/sources">Source Registry</a>
  ·
  <a href="#quickstart">Quickstart</a>
  ·
  <a href="#roadmap">Roadmap</a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/TypeScript-111827?style=flat&logo=typescript&logoColor=3178c6" alt="TypeScript" />
  <img src="https://img.shields.io/badge/Cloudflare_Workers-111827?style=flat&logo=cloudflare&logoColor=f38020" alt="Cloudflare Workers" />
  <img src="https://img.shields.io/badge/Workers_KV-111827?style=flat&logo=cloudflare&logoColor=f38020" alt="Workers KV" />
  <img src="https://img.shields.io/badge/JSON_API-111827?style=flat" alt="JSON API" />
  <img src="https://img.shields.io/badge/Scheduled_Ingestion-111827?style=flat" alt="Scheduled ingestion" />
</p>

## Why Palo Wire

Most trend-tracking products are built for people to browse.

Palo Wire is built for systems that need a clean, repeatable source layer. Instead of asking every downstream agent to rediscover the same feeds, pages, podcasts, and launch sources, Palo Wire keeps a small curated graph of public signals fresh and machine-readable.

That makes it useful for workflows such as:

- daily Silicon Valley signal monitoring
- source-grounded agent research
- lightweight startup, product, and VC briefing pipelines
- downstream ranking, summarization, and synthesis tasks

## Product Shape

Palo Wire is not a traditional media product.

It is a continuously refreshed source node that:

1. reads a curated source registry
2. ingests sources using the most stable available public interface
3. normalizes results into lightweight documents
4. stores the latest snapshot per source
5. exposes minimal APIs for downstream agents

In one line:

`Palo Wire = a rolling, high-signal document layer for AI systems watching Silicon Valley.`

## Live Access

- Landing page: [https://silicon.yulu34.top](https://silicon.yulu34.top)
- Global documents feed: [https://silicon.yulu34.top/api/documents](https://silicon.yulu34.top/api/documents)
- Source registry: [https://silicon.yulu34.top/api/sources](https://silicon.yulu34.top/api/sources)
- Worker preview: [https://palo-wire.ylu665485.workers.dev](https://palo-wire.ylu665485.workers.dev)

If you are a human, start with the landing page.

If you are an agent, start with:

- `/api/sources`
- `/api/documents`
- `/api/sources/:id/documents`
- `/api/runs/latest`

## Design Principles

- `Agent-first`: optimize for downstream model consumption
- `Official-entry-first`: prefer feeds, sitemaps, APIs, and structured endpoints over brittle scraping
- `High-signal only`: fewer sources, better sources
- `Minimal schema`: keep documents cheap to ingest downstream
- `Rolling freshness`: preserve the last good snapshot for low-frequency publishers
- `Operational restraint`: fit inside the practical limits of Workers and KV

## Coverage

### Tech

- Hacker News
- Product Hunt
- Y Combinator Launches
- TechCrunch
- Lenny's Newsletter
- Lenny's Podcast
- Latent Space
- First Round Review
- Y Combinator Blog

### VC

- Crunchbase News
- a16z
- a16z Podcast Network
- Sequoia
- Lightspeed
- NFX
- Benchmark

## Ingestion Strategy

Palo Wire does not treat every source the same.

Each source is assigned an explicit ingestion mode:

- `rss_feed` for stable public feeds
- `xml_sitemap` for publisher-managed sitemap indexes
- `official_api` when a vendor API is more stable than HTML
- `page_data` for application shells with structured payloads
- `manual_curated` for sources that need explicit curation

## Public Interface

### Root

- `GET /`

Human-facing landing page.

### Source Registry

- `GET /api/sources`
- `GET /api/sources/:id`

Source metadata plus latest snapshot summary.

### Documents

- `GET /api/documents`
- `GET /api/sources/:id/documents`

Normalized `article` and `podcast` documents.

### Links

- `GET /api/sources/:id/links`

Outbound links extracted from the latest source snapshot.

### Operations

- `GET /api/runs/latest`
- `POST /api/sync`

Operational status and manual sync entry point.

## Repository Layout

```text
src/                    Worker entry point, routing, sync logic
sources/                Curated source registry
docs/                   API and architecture notes
scripts/                Local support scripts
wrangler.jsonc          Cloudflare Worker configuration
```

## Quickstart

Install dependencies:

```bash
npm install
```

Run locally:

```bash
npm run dev
```

Type-check:

```bash
npx tsc --noEmit
```

Deploy:

```bash
npm run deploy
```

## Runtime Requirements

- Cloudflare Workers
- Workers KV
- scheduled triggers
- source registry configuration
- optional authenticated sync trigger for `POST /api/sync`

## Documentation

- API reference: [docs/api.md](./docs/api.md)
- Architecture notes: [docs/architecture.md](./docs/architecture.md)
- Worker config: [wrangler.jsonc](./wrangler.jsonc)
- Source registry: [sources/registry.json](./sources/registry.json)

## Roadmap

- Add more source-specific ingest handlers where structured endpoints exist
- Improve normalized signal extraction on top of raw snapshots
- Expand operational visibility for crawl failures and source freshness
- Add clearer public changelog and source coverage notes
- Tighten downstream agent examples and starter clients
