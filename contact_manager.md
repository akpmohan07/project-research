

# Contact Graph Manager (MVP) – Notes

**Date:** 2025-10-01  
**Project Type:** Personal/Portfolio Project  
**Goal:** Build a contact management app using a **graph structure**, with multi-parameter filtering and file persistence.

---

## Goal
- Manage contacts as a **graph**:  
  - **Nodes (Contacts):** `name`, `email`, `company`, `skills`, `interests`  
  - **Edges (Connections):** `context`, `type`, `date`  
- Support **multi-parameter filtering** (skills, interests, events, connection type).  
- Store/load the graph to/from **JSON** (human-readable, portable).

---

## Data Storage Options

| Format | Pros | Cons | Learning |
|--------|------|------|---------|
| **JSON** ✅ | Human-readable, portable, nested structure, easy parsing | Slightly slower for huge graphs | Serialization, filtering, multi-platform apps |
| **CSV** | Simple, lightweight | Hard for nested data | Parsing tabular data |
| **Binary Serialization** | Fast, compact | Java-specific, not readable | Object persistence, memory-efficient |
| **GraphML / GEXF** | Visualization, metadata | Verbose, complex | Graph theory, visualization |
| **YAML** | Clean syntax | Parser needed | Similar to JSON |

**Recommended for MVP:** **JSON** → maximum learning, human-readable, portable.

---

## MVP Features
1. Add / remove contacts  
2. Add / remove connections (`context`, `type`, `date`)  
3. Multi-parameter filtering (`skills`, `interests`, `context`, `type`, `date`)  
4. Load/save JSON  
5. Optional: console UI or minimal visualization

---

## Data Structure (Java Example)
```java
class Contact {
    String id, name, email, company;
    List<String> skills, interests;
}

class Connection {
    Contact to;
    String context, type;
    Date date;
}

class ContactGraph {
    Map<String, Contact> contacts;
    Map<String, List<Connection>> edges;

    List<Contact> findContacts(String skill, String context, Date fromDate, Date toDate) { ... }
}

---

## Example JSON Structure

```json
{
  "contacts": [
    {
      "id": "1",
      "name": "Mohan",
      "email": "mohan@example.com",
      "company": "Freshworks",
      "skills": ["Java","AI"],
      "interests": ["Graph","Cloud"]
    },
    {
      "id": "2",
      "name": "Alice",
      "email": "alice@example.com",
      "company": "TechCorp",
      "skills": ["React","NodeJS"],
      "interests": ["Frontend","UI"]
    }
  ],
  "connections": [
    {
      "from": "1",
      "to": "2",
      "context": "Met at DublinJS Meetup",
      "type": "friend",
      "date": "2025-09-10"
    }
  ]
}
```

---

## Workflow

1. **Load JSON** → parse into in-memory graph (`ContactGraph`)
2. **Add/remove contacts/connections** in memory
3. **Filter/search** using multi-parameter queries (`skills`, `interests`, `context`, `type`, `date`)
4. **Save back** to JSON for persistence
5. Optional: visualization (GraphML/GEXF/D3.js)

---

## Estimated Timeline

| Task                              | Duration  | Notes                                   |
| --------------------------------- | --------- | --------------------------------------- |
| Project setup + classes           | 1 day     | `Contact`, `Connection`, `ContactGraph` |
| JSON load/save                    | 0.5–1 day | Use Jackson/Gson                        |
| Add/remove contacts & connections | 1 day     | In-memory operations                    |
| Multi-parameter filtering         | 1–2 days  | Skills, interests, context, type, date  |
| Testing/validation                | 1 day     | Verify filtering, adding/removing       |
| Console UI / CLI                  | 0.5–1 day | Optional                                |
| Visualization (GraphML/D3.js)     | 2–3 days  | Optional                                |

**Total MVP Time:** 4–6 days (without visualization), 1–2 weeks (with visualization)

---

## Key Learning Points

* Graph modeling in memory (nodes/edges)
* Serialization/deserialization (JSON)
* Multi-parameter filtering in-memory
* File I/O (load/save JSON)
* Optional: graph visualization (GraphML/GEXF/D3.js)

---

## Next Steps

* Design **ready-to-code JSON schema** and Java classes
* Implement **add/remove/filter** functionality
* Extend with **visualization** later
