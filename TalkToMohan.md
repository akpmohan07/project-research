https://claude.ai/chat/76646b9d-eb52-4c19-b005-aad133b67671

# Talk to Me — Hackathon Idea Doc
> Daytona x Give(a)Go HackSprint Dublin | 28 March 2026

---

## One-line pitch

A live chat UI where anyone can ask questions about you — answered in real time by parallel Daytona sandboxes fetching your actual public data.

---

## The problem

A CV is static, generic, and ignored. Recruiters spend 30 seconds on it. Collaborators don't know how you work. Investors can't tell if you can ship. There's no good way for the world to *actually* get to know you.

---

## The solution

**"Talk to Me"** — your personal API for the world.

A chat interface backed by your real public data. Every question spins isolated Daytona sandboxes that fetch live data on demand, feed it to an LLM, and respond *as you*.

---

## How it works

```
User asks a question
        ↓
Orchestrator decides which data sources are relevant
        ↓
Parallel Daytona sandboxes spin up (sub-90ms each)
    Sandbox 1 → GitHub API       (code, repos, activity)
    Sandbox 2 → Spotify API      (music, taste, mood)
    Sandbox 3 → Google Calendar  (availability, priorities)
    Sandbox 4 → Resume PDF       (career, skills, story)
    Sandbox 5 → Blog / posts     (opinions, personality)
        ↓
All results aggregated
        ↓
Claude synthesises → responds as Mohan
        ↓
Live chat UI displays answer
```

---

## Why Daytona is the right tool

| Without Daytona | With Daytona |
|---|---|
| Pre-load all data into a vector DB (stale) | Fetch live on every question (always current) |
| Single process, sequential fetches | Parallel isolated sandboxes, simultaneous |
| Data sources bleed into each other | Each sandbox is fully isolated |
| Slow cold start | Sub-90ms sandbox spin-up |

The **isolation per data source** is the key insight — each API call runs in its own sandbox, so a Spotify token never touches a GitHub call. Secure and parallelised by design.

---

## Data sources

| Source | What it reveals | Auth complexity |
|---|---|---|
| GitHub (public API) | Developer identity, activity, languages | None — public |
| Resume PDF | Career story, skills, experience | None — just a file |
| Spotify API | Music taste, mood, personality | OAuth — quick setup |
| Google Calendar | How you spend time, priorities | OAuth — have credentials |
| Blog / public posts | Opinions, writing style | Scrape or RSS |
| LinkedIn (public) | Professional narrative | Public scrape |

**MVP for today:** GitHub + Resume PDF + Spotify = enough for a compelling demo.

---

## Target users

| User | What they want to know | Value |
|---|---|---|
| **Recruiter** | Can Mohan do the job? Is he a fit? | Highest — replaces the CV |
| **Collaborator** | How does Mohan work? What's his style? | High — replaces the intro call |
| **Investor / Baseline** | Can Mohan ship? Does he have founder instincts? | High — relevant today |
| **Friend** | What's Mohan into? What's he up to? | Fun — personality layer |
| **Stranger** | Who is this person? Are they interesting? | Broad — portfolio use case |

---

## The bigger vision

This stops being about Mohan and becomes a **product anyone can deploy for themselves.**

> "Talk to [anyone]" — a platform where you connect your accounts, and the world gets a live, intelligent interface to your digital identity.

This is the pitch to Baseline: not a personal toy, but a new primitive for how people present themselves online.

---

## Demo script (for judges)

1. Open the chat UI
2. Ask: *"What kind of developer is Mohan?"* → GitHub + Resume sandboxes fire → answer
3. Ask: *"What does Mohan listen to when he codes?"* → Spotify sandbox fires → answer
4. Ask: *"Is Mohan free this weekend?"* → Calendar sandbox fires → answer
5. Show the terminal — parallel sandbox logs firing simultaneously
6. Show timing: parallel vs sequential comparison

---

## Build plan for today

### Phase 1 — Core (12:00–2:00 PM)
- [ ] Daytona async sandbox setup
- [ ] GitHub data fetcher sandbox
- [ ] Resume PDF parser sandbox
- [ ] Basic orchestrator that routes questions to right sandboxes
- [ ] Claude synthesis layer

### Phase 2 — Polish (2:00–4:00 PM)
- [ ] Spotify sandbox
- [ ] Simple chat UI (Streamlit or plain HTML)
- [ ] Parallel timing display

### Phase 3 — Demo prep (4:00–4:45 PM)
- [ ] Test all demo questions
- [ ] Clean up output formatting
- [ ] Prepare 2-min pitch

---

## Stack

```
Python 3.11+
daytona          — sandbox orchestration
anthropic        — Claude for synthesis
python-dotenv    — API key management
requests         — API calls inside sandboxes
streamlit        — chat UI (fast to build)
PyPDF2           — resume parsing
```

---

## Repo

- Group project used for testing: https://github.com/akpmohan07/group4-safeflight-project
- Hackathon repo: TBD

---

*Ideated at Daytona x Give(a)Go HackSprint Dublin, 28 March 2026*
