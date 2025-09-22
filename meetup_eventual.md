
---

# **Project Brief: Meetup Networking Companion App**

## 1️⃣ Problem Statement

Attending tech meetups often comes with the following pain points:

**For Participants:**

* Hard to meet people with similar interests.
* Real-time content sharing (slides, links, resources) is clunky — often requires QR scanning or typing URLs.
* Pressure to take photos or notes instead of focusing on the speaker.
* LinkedIn or collected contacts lack context → hard to recall people later.

**For Presenters:**

* Struggle to share slides quickly.
* Difficult to engage audience with real-time polls or questions.

**General Event Pain Points:**

* Post-event follow-ups are manual and inefficient.
* Data and connections are fragmented and short-lived.

---

## 2️⃣ Proposed Solution

A **self-hosted, laptop-based local-network MVP**:

**Key Features (MVP):**

* Attendees join via QR code on the local network.
* Lightweight attendee profiles (name, role, interests).
* Real-time contact exchange (one-tap or QR fallback).
* Presenter slides broadcast to all attendees.
* Notes can be taken and linked to attendees or slides.
* Local storage (SQLite/JSON) to keep event data offline.
* Optional cloud sync or export after event.

**Advanced Features for Future Versions:**

* Polls, Q\&A, analytics dashboard.
* NFC “bump” contact exchange.
* AI-assisted notes and follow-up reminders.
* Cloud backup and cross-event history.

---

## 3️⃣ Learning Opportunities

By building this project, contributors can gain experience in:

* **Backend Development:** Node.js/Express, WebSocket (Socket.IO), SQLite or JSON data management.
* **Frontend Development:** React/Vue, PWA, responsive UI, QR code integration.
* **Networking Concepts:** LAN-only apps, WebSocket real-time communication, local network security.
* **Security & Privacy:** Authentication, LAN isolation, secure data handling.
* **Collaboration & Project Management:** GitHub workflow, issue tracking, sprint planning.
* **UX Design:** Designing intuitive attendee and presenter interfaces for real-time events.

---

## 4️⃣ Impact

**For Participants:**

* Simplifies networking at tech meetups.
* Reduces cognitive load — attendees can focus on speakers.
* Keeps meaningful context for post-event follow-ups.

**For Presenters:**

* Quick slide sharing and smoother session start.
* Easier engagement with attendees.

**For Organizers:**

* Lightweight, easy-to-deploy event companion.
* Reduces manual tracking of attendance and contacts.

**Wider Impact:**

* Encourages collaboration and knowledge sharing in local tech communities.
* Demonstrates a scalable model for private or sensitive events.

---

## 5️⃣ Competitive Research

| Competitor                             | Features                                                      | Pros                                 | Cons                                                 | Relevance                                                              |
| -------------------------------------- | ------------------------------------------------------------- | ------------------------------------ | ---------------------------------------------------- | ---------------------------------------------------------------------- |
| **Brella**                             | Networking AI, agenda, matchmaking, virtual & physical events | Strong networking tools, polished UI | Cloud-based, may require subscription                | Partial — focuses on networking, but may be overkill for small meetups |
| **Swapcard**                           | Event app, attendee list, messaging, schedule                 | Good attendee engagement             | Cloud dependency, complex for small events           | Some overlap in attendee management                                    |
| **Meetup App**                         | Event discovery, RSVP, basic messaging                        | Widely known                         | Limited real-time slides sharing, networking context | Inspiration for event access                                           |
| **Hopin**                              | Virtual events, networking tables, polling                    | Mature platform                      | Requires Internet, SaaS, complex                     | Overpowered for small offline meetups                                  |
| **QR & NFC Card Apps (various)**       | Contact exchange via QR/NFC                                   | Fast connections                     | Limited context & analytics, mostly 1:1              | Relevant for offline contact exchange                                  |
| **Google Slides / AirDrop / OneDrive** | Resource sharing                                              | Easy to use                          | Not integrated with attendee context                 | Partial — only solves slide/resource sharing                           |

**Key Insight:**
No existing solution fully combines **offline/local networking, real-time slide sharing, attendee context retention, and lightweight deployment** — this is your unique value proposition.

---

## 6️⃣ Call to Action

We are looking for **2 backend + 1 frontend contributors** from the department to validate the idea by building an MVP:

* Duration: \~6–8 weeks
* Tech stack: Node.js (backend), React/Vue (frontend), WebSocket, SQLite/JSON
* Outcome: Functional MVP tested at a real department meetup

**Goal of Validation:**

* Assess user interest in offline networking and real-time sharing.
* Gather feedback on usability and feature relevance.
* Learn practical skills in full-stack development and local-network apps.

---

If you want, I can also **turn this into a visually appealing one-page PDF/flyer** with diagrams, feature icons, and a competitive snapshot — ready to send to friends or potential contributors.

Do you want me to do that next?
