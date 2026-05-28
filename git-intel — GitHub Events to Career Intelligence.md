https://claude.ai/chat/65b25ca8-8a53-4fdd-a8d0-d297e8cb994f

# git-intel — GitHub Events to Career Intelligence

> A multi-agent system that autonomously watches 3.5 million daily GitHub events, investigates anomalies, detects emerging patterns, and builds an ever-growing intelligence base — answering career questions grounded in real evidence.

**GitHub:** [github.com/akpmohan07/git-intel](https://github.com/akpmohan07/git-intel)

---

## The Problem

Every day, millions of engineers push code, star repos, fork projects, and ship releases on GitHub. This collective activity is the clearest signal of what the engineering world is actually building — not what people are writing about, not what's being hyped, but what is actually happening.

The problem: nobody synthesises this signal for you.

Existing tools fail in two ways:

- **Generic tools** (Changelog Nightly, OSSInsight) show what's trending globally — not what's relevant to your specific stack
- **AI assistants** (GitHub Copilot, ChatGPT) hallucinate specific numbers when asked about current trends because they don't have a real pipeline processing actual GitHub data

The gap: a system that processes real GitHub events and answers one question grounded in evidence:

> *"What should a backend engineer know this week, based on what 3.5 million engineers actually committed, starred, and built?"*

---

## The Data

**Source:** [GH Archive](https://gharchive.org) — complete public GitHub event stream, updated hourly, free.

**Scale:**
- 3,546,395 events per day
- ~155,000 events per hour
- ~2.5GB uncompressed per day
- 15 years of historical data available

**Event types available:**

| Event | Volume/day | Signal value |
|-------|-----------|--------------|
| PushEvent | 2,869,345 | Low — noise |
| CreateEvent | 348,889 | High — repo descriptions |
| WatchEvent | 18,079 | High — trending signal |
| ForkEvent | 4,406 | Very high — usage signal |
| ReleaseEvent | 4,163 | Highest — actionable |
| PullRequestEvent | 77,353 | High — PR titles |
| IssuesEvent | 19,182 | High — problem detection |

**Signal events after filtering: ~375,537/day (10.6% of total)**

---

## Architecture

### Overview

```
GH Archive (hourly files)
        ↓
Ingestion Agent
        ↓
Kafka — "gh-events-raw" topic
        ↓
Kafka Streams (filter + aggregate)
        ↓
Kafka — "gh-events-signal" topic
        ↓
PostgreSQL + pgvector
        ↓
Investigation / Pattern / Career Agents
        ↓
LLM (Claude API)
        ↓
Intelligence insights stored as vectors
        ↓
Query Agent (user facing)
```

### The Multi-Agent System

The project is built as a multi-agent system — each agent has one focused job and operates autonomously.

---

#### Agent 1 — Ingestion Agent
**Job:** Watch for new GH Archive files every hour. Download, decompress, parse, push signal events to PostgreSQL.

**Triggers:** Scheduled — every hour

**Tools:**
- `download_archive(hour, date)`
- `parse_events(file)`
- `filter_signal_events(events)`
- `store_events(events)`

---

#### Agent 2 — Investigation Agent
**Job:** Look at fresh data and autonomously decide what is worth investigating deeper. No pre-built queries — the agent reasons about what matters.

**Triggers:** After Ingestion Agent completes

**Tools:**
- `query_top_repos(hours=1)`
- `get_repo_velocity(repo, days=7)`
- `find_related_repos(keyword)`
- `compare_this_week_vs_last(repo)`

**Example reasoning:**
```
"LangChain4j spiked 340% — let me check for a release"
→ queries ReleaseEvent for langchain4j
→ "v1.1.0 released 2 hours ago"
→ "Let me check if new repos reference it"
→ "23 new repos in 2 hours — significant"
→ stores insight
```

---

#### Agent 3 — Pattern Agent
**Job:** Find non-obvious connections across repos and events. Detect emerging technology combinations before they become mainstream.

**Triggers:** Daily

**Tools:**
- `cluster_descriptions(date)`
- `find_cooccurrence(tech1, tech2)`
- `detect_emerging_combinations()`
- `compare_language_trends()`

**Example output:**
```
"Kafka + pgvector appearing together in 18 repos 
 this week — new architectural pattern emerging"
```

---

#### Agent 4 — Career Intelligence Agent
**Job:** Translate GitHub signals into career-specific, actionable advice for backend engineers.

**Triggers:** Daily or on demand

**Tools:**
- `search_insights(query)`
- `get_job_relevant_trends()`
- `compare_skill_demand(skill, weeks=4)`
- `get_release_summaries()`

**Example output:**
```
LEARN THIS WEEK:
  LangChain4j + Kafka integration pattern —
  23 independent repos built this in 48 hours.
  This will be in job descriptions in 90 days.

ADD TO CV:
  "Built async LLM processing pipeline using 
   Kafka consumer groups" — this exact pattern 
   is appearing in 23 new repos this week.

TALK ABOUT IN INTERVIEWS:
  "Kafka + LLM enrichment is becoming a standard
   architectural pattern — I've been tracking 
   this emerge in real time on GitHub."
```

---

#### Agent 5 — Alert Agent
**Job:** Detect anomalies and urgent signals. Notify immediately without waiting for the daily digest.

**Triggers:** Every 15 minutes

**Tools:**
- `detect_spike(threshold=300%)`
- `detect_major_release()`
- `detect_security_issue()`
- `send_alert(message)`

---

#### Agent 6 — Memory Agent
**Job:** Maintain long-term intelligence. Connect today's events to historical patterns. Build a timeline of how the ecosystem evolves.

**Triggers:** Weekly

**Tools:**
- `search_historical_insights(query)`
- `build_trend_timeline(topic, months=3)`
- `detect_cycle_patterns()`
- `summarise_evolution(topic)`

---

#### Agent 7 — Query Agent (user facing)
**Job:** Answer user questions using all accumulated intelligence. The only agent the user interacts with directly.

**Triggers:** On demand

**Example queries it handles:**
```
"What's happening with Kafka this week?"
"What Java tools are engineers using for AI?"
"Is Spring AI gaining or losing traction?"
"What should I learn this month?"
"What are Dublin companies building?"
```

---

### Why RAG + Vector Search

The system uses **Retrieval Augmented Generation (RAG)** — ensuring every answer is grounded in real GitHub data, not hallucinated.

**The problem with LLMs answering GitHub questions directly:**

GitHub Copilot, when asked "What's happening with Kafka this week?", responded:

> *"I'm unable to provide precise real-time GitHub metrics due to current API/search limitations"*

...then proceeded to invent specific star counts and repo names that don't exist.

**How git-intel solves this:**

```
User: "What's happening with Kafka this week?"
        ↓
Embed question → vector
        ↓
pgvector similarity search across stored insights
        ↓
Retrieve top 20 most relevant real datapoints:
  - "apache/kafka: 1,203 WatchEvents on May 12"
  - "Kafka 4.2.0 released — virtual threads stable"
  - "23 repos combined Kafka + LLM this week"
        ↓
LLM answers using only retrieved evidence
        ↓
Grounded, specific, verifiable answer
```

**No hallucination. Real numbers. Real dates. Real events.**

---

## Tech Stack

| Layer | Technology | Why |
|-------|-----------|-----|
| Language | Java 21 | Virtual threads, production-grade |
| Framework | Spring Boot 3.4 | Familiar, production-ready |
| AI framework | Spring AI | Embeddings + vector search in Java |
| Event streaming | Apache Kafka | Reliable ingestion, replay capability |
| Stream processing | Kafka Streams | Real-time filtering + windowing |
| Database | PostgreSQL 16 | Relational + vector in one |
| Vector search | pgvector | Semantic similarity, no extra DB |
| Embeddings | Ollama (local) | Free, runs locally |
| LLM | Claude API | Insight generation |
| Build tool | Gradle | Faster, cleaner syntax |

---

## Data Flow in Detail

### Stage 1 — Ingestion
```
GH Archive drops hourly file: 2026-05-16-14.json.gz
  ↓ ~22MB compressed, ~108MB decompressed
Java reads line by line (155,313 lines)
  ↓
Filter: keep WatchEvent, ForkEvent, ReleaseEvent, CreateEvent
  ↓ ~30,000 events/hour pass filter
Produce to Kafka topic "gh-events-raw"
```

### Stage 2 — Stream Processing
```
Kafka Streams consumes "gh-events-raw"
  ↓
Extract fields: repo name, description, PR title, 
                release body, branch name
  ↓
Apply keyword filter: Java, Kafka, Spring, AI, LLM...
  ↓ ~5,000 events/hour
Aggregate: top repos by stars, forks, releases
  ↓
Produce to "gh-events-signal"
```

### Stage 3 — Storage + Embedding
```
Consumer reads "gh-events-signal"
  ↓
Store raw event in PostgreSQL
  ↓
Build text representation:
  "WatchEvent apache/kafka distributed streaming 
   Java platform 1203 stars May 2026"
  ↓
Embedding model → vector [0.23, 0.87, 0.12, ...]
  ↓
Store vector in pgvector
```

### Stage 4 — Agent Investigation
```
Investigation Agent wakes up hourly
  ↓
Queries PostgreSQL for anomalies
  ↓
Reasons about what is interesting
  ↓
Runs follow-up queries autonomously
  ↓
Generates structured insight:
{
  "type": "SPIKE_DETECTED",
  "repo": "langchain4j/langchain4j",
  "signal": "340% above 7-day average",
  "insight": "LangChain4j spiking post v1.1.0 release",
  "evidence": "1,876 stars, 456 forks in 24 hours",
  "generated_at": "2026-05-16T14:00:00Z"
}
  ↓
Embed insight → store in pgvector
```

### Stage 5 — Query + Answer
```
User: "What Java AI libraries should I learn?"
  ↓
Embed question → vector
  ↓
pgvector: find top 20 similar insights
  ↓
Build context from real evidence
  ↓
Claude API generates grounded answer
  ↓
"Based on this week's GitHub activity:
 LangChain4j received 1,876 stars and 456 forks
 following its v1.1.0 release. 23 independent 
 repos built Kafka + LangChain4j pipelines this 
 week — this pattern is crystallising fast..."
```

---

## Signals the System Detects

### From WatchEvent — Trending signal
- Repos getting starred faster than baseline
- New repos getting starred immediately
- Stack-specific repos gaining attention

### From ForkEvent — Usage signal
- High fork-to-star ratio = practical adoption
- New repos forked immediately = strong early signal

### From ReleaseEvent — Update signal
- Major releases in your stack
- Breaking changes to know about
- Safe upgrade signals

### From CreateEvent — Emerging pattern signal
- New repo descriptions reveal what engineers are starting to build
- Technology combinations appearing in names
- Clusters of similar repos = pattern crystallising

### From PullRequestEvent — Problem/solution signal
- PR titles reveal what engineers are actively solving
- Merged PRs = shipped solutions
- Label patterns = trending problem categories

### Cross-event correlations
- Same repo across multiple event types = significant event
- Technology appearing in unrelated repos simultaneously = emerging standard
- Issue spike followed by PR spike = active community problem solving

---

## Build Phases

### Phase 1 — Data Foundation (Week 1)
- [x] Repo created
- [x] Spring Boot project set up
- [ ] GH Archive file reader (Java + Jackson)
- [ ] Signal event filter
- [ ] Store events in PostgreSQL

### Phase 2 — Vector Layer (Week 2)
- [ ] pgvector extension in PostgreSQL
- [ ] Ollama set up locally
- [ ] Embed each signal event
- [ ] Similarity search working

### Phase 3 — Agent Foundation (Week 3)
- [ ] Ingestion Agent (scheduled)
- [ ] Investigation Agent (autonomous queries)
- [ ] Query Agent (user facing)

### Phase 4 — Intelligence Layer (Week 4)
- [ ] Pattern Agent
- [ ] Career Intelligence Agent
- [ ] Alert Agent

### Phase 5 — Memory + Polish (Week 5+)
- [ ] Memory Agent (long-term patterns)
- [ ] Kafka integration
- [ ] Production hardening

---

## Why This Is Different

| Tool | What it does | What it misses |
|------|-------------|----------------|
| OSSInsight | Generic GitHub analytics | No personalisation, no career angle |
| Changelog Nightly | Daily trending repos email | No LLM synthesis, no career intelligence |
| GitHub Copilot | Answers GitHub questions | Hallucinates — no real data pipeline |
| git-intel | Evidence-based career intelligence | — |

**The core differentiator:**

> Every insight is grounded in real, timestamped GitHub events. No hallucination. Verifiable. Specific to your stack. Continuously updated.

---

## Design Decisions — What We Tried and Why

Every architectural decision in this project was arrived at through exploration and deliberate reasoning. This section documents the journey.

---

### Decision 1 — Data Source: GH Archive over GitHub REST API

**What we tried:** GitHub REST API (`api.github.com/events`) for real-time polling.

**The problem:**
- Only returns last 300 events per poll
- At peak GitHub generates 1,000-2,000 events/minute — window fills in 10-15 seconds
- Unauthenticated rate limit: 60 requests/hour — not enough
- Even with auth token (5,000/hour) — events still fall off the window permanently

**Decision:** Use GH Archive instead.
- Complete hourly dumps — zero gaps, zero missed events
- Free, no auth needed, no rate limits
- Same data OSSInsight uses — proven at scale
- One day = 3,546,395 events in 24 files

**Lesson:** Real-time API polling is the wrong tool for completeness. Batch files give you everything.

---

### Decision 2 — Start Local, Then BigQuery

**What we tried:** BigQuery first for exploration (GH Archive is a public dataset there).

**The problem:** BigQuery table `githubarchive.day.20260512` returned no data — likely a lag or naming issue.

**Decision:** Download files locally first, validate the data, then use BigQuery for historical queries later.

**Why this was right:** Exploration on local files is free, fast, and doesn't burn through the 1TB free BigQuery quota while still figuring out what queries you need.

**Lesson:** Validate data locally before investing in cloud infrastructure.

---

### Decision 3 — PostgreSQL over Specialised Databases

**What we evaluated:**

| Database | Considered | Decision |
|----------|-----------|----------|
| PostgreSQL | Primary choice | Yes — relational + pgvector in one |
| TimescaleDB | Time-series extension | Later — when query performance degrades |
| ClickHouse | Columnar analytics | Later — if historical analysis needed |
| ScyllaDB | High write throughput | No — overkill at 40 events/second |
| BigQuery | Managed warehouse | Later — for multi-year historical queries |

**Why PostgreSQL won for now:**
- 40 events/second is trivially handled
- pgvector extension adds vector search without extra infrastructure
- Single database for both relational queries and semantic search
- ScyllaDB and ClickHouse become relevant at 100K+ writes/second — not our scale

**Lesson:** Match database choice to actual scale, not aspirational scale. Senior engineers explain why they chose something, not just what they chose.

---

### Decision 4 — Kafka for Transport (Despite Not Needing It Yet)

**What we considered:** Skip Kafka entirely — just read files directly into PostgreSQL.

**Why we kept Kafka:**
- Decouples ingestion from processing — file reader doesn't need to know about downstream consumers
- Replay capability — if the LLM layer fails at hour 14, reprocess from hour 14
- Multiple consumers — Investigation Agent, Pattern Agent, Alert Agent can all consume independently
- Directly relevant to existing Freshworks experience and Apache Kafka contribution goal
- The learning value justifies the complexity at this stage

**What we rejected:** Apache Spark — overkill at 3.5M events/day, only becomes relevant at 100GB+/day.

**Lesson:** Add complexity when it earns its place — Kafka earns its place here through replay and decoupling, not scale.

---

### Decision 5 — RAG over Direct LLM Queries

**What we tried:** Ask GitHub Copilot directly: "What's happening with Kafka this week?"

**What happened:** Copilot first gave generic advice that could have been written without any GitHub data. When pushed for specifics, it admitted it lacked real-time access — then invented specific star counts, fork velocities, and repo names that don't exist.

**This validated the entire project.**

**Decision:** Build a real pipeline. Store actual GitHub events. Use RAG — retrieve real datapoints, feed to LLM as grounded context.

**Why RAG over loading all data to LLM:**
- One day of signal events = ~187MB of text
- Claude context window = ~1MB
- Can't fit — and even if you could, LLMs are poor at counting/aggregating millions of rows
- Right division of labour: SQL aggregates, LLM interprets

**Lesson:** LLMs are not databases. Use each tool for what it is good at.

---

### Decision 6 — Proactive Agents over Pure Search

**What we considered:** Pure search system — user asks question, system retrieves and answers.

**The problem:** Pre-built queries and pure search both require you to know what to ask. They miss patterns nobody anticipated.

**Decision:** Autonomous agents that decide what is interesting without being asked.

**The insight:** GitHub Copilot has direct GitHub access but gives generic answers because it lacks a reasoning layer that decides what matters. Our Investigation Agent fills this gap — it doesn't wait to be asked, it investigates autonomously and stores what it finds.

**Result:** A system that builds its own intelligence base over time. The longer it runs, the smarter it gets.

**Lesson:** The most valuable intelligence is often the pattern nobody thought to ask about.

---

### Decision 7 — Multi-Agent over Monolithic Pipeline

**What we considered:** One large pipeline — ingest, process, synthesise, serve.

**Why multi-agent:**
- Each agent has one focused job — easier to test, debug, improve independently
- Agents run on different schedules (hourly, daily, weekly, on-demand)
- New agents can be added without touching existing ones
- Directly relevant to the Lyzr AI Agentic Architect Hackathon theme

**The agents and their separation of concerns:**

```
Ingestion Agent    — data collection (hourly)
Investigation Agent — anomaly detection (hourly)
Pattern Agent      — cross-repo connections (daily)
Career Agent       — career interpretation (daily)
Alert Agent        — urgent signals (every 15 min)
Memory Agent       — long-term patterns (weekly)
Query Agent        — user interface (on demand)
```

**Lesson:** Separation of concerns applies to agents just as it applies to microservices.

---

### Decision 8 — Filter Everything Before LLM

**What we considered:** Feed all 3.5M events directly to LLM to find patterns.

**The math problem:**
```
3.5M events × 500 bytes = 1.75GB of text
Claude context window = ~1MB
Required API calls = 1,750
Cost = impractical
Quality = poor (LLMs are bad at counting)
```

**Decision:** Four-stage filtering before LLM ever sees data:

```
Stage 1: Event type filter → discard 89% (PushEvent noise)
Stage 2: Bot filter → discard bots
Stage 3: Keyword filter → keep Java/Kafka/AI ecosystem only
Stage 4: Aggregation → SQL counts and patterns
↓
LLM sees: ~500 words of structured summary
```

**Lesson:** The most important engineering in an AI pipeline is often what you filter out, not what you feed in.

---

### What We Rejected and Why

| Idea | Why rejected |
|------|-------------|
| HackerNews as primary data source | Already done well by many tools. GH Archive is richer and less processed. |
| AI news aggregator | Crowded space — Particle, Feedly, TLDR Newsletter all exist. |
| Database benchmark project | Valid project but separate from the intelligence pipeline. Scope creep. |
| Filtering pipeline to Java only | Too narrow. Process everything, filter at query time. |
| Daily briefing without search | Static output. Search-based RAG is more flexible and more useful. |
| Commit messages as signal | Not available in GH Archive — stripped out. Branch names and PR titles are the available text signals. |

---

## Interview Story

> "I built git-intel — a multi-agent system that processes 3.5 million daily GitHub events from GH Archive through a Kafka pipeline, stores them in PostgreSQL with pgvector for semantic search, and uses autonomous agents to investigate anomalies and generate career intelligence. The system answers questions like 'what should I learn this week' with evidence from real GitHub activity — not hallucinated advice. I built it because I noticed GitHub Copilot hallucinates specific star counts and repo names when asked about current trends. My pipeline uses actual data."

---

*Built by Mohan — Senior Software Engineer, Dublin*
*MSc Computing, Dublin City University*
*github.com/akpmohan07/git-intel*
