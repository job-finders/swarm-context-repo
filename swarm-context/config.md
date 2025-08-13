---

## **1. Folder Structure**

```
/agentic-context
│
├── /features           # One folder per active feature/task
│   ├── job-alert-system/
│   │   ├── context.md         # Latest context
│   │   ├── history/           # Older versions
│   │   │   ├── 2025-08-13_kiro.md
│   │   │   ├── 2025-08-13_kilocode.md
│   │   │   └── ...
│   │   └── attachments/       # Any screenshots, code snippets, diagrams
│   │
│   ├── cv-optimizer/
│   │   ├── context.md
│   │   └── history/
│   │       ├── ...
│   │
│   └── ...
│
└── /templates          # Spec/context templates for agents
```

---

## **2. Context File Structure**

**`context.md`** is the “live” memory for that feature.
Agents always:

1. **Read** this file before starting work.
2. **Append updates** to the bottom when done.
3. **Version it** by moving the old copy to `/history/`.

Example:

```markdown
# Feature: Job Alert System

## Last Update
2025-08-13 15:42 – Updated by Kilocode

## Current Status
- Backend endpoint `/alerts/create` implemented.
- Awaiting frontend integration for alert subscription form.

## Next Agent Task
- Kiro: Plan email template structure.
- Cursor: Prepare SQL query for filtering job alerts by user preferences.

## Known Issues
- Email scheduling service not configured yet.

## Relevant Links
- Planning spec: ../specs/planning/2025-08-13__kiro__job-alert-system-plan.md
- GitHub branch: `feature/job-alerts`
```

---

## **3. Agent Workflow Rules**

For every agent in your swarm:

**Step 1 – Load Context**

* Before starting, open `/features/<feature-name>/context.md`.

**Step 2 – Work**

* Execute your task based on the plan.

**Step 3 – Update Context**

* Append a new section like:

  ```markdown
  ### Update – 2025-08-13 16:20 by Kiro
  - Added detailed plan for email templates.
  - Defined placeholders for variables in email body.
  - Next: Kilocode implements email sending module.
  ```

**Step 4 – Versioning**

* Move the previous `context.md` to `/history/YYYY-MM-DD_agent.md`
* Save your new `context.md` in its place.

---

## **4. Naming & Versioning**

* Always timestamp updates: `YYYY-MM-DD_HHMM_agent.md`
* Example:

  ```
  /features/job-alert-system/history/2025-08-13_1642_kilocode.md
  ```

---

## **5. Templates for Consistency**

You can keep a `/templates/context_template.md` so all agents follow the same structure:

```markdown
# Feature: [Feature Name]

## Last Update
[YYYY-MM-DD HH:MM] – Updated by [Agent Name]

## Current Status
[Summary of where this feature is right now]

## Next Agent Task
[Who’s up next and what they need to do]

## Known Issues
[List blockers or bugs]

## Relevant Links
[Links to specs, branches, designs, etc.]
```

---

This method has a big advantage:

* **No tool lock-in** — works with Kiro, Kilocode, Cursor, Claude, GPT, whatever.
* **Swarm ready** — any number of agents can pick up where the last left off.
* **Zero API complexity** — it’s just text files.
---
