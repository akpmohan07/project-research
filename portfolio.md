https://app.clickup.com/t/86d0ch89c

https://chatgpt.com/c/68cdb23d-5b84-832e-80a5-8430b55b3c02


# Portfolio Landing Page – Project Description

## 1️⃣ Project Vision

Create a **lightweight personal portfolio** that presents both professional achievements and personal interests in one scrollable page.
The site should be easy to update: every change to experience, projects, or hobbies will come from small JSON files, merged through a Pull Request.

---

## 2️⃣ Objectives

* Provide recruiters a clear, concise view of my skills, work history, and pet projects.
* Offer fellow developers an easy way to discover my open-source work and research ideas.
* Maintain a personal touch by showing interests such as music, movies, and fitness progress.

---

## 3️⃣ Key Principles

* **Simplicity first** – no heavy framework or build step.
* **Separation of concerns** – keep data in JSON, presentation in HTML/Tailwind, logic in a tiny JS file.
* **Ease of maintenance** – edit JSON + PR → automatic site update via GitHub Pages.
* **Progressive enhancement** – start minimal, add features only when needed.

---

## 4️⃣ Core Features

| Area              | Description                                                        |
| ----------------- | ------------------------------------------------------------------ |
| Hero              | Top banner with name, tagline, and quick links                     |
| Experience        | Timeline rendered from `experience.json`                           |
| Projects          | Cards rendered from `projects.json` with links to code/demo        |
| Tech Profiles     | GitHub, LeetCode, LinkedIn icons with links; optional commit graph |
| Research & Events | Simple lists of ideas and attended events                          |
| Blogs             | Space for articles or external links                               |
| Personal Section  | Music history, movie history, fitness milestones                   |
| Contact           | Email + social handles in footer                                   |

---

## 5️⃣ Data Model (JSON Examples)

All content is stored in JSON files inside `/data`.
The HTML page dynamically fetches and renders this content using JavaScript.

---

### 5.1 Experience (`experience.json`)

```json
[
  {
    "role": "Software Engineer",
    "company": "ABC Tech",
    "period": "Jan 2023 – Present",
    "details": "Worked on Time Machine Project (RDS & Redis restoration) and Azure integration."
  },
  {
    "role": "Associate Engineer",
    "company": "XYZ Ltd",
    "period": "Jun 2021 – Dec 2022",
    "details": "Built scalable APIs and improved DB performance by 30%."
  }
]
```

---

### 5.2 Projects (`projects.json`)

```json
[
  {
    "title": "Scandgo",
    "desc": "Automated laptop check-ins/out using QR codes and Excel logs for lab management.",
    "link": "https://github.com/akpmohan07/Scandgo"
  },
  {
    "title": "CGPA Calculator",
    "desc": "Android app to automate CGPA calculation for Computer Science students.",
    "link": "https://github.com/yourhandle/cgpa-calculator"
  }
]
```

---

### 5.3 Personal (`personal.json`)

```json
{
  "music": [
    {"artist": "Daft Punk", "topAlbum": "Discovery"},
    {"artist": "Hans Zimmer", "topAlbum": "Inception OST"}
  ],
  "movies": [
    {"title": "Interstellar", "year": 2014, "note": "Inspiration for space & physics interest"},
    {"title": "The Equalizer 2", "year": 2018, "note": "Favourite action movie"}
  ],
  "fitness": {
    "weightKg": 77,
    "heightCm": 162,
    "stepsPerDay": 10000,
    "gymDaysPerWeek": 6
  }
}
```

---

## 6️⃣ Technology Stack

* **Frontend:** HTML5 + Tailwind CSS
* **Logic:** Vanilla JavaScript (`fetch` + DOM rendering)
* **Hosting:** GitHub Pages
* **Versioning:** GitHub PRs for content and code

---

## 7️⃣ Milestones

### Phase 1 – MVP (Weeks 1–2)

* Implement hero, experience, projects
* Deploy working page

### Phase 2 – Polish (Weeks 3–4)

* Add tech profiles, research, events
* Improve layout & mobile view

### Phase 3 – Personal & Enhancements (Weeks 5+)

* Add personal JSON data (music/movies/fitness)
* Optional charts or animations
* Write blogs directly or link external posts

---

## 8️⃣ Future Ideas

* Integrate analytics (privacy-friendly)
* Dark/light theme toggle
* Markdown blog rendering
* Auto-fetch GitHub activity for commit chart

---

## 9️⃣ Notes

Keep the project **evolving in small increments**.
Document decisions and new features directly in this file so it becomes a living history of the portfolio.

> *Initial draft created: 19 Sep 2025*
> *Next update planned after completing Phase 1*
