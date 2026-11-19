<div align="center">

# 🧩 TaskBridge

### Work Planning Web Application

*Turns unclear work requests and goals into clear, actionable plans with tasks, priorities, and progress tracking.*

**Built with Lovable + Supabase** · **Build the System, Not the Screen**

</div>

---

## 📑 Table of Contents

1. [Problem](#-problem)
2. [Solution](#-solution)
3. [Users](#-users)
4. [How I Designed the Solution](#-how-i-designed-the-solution)
5. [How It Works](#️-how-it-works)
6. [Role of AI](#-role-of-ai)
7. [Automation](#-automation)
8. [Data](#️-data)
9. [Tools & Technologies](#️-tools--technologies)
10. [Key Design Decisions](#-key-design-decisions)
11. [Testing](#-testing)
12. [What I Learned](#-what-i-learned)
13. [Future Improvements](#-future-improvements)
14. [Project Links](#-project-links)
15. [Author](#-author)

---

## 🎯 Problem

### The Context

Freelancers, recent graduates, and early-career professionals often receive work requests or set goals that are not clear. They know what they want to achieve, but the work is not yet organized into steps.

### The Problem

It is hard to turn a goal into practical steps. Without a clear plan, a person cannot easily answer:

- What result do I need to reach?
- Which tasks are needed to reach it?
- Which tasks should I start with?
- What is already done, and what is still in progress?
- What is the next step?

### Why It Matters

Without a clear plan, it is difficult to organize the work, set priorities, and follow progress. A structured plan makes the work visible and shows exactly what to do next.

---

## 💡 Solution

TaskBridge is a responsive web app that gives the user one organized place to manage plans and tasks. It follows this sequence:

```text
Goal → Plan → Tasks → Priorities → Status → Progress
```

**What does the system do?**

| # | Feature | Description |
|:-:|---|---|
| 01 | **Authentication** | Sign up, log in, and log out. Private pages need a logged-in user. |
| 02 | **Plan Management** | Create, view, edit, and delete plans. |
| 03 | **Task Management** | Add, view, edit, and delete tasks inside a plan. |
| 04 | **Priorities** | Each task has a priority: High, Medium, or Low. |
| 05 | **Status** | Each task has a status: To Do, In Progress, or Done. |
| 06 | **Progress Tracking** | The app calculates the completion percentage of each plan. |
| 07 | **Data Persistence** | Plans and tasks stay saved after a refresh or a new login. |
| 08 | **User Data Isolation** | Each user can access only their own data. |

---

## 👤 Users

| | |
|---|---|
| **Primary Users** | Freelancers, recent graduates, early-career professionals, and individuals who need to organize their goals. |
| **User Need** | To turn a goal or an unclear work request into a plan with defined tasks, clear priorities, and visible progress. |

> The first version is for **individual use**. It does not include collaboration between several users inside the same plan.

---

## 🧠 How I Designed the Solution

The main principle of this project is **Build the System, Not the Screen**. The goal was not only an attractive interface, but also the system behind it: its data, its behavior, and its security.

I designed the system around one relationship:

```text
User → Plans → Tasks
```

- A user owns many plans.
- A plan contains many tasks.
- Each task belongs to one plan.
- The owner of a task must be the owner of its plan.
- Deleting a plan deletes its tasks.

I built the project in six connected stages:

| Stage | What happens |
|---|---|
| **1 — Set up Supabase** | Tables, relationships, constraints, indexes, RLS, and access policies |
| **2 — Connect Lovable to Supabase** | Create the Lovable project and check the connection |
| **3 — Build the interface** | Landing, authentication, My Plans, Create / Edit Plan, Plan Details |
| **4 — Implement the functions** | Auth, CRUD for plans and tasks, progress calculation |
| **5 — Test and improve** | Functions, data persistence, and user data isolation |
| **6 — Prepare for publishing** | Review security, test screen sizes, remove test data |

---

## ⚙️ How It Works

```text
User signs up / logs in
          ↓
   Creates a plan
(title, description, goal, deadline)
          ↓
  Adds tasks to the plan
 (priority + status for each task)
          ↓
Supabase saves the data and applies RLS
          ↓
The app calculates the progress percentage
          ↓
 The user follows the plan in one place
```

**Progress logic**

```text
Progress = (Completed Tasks ÷ Total Tasks) × 100
```

| Case | Result |
|---|---|
| 5 tasks, 2 done | `(2 ÷ 5) × 100 = 40%` |
| No tasks in the plan | `0%` |

The percentage is recalculated every time a task status changes.

---

## 🤖 Role of AI

> In this version, AI is used to **build** the application, not inside the application.

### What does AI do in this solution?

- ✅ Lovable (an AI App Builder) builds the pages and functions from my written requirements.
- ✅ It speeds up the implementation of the interface, authentication flow, and CRUD operations.
- ✅ It applies changes step by step when I describe what to fix or improve.

### What AI Should NOT Do

- ❌ Generate plans or suggest tasks inside the app. This is outside the MVP.
- ❌ Decide the database design, the relationships, or the security rules. These are my responsibility.
- ❌ Be trusted without checking. Every function must be tested on the real app.
- ❌ Put the `service_role` key in frontend code or in a public repository.

---

## 🔄 Automation

**What parts of the process are automated?**

- Recalculating the progress percentage when a task status changes.
- Linking every plan and task to the logged-in user.
- Deleting the tasks of a plan automatically when the plan is deleted.
- Applying the access rules (RLS) in the database on every request.

> There is no integration with external automation platforms in this version.

---

## 🗂️ Data

### Input

| Plan data (`plans`) | Task data (`plan_tasks`) |
|---|---|
| `title` | `title` |
| `description` | `description` (optional) |
| `goal` | `priority` — High / Medium / Low |
| `deadline` (optional) | `status` — To Do / In Progress / Done |
| `deliverables` (optional) | `sort_order` |
| `next_step` (optional) | |

Account data (email and password) is managed by Supabase Auth.

### Output

| Output | Description |
|---|---|
| **My Plans** | A list of the plans owned by the current user |
| **Plan Details** | The plan with its tasks, priorities, and statuses |
| **Progress** | The completion percentage of each plan |

### Data Integrity

- Every record has a unique primary key.
- Every plan is linked to a user, and every task is linked to an existing plan.
- The task owner must match the plan owner.
- Only the allowed priority and status values are accepted.

Full details are in [`database-schema.md`](database-schema.md).

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **Lovable** | Building the application with an AI App Builder |
| **Supabase Auth** | Authentication and user accounts |
| **Supabase PostgreSQL** | Storing plans and tasks |
| **Supabase RLS** | Controlling access to the data |
| **GitHub** | Documenting the project and managing its files and versions |

---

## 🔑 Key Design Decisions

### Decision 1 — Security in the database, not only in the interface

**Decision:** Enable Row Level Security (RLS) on `plans` and `plan_tasks`, so each user can reach only the records they own.

**Why:** Hiding data in the interface is not real protection. The rules must be enforced by the database itself.

### Decision 2 — A relational design with constraints

**Decision:** Use two related tables (`plans` and `plan_tasks`) with foreign keys, allowed values for priority and status, and cascade delete.

**Why:** This keeps the data correct and consistent. A task cannot exist without a plan, and no invalid values can be saved.

### Decision 3 — No AI features inside the first version

**Decision:** Leave out AI plan generation, automatic task suggestions, payments, team collaboration, and notifications.

**Why:** A small scope lets me focus on the core functions and check their quality before adding new abilities.

### Decision 4 — Database first, then the interface

**Decision:** Set up Supabase (tables, constraints, RLS) before building the pages in Lovable.

**Why:** The interface depends on the data. Designing the system first means the screens are built on a correct base.

---

## 🧪 Testing

> No function counts as tested until its real behavior is checked on the app.

### Test 1 — Create a plan and keep it saved

| | |
|---|---|
| **Input** | Sign up, create a plan with a title and goal, refresh the page, then log out and log in again. |
| **Expected Result** | The plan appears in My Plans and is still there after the refresh and the new login. |
| **Status** | ✅ / ❌ |

### Test 2 — Progress calculation

| | |
|---|---|
| **Input** | A plan with 5 tasks. Mark 2 as Done. Then open a plan with no tasks. |
| **Expected Result** | The first plan shows 40%. The empty plan shows 0%. The percentage changes when a status changes. |
| **Status** | ✅ / ❌ |

### Test 3 — User data isolation

| | |
|---|---|
| **Input** | Create plans with User A. Log in as User B and try to see, edit, or delete User A's plans and tasks. |
| **Expected Result** | User B cannot read, edit, or delete anything that belongs to User A. |
| **Status** | ✅ / ❌ |

### Test 4 — Deleting a plan

| | |
|---|---|
| **Input** | Delete a plan that contains several tasks. |
| **Expected Result** | The plan is removed and its tasks are deleted with it. |
| **Status** | ✅ / ❌ |

---



## 📚 What I Learned

| Lesson | What I learned |
|---|---|
| **Technical** | A real application needs more than pages. It needs authentication, a relational database with constraints, and access rules (RLS) enforced in the database. |
| **Problem-Solving** | Design the system before the screen: define the data, the relationships, and the expected behavior first, then build in stages and test each one. |
| **AI** | AI App Builders make building faster, but I am still responsible for understanding, directing, evaluating, and improving what the AI builds. A working screen does not prove the system is correct or secure. |

---

## 🔮 Future Improvements

If I continued developing this project, I would:

- [ ] Add AI plan generation: create a first plan from a goal written in natural language.
- [ ] Add AI output evaluation: check generated plans for clarity, completeness, and realism.
- [ ] Connect the app to external automation platforms.
- [ ] Study turning it into a Progressive Web App (PWA).

---

## 🔗 Project Links

| | |
|---|---|
| **Live Demo** | [Open the app](https://pixel-perfect-forge-325.lovable.app) |

---

## 👩‍💻 Author

<div align="center">

**Zainab Maher**

[LinkedIn](https://www.linkedin.com/in/zainab-maher-2211553b6/) · [GitHub](https://github.com/ZainabMaher)

*Build the System, Not the Screen.*

</div>
