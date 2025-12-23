Here is a **clean, self-contained Markdown (`.md`) document** you can drop into a repo (e.g. `README.md` or `PROJECT_OVERVIEW.md`).
It is written to **freeze the idea clearly**, so you can continue later without losing intent or scope.

---

````md
# Semantic Video Timeline Format (Working Title)

## Overview

This project explores the creation of a **new open data format** for describing **what happens in a video over time**, beyond dialogue-based subtitles.

The goal is to define a **lightweight, structured, time-aware format** (similar in spirit to `.srt`) that can capture **semantic information** such as:

- Actors present
- Locations
- Actions and events
- Objects
- Emotions or states
- Optional frame-level precision

The format is designed to be **human-readable**, **machine-friendly**, and **tool-agnostic**.

---

## Motivation

Existing subtitle formats (SRT, WebVTT) focus only on **spoken text**.  
Professional metadata standards (e.g. MPEG-7, AAF) are **too complex**, heavy, or impractical for modern workflows.  
AI annotation tools and datasets define **ad-hoc schemas** that are not interoperable.

There is currently **no simple, open, portable standard** to answer:

> “At this moment in the video, who is present, where are we, and what is happening?”

This project aims to fill that gap.

---

## Core Idea

Create a **semantic timeline layer** that sits alongside video, similar to subtitles, but structured and extensible.

Key principles:
- Time is the primary axis
- Meaning is attached to time
- Structure over free text
- Minimal core, extensible design
- Open and versioned

---

## Intended Use Cases

### Primary
- AI / ML video understanding datasets
- Accessibility (scene-aware audio descriptions)
- Video analytics and search

### Secondary
- Media archives
- Post-production metadata
- Education and training content
- Research and annotation tooling

---

## Design Goals

- **Simple**: Easy to read, write, and diff
- **Flexible**: Support time ranges and frame-level precision
- **Structured**: Clear fields for actors, actions, locations
- **Extensible**: Allow future metadata without breaking compatibility
- **Tool-neutral**: Not tied to any editor, platform, or vendor

---

## Non-Goals

- Not a replacement for video containers
- Not a full ontology or knowledge graph
- Not editor-specific metadata
- Not a proprietary annotation system

---

## Format Characteristics (Draft)

- File format: JSON (or JSON Lines for large/frame-level data)
- Versioned schema
- Time-based entries using:
  - `start` / `end` timestamps, or
  - exact `frame` numbers with declared FPS
- Minimal required fields:
  - time reference
  - semantic content (actors, actions, location)

---

## Example (Illustrative)

```json
{
  "format": "SMD",
  "version": "0.1",
  "video": { "fps": 24 },
  "entries": [
    {
      "start": "00:01:12.000",
      "end": "00:01:15.500",
      "location": "Hospital - ER",
      "actors": ["Dr. Miller", "Patient"],
      "actions": ["examining patient", "monitor beeping"]
    }
  ]
}
````

This example is illustrative, not final.

---

## Relationship to Existing Work

This project is conceptually related to:

* Subtitle formats (SRT, WebVTT)
* Video annotation schemas used in AI datasets
* Academic multimedia description standards (e.g. MPEG-7)

However, it deliberately avoids:

* Heavy XML-based ontologies
* Tool-specific or proprietary schemas
* Over-standardization at early stages

---

## Adoption Strategy

The project is intended to grow as:

1. An open specification
2. A small set of reference tools (validator, viewer)
3. A practical demo use case
4. Gradual adoption through usefulness, not formal mandates

---

## Risks & Open Questions

* Scope creep and over-complexity
* Fragmentation via incompatible extensions
* Lack of a strong initial use case
* Balancing human readability with machine precision

These will be addressed by:

* Keeping a strict minimal core
* Versioning and extension namespaces
* Anchoring early versions to a single domain

---

## Current Status

* Conceptual design phase
* Competitive and landscape analysis ongoing
* No finalized schema yet

---

## Next Steps (Future Work)

* Define v0.1 minimal schema
* Write formal JSON Schema
* Build validator CLI
* Create simple video overlay viewer
* Test against a real dataset or accessibility scenario

---

## License / Openness

Intended to be:

* Open specification
* Open-source reference tools
* Vendor-neutral

License to be decided.

---

## Notes

This document captures the **intent and direction** of the project at an early stage.
Details are expected to evolve, but the core problem and philosophy should remain stable.


