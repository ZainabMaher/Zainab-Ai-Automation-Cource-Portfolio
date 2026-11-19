<div align="center">

# 🌉 SkillBridge Lite

### AI-Powered Career Fit Assistant

*Turns a professional profile and a selected opportunity into actionable AI feedback.*

**Built with Lovable** · **U2 — System Thinking** · **MVP Prototype**

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
12. [Evidence](#-evidence)
13. [Challenges & Failures](#️-challenges--failures)
14. [What I Learned](#-what-i-learned)
15. [Future Improvements](#-future-improvements)
16. [Project Links](#-project-links)
17. [Author](#-author)

---

## 🎯 Problem

### The Context

Students, recent graduates, and early-career professionals usually have some skills, projects, and experience, but this information is scattered. When they find a specific opportunity, they have no clear way to see how their profile relates to what the opportunity asks for.

### The Problem

It is hard to turn scattered professional information into a clear understanding of the relationship between a profile and the requirements of **one specific opportunity**.

People struggle to answer questions such as:

- Which of my skills relate to this opportunity?
- What evidence in my projects and experience supports my fit?
- Which requirements have I not given enough information about?
- What can I do to be better prepared?

### Why It Matters

Without this clarity, people apply without knowing their strengths, miss gaps they could close, or do not know what to improve next. A clear, honest comparison helps them present themselves better and plan practical next steps.

---

## 💡 Solution

SkillBridge Lite is a small web app with one clear flow: review your profile, pick an opportunity, and get an AI analysis of how the two relate.

> It is **not** a full recruitment platform. It is a small digital solution for one specific problem.

**What does the system do?**

| # | Feature | Description |
|:-:|---|---|
| 01 | **View and Edit My Profile** | The user reviews and edits name, headline, about, skills, projects, and experience. |
| 02 | **Explore Opportunities** | The app shows three ready-made sample opportunities. |
| 03 | **View Opportunity Details** | The user opens an opportunity to read its description, required skills, and responsibilities. |
| 04 | **Analyze My Fit** | The user requests an analysis that compares the profile with the selected opportunity. |
| 05 | **View AI Feedback** | The result appears in three sections: Relevant Skills, Potential Gaps, Recommended Next Steps. |

---

## 👤 Users

| | |
|---|---|
| **Primary Users** | Students, recent graduates, and early-career professionals who have some skills, projects, or experience. |
| **User Need** | To understand how their professional profile relates to a specific opportunity, and to know what to do next to improve their readiness. |

> This version is designed for a **single user**. There are no multiple roles and no admin dashboard.

---

## 🧠 How I Designed the Solution

I followed the five U2 layers. Each layer produced decisions that I used in the next one.

| Layer | What I decided | Output |
|---|---|---|
| **01 — Understand the User** | Who the user is, their goal, need, and context | User Definition |
| **02 — Define the Solution** | The problem statement, the solution, and the MVP | Solution Definition |
| **03 — Design the Experience** | Screens, navigation, and interactions | UX Flow |
| **04 — Design the System** | Data, inputs, outputs, and system logic | System Design |
| **05 — Specify & Build with AI** | Clear specifications to guide Lovable | Working Prototype |

**Main idea:** building with AI does not start with a prompt. It starts with understanding the problem, the user, and the result we want. I defined a small MVP of five features and a clear list of what *not* to build, then built it step by step in Lovable instead of using one huge prompt.

---

## ⚙️ How It Works

```text
Professional Profile + Selected Opportunity
                  ↓
     User clicks "Analyze My Fit"
                  ↓
 AI compares the profile with the
     opportunity requirements
                  ↓
 The result is organized into sections
                  ↓
 Relevant Skills · Potential Gaps · Recommended Next Steps
```

**Core user flow**

```text
Home
  ↓
My Profile
  ↓
Explore Opportunities
  ↓
Opportunity Details
  ↓
Analyze My Fit
  ↓
AI Fit Analysis
  ↓
Recommended Next Steps
```

---

## 🤖 Role of AI

> AI is **one function inside the solution**, not the whole product.

### What does AI do in this solution?

- ✅ Finds the skills and experience in the profile that relate to the opportunity requirements.
- ✅ Points out requirements that the profile does not give enough information to support, or that may need development.
- ✅ Suggests practical next steps to improve the profile or the user's readiness.

### What AI Should NOT Do

- ❌ Use information that is not in the profile, or invent skills or experience.
- ❌ Treat missing information as proof that the user lacks a skill.
- ❌ Treat a skill that is only mentioned as if it were proven by evidence.
- ❌ Guarantee acceptance or predict the hiring result.
- ❌ Present its result as a final judgment. It is a helpful estimate only.

### Real vs. Sample Analysis

| Type | Meaning |
|---|---|
| **Real AI Analysis** | A result generated by an AI model. |
| **Sample Analysis** | Fixed demo data, used to show the shape of the output when the AI connection is not available. |

> ⚠️ The app must always make clear which one the user is seeing. A sample result is never presented as real AI output.

---

## 🔄 Automation

**What parts of the process are automated?**

- Comparing the profile with the requirements of the selected opportunity.
- Generating the feedback and organizing it into the three sections.
- Keeping profile edits in the app (app state / browser storage), so the user does not re-enter them for each analysis.

---

## 🗂️ Data

> There is no database and no backend in this version. Data lives inside the app.

### Input

| Profile Data | Opportunity Data |
|---|---|
| `name` | `title` |
| `headline` | `company` |
| `about` | `description` |
| `skills` | `requiredSkills` |
| `projects` | `responsibilities` |
| `experience` | |

### Output

An AI fit analysis with three sections:

| Section | What it contains |
|---|---|
| **1. Relevant Skills** | Skills or experience in the profile that relate to the opportunity requirements. |
| **2. Potential Gaps** | Requirements the profile does not give enough information about, or that may need development. |
| **3. Recommended Next Steps** | Practical steps to improve the profile or the user's readiness. |

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **Lovable** | Building the web app from natural-language specifications, step by step |
| **App state / browser storage** | Keeping the profile data and edits without a database |
| **Built-in sample data** | The three opportunities and the sample analysis |

---

## 🔑 Key Design Decisions

### Decision 1 — A five-feature MVP

**Decision:** Keep the MVP to five features only: edit profile, explore opportunities, view opportunity details, analyze my fit, view AI feedback.

**Why:** This is the smallest version that completes the core user flow. It can be built in one training session with a limited number of Lovable credits.

### Decision 2 — No login and no database

**Decision:** No login, no database, no Supabase, and no admin dashboard. Data is kept in app state or browser storage.

**Why:** These parts do not serve the learning goal of this unit and would add cost and complexity. The trade-off: edits may stay after a refresh on the same device, but there is no personal account across devices.

### Decision 3 — Strict AI rules and honest labeling

**Decision:** Give the AI strict rules and always label the result as real or sample.

**Why:** The feedback must be honest and based only on what the user provided. A screen that shows an "AI result" is not proof that the analysis is real, so the user has to know which one they are seeing.

### Decision 4 — Build in stages

**Decision:** Build step by step (foundation → core experience → opportunity flow → AI analysis → review and refine) instead of one large prompt.

**Why:** Each step has one clear goal, keeps what was built before, and avoids rebuilding the whole app for a small change.

---

## 🧪 Testing

### Test 1 — Profile that matches the opportunity

| | |
|---|---|
| **Input** | A profile with skills and projects that relate to the selected opportunity, then click **Analyze My Fit**. |
| **Expected Result** | The related skills appear under Relevant Skills, and every item comes from the profile. No invented skills. |
| **Status** | ✅ / ❌ |

### Test 2 — Profile with little information

| | |
|---|---|
| **Input** | A profile with only one or two skills and no projects, analyzed against the same opportunity. |
| **Expected Result** | Missing requirements appear under Potential Gaps as "not enough information", not as "the user does not have this skill". No hiring prediction. |
| **Status** | ✅ / ❌ |

### Test 3 — Editing the profile

| | |
|---|---|
| **Input** | Add a new skill in My Profile, save, then run the analysis again. |
| **Expected Result** | The edit is saved and the new analysis uses the updated profile. |
| **Status** | ✅ / ❌ |

---

---



## 📚 What I Learned

| Lesson | What I learned |
|---|---|
| **Technical** | A useful prototype does not need a database or login. Simple in-app data is enough to deliver the core flow, and building in small stages keeps the work under control. |
| **Problem-Solving** | Start from the problem, the user, and the result, not from the tool. Deciding what *not* to build is as important as deciding what to build. |
| **AI** | AI is a function with a specific purpose inside the solution. It needs clear rules: use only the given information, do not invent, do not predict hiring results. A result must also be labeled honestly as real or sample. |

---

## 🔮 Future Improvements

If I continued developing this project, I would:

- [ ] Add user accounts and a database so the profile is saved across devices.
- [ ] Let the user add or paste their own opportunities instead of only three samples.
- [ ] Let the user save opportunities and past analyses to track progress over time.

---

## 🔗 Project Links

| | |
|---|---|
| **Live Demo** | [Open the app](https://preview--exact-render-studio-47.lovable.app/) |
| **Workflow** | [View workflow](https://github.com/ZainabMaher/Zainab-Ai-Automation-Cource-Portfolio/tree/main/02-System%20Thinking/Course-Project/Screenshots) |
| **Repository** | [GitHub repo](https://github.com/ZainabMaher/exact-render-studio-47) |
---

## 👩‍💻 Author

<div align="center">

**Zainab Maher**

[LinkedIn](https://www.linkedin.com/in/zainab-maher-2211553b6/) · [GitHub](https://github.com/ZainabMaher)

*Build the smallest useful solution that solves the right problem.*

</div>
