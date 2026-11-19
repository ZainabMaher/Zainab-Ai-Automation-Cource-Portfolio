<div align="center">

# 🗺️ Concept Atlas · أطلس المفاهيم

### Visual Thinking Canvas

*A local-first, interactive canvas for mapping complex knowledge with meaningful relationships, offline support, and optional cloud sync.*

**Built with Lovable** · **React Flow + Supabase** · **Arabic & English**

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

In an era of information overload, researchers, students, software engineers, and strategic thinkers deal with deeply connected concepts, literature, projects, and hypotheses. Understanding these domains means exploring how ideas influence, contradict, or depend on one another, not flattening them into separate text documents.

### The Problem

- **Note-taking apps** rely on linear documents or nested folders, so they do not show multi-dimensional dependencies and feedback loops.
- **Visual diagramming tools** need a constant internet connection, store private thoughts on outside servers, and treat connectors as decorative arrows with no meaning.

### Why It Matters

Modeling relationships by meaning (causality, contradiction, dependency, support) mirrors how the human mind builds knowledge. An intuitive and secure visual medium uncovers blind spots, clarifies trade-offs, and speeds up deep learning and problem-solving.

---

## 💡 Solution

Concept Atlas is a high-performance visual thinking workspace built on a strict local-first architecture. Users map, categorize, and cross-reference knowledge elements, custom shapes, and images with rich directed relationships. It works completely offline, with cloud backup when desired.

**What does the system do?**

| Feature | Description |
|---|---|
| **Typed Knowledge Nodes** | Organizes items by type (person, book, idea, question, project, goal, quote, problem, resource, or custom) with custom styling and media attachments. |
| **Rich Semantic Edges** | Links concepts with typed relationships (causes, contradicts, supports, depends on, part of, influences, leads to), with direction, explanation, confidence rating, and source. |
| **Freeform Elements & Resizing** | Adds resizable shapes and floating images that share connection handles with concept nodes. |
| **Local-First Privacy** | Saves graph structure in browser `localStorage` and images in `IndexedDB`, with no cloud dependency. |
| **Optional Cloud Sync** | Supabase authentication and automatic cloud backup for cross-device access, protected by Row-Level Security (RLS). |
| **High-Definition Export** | Exports the full canvas as a high-resolution PNG image or a portable JSON file. |

---

## 👤 Users

**Primary Users**

| User | How they use it |
|---|---|
| **Academic Researchers & Students** | Synthesizing research papers, philosophical arguments, and multidisciplinary literature |
| **Engineers & Architects** | Designing workflows, system architectures, and decision trees |
| **Writers & Creative Strategists** | Brainstorming non-linear narratives, world-building, and concept incubation |

**User Need**

A fast, distraction-free spatial thinking tool that works anywhere without lag or mandatory sign-in, with full data ownership and high-quality visual output.

---

## 🧠 How I Designed the Solution

The core design philosophy is **data sovereignty and immediacy**. The canvas opens directly into a fully working local workspace, without asking for credentials or making network calls.

- **Modular architecture:** React Flow handles the graph. A browser storage layer keeps the data: `IndexedDB` for large image files and `localStorage` for the graph structure.
- **Backward compatibility:** Data normalization pipelines upgrade older maps automatically as the schema changes, so no user data is lost.
- **Bilingual interface:** Native RTL Arabic and LTR English, with an adaptive light / dark theme.

---

## ⚙️ How It Works

```text
User Input (Concept, Resizable Shape, or Image)
  ↓
Local Storage Engine
(IndexedDB for binary files + localStorage for graph data)
  ↓
Semantic Normalization & Graph Engine
(React Flow canvas & custom edge resolvers)
  ↓
Debounced Cloud Synchronization
(Supabase PostgreSQL with RLS, when signed in)
  ↓
Interactive Canvas / High-Resolution PNG / Portable JSON Export
```

---

## 🤖 Role of AI

### What does AI do in this solution?

- ✅ **Knowledge modeling and workflow blueprints:** turns structured knowledge domains into ready-made interactive concept maps, such as the AI & Intelligent Automation ecosystem map.
- ✅ **Semantic relationship recommendations:** structures logical relationship types (cause and effect, systemic dependencies, and contradictions).

### What AI Should NOT Do

- ❌ Alter, summarize, or overwrite user-written concepts without explicit confirmation.
- ❌ Force rigid hierarchies onto natural, organic thinking.
- ❌ Send private canvas content to third parties without user consent.

---

## 🔄 Automation

**What parts of the process are automated?**

| Automation | What it does |
|---|---|
| **Debounced Autosave** | Detects canvas changes and saves them locally within 600 ms of inactivity. |
| **Background Cloud Sync** | Syncs to Supabase after each save whenever the user is signed in. |
| **Schema Normalization** | Upgrades old edges and node definitions on load to the new relationship structure, without breaking older maps. |
| **Aspect-Ratio Calculation** | Reads media dimensions and scales node containers to fit uploaded covers, portraits, and images. |

---

## 🗂️ Data

### Input

| Input | Details |
|---|---|
| **Concept nodes** | Title, archetype, description, references, attachments |
| **Binary media** | PNG, JPEG, WebP, GIF files up to 5 MB, stored in IndexedDB |
| **Relationship descriptors** | Semantic type, direction, description, source URL, confidence score (0–100%) |
| **Shapes** | Geometric shapes with resizable bounding boxes |

### Output

| Output | Details |
|---|---|
| **Interactive graph** | A responsive spatial graph in the browser |
| **PNG image** | High resolution: scale ×3, up to 6000 × 6000 px |
| **JSON file** | A fully portable standalone map |
| **Cloud snapshot** | Encrypted `jsonb` map snapshots saved in the cloud |

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **React 19 & TanStack Start** | Full-stack application foundation, SSR capability, and routing |
| **@xyflow/react (React Flow v12)** | Infinite interactive canvas, custom nodes, handles, and edge routing |
| **Tailwind CSS v4** | Design tokens, fluid typography, dark mode, and RTL layout |
| **IndexedDB & LocalStorage** | High-capacity local-first storage for images and graph state |
| **Supabase (PostgreSQL & GoTrue)** | Authentication, Row-Level Security (RLS), and cloud sync |
| **html-to-image** | Rendering the canvas into high-resolution images in the browser |
| **@fontsource/cairo** | Self-hosted font for consistent Arabic / English rendering without CORS blocks |
| **Vitest** | Unit and integration tests for persistence schemas and node rules |

---

## 🔑 Key Design Decisions

### Decision 1 — Local-first architecture

**Decision:** Build the application as a strict local-first system instead of relying on a cloud-dependent CRUD server.

**Why:** It loads instantly, works on unreliable connections, and removes privacy concerns for sensitive notes and private brainstorming.

### Decision 2 — Relationships as first-class entities

**Decision:** Treat relationships as semantic entities with direction, confidence ratings, and contextual notes.

**Why:** Traditional mind maps use generic lines that lose their meaning over time. Rich, typed relationships turn a sketch into a verifiable, machine-readable knowledge graph.

---

## 🧪 Testing

### Test 1 — Persistence & Offline Resilience

| | |
|---|---|
| **Input** | Create a new node with a high-resolution image, connect it to an existing concept with an 85% confidence "Causes" relationship, then do a hard browser reload. |
| **Expected Result** | The map restores completely. The image reloads from IndexedDB, and the relationship keeps its semantic data and visual styling. |
| **Actual Result** | All nodes, custom attributes, and image references were restored with 100% data fidelity. |
| **Status** | ✅ |

### Test 2 — Universal Connections & Resizing

| | |
|---|---|
| **Input** | Insert an independent shape and a floating image, resize them with the resizer handles, and draw a connector from the shape to a core knowledge node. |
| **Expected Result** | Connection handles attach correctly for every element type. Dimensions persist across map switches and exports without distortion. |
| **Actual Result** | The universal handles connected successfully, and the resized dimensions were saved accurately. |
| **Status** | ✅ |

---

## 📸 Evidence

### Final Result

An infinite visual workspace in English and Arabic, with light / dark themes, full node type palettes, customizable board backgrounds, and unified account management.

![Final Result](Screenshots
/Final_Result_Atlas.png
)

### Workflow

`Add Element` → `Define Archetype & Details` → `Connect & Assign Relationship` → `Automatic Local / Cloud Save` → `Export`

![Workflow](Screenshots
/workflow.png
)

---

## ⚠️ Challenges & Failures

**What didn't work as expected?**

- **Arabic text in PNG export:** Arabic typography fell back to system fonts or did not render at all, because external Google Fonts URLs were blocked by browser CORS rules.
- **Older maps breaking:** Adding new relationship types broke the rendering of existing maps.

**How did I solve it?**

- Bundled the Cairo font inside the project (`@fontsource/cairo`) instead of loading it from a remote CDN, so `html-to-image` captures the glyphs correctly.
- Built a backward-compatible normalization layer (`normalizeRelationship`) that maps old edges to the new schema at runtime, without changing or corrupting the user's older files.

---

## 📚 What I Learned

| Lesson | What I learned |
|---|---|
| **Technical** | Local-first engineering: coordinating image storage in `IndexedDB` with structured data in `localStorage`, and syncing both with a PostgreSQL backend through debounced background saves. |
| **Problem-Solving** | Schema migration and backward compatibility matter. Core data models must be normalized defensively, so new features never break what users already created. |
| **AI** | AI tools give the most value when they support human reasoning and scaffold complex structures, while the user keeps full ownership and final validation. |

---

## 🔮 Future Improvements

If I continued developing this project, I would:

- [ ] **Real-time collaboration:** add WebRTC / CRDTs so distributed teams can edit together.
- [ ] **AI-driven concept discovery:** an intelligent agent that analyzes the canvas to highlight hidden connections, paradoxes, and knowledge gaps.
- [ ] **Mobile app:** extend the local-first engine to native iOS and Android.

---

## 🔗 Project Links

| | |
|---|---|
| **Live Demo** | [Open the app](https://visual-style-snapshot.lovable.app) |
| **Workflow** | [View workflow](Screenshots/workflow.png) |
| **Repository** | [GitHub repo](https://github.com/ZainabMaher/visual-style-snapshot) |
---

## 👩‍💻 Author

<div align="center">

**Saja Saja**

[LinkedIn](https://www.linkedin.com/in/zainab-maher-2211553b6/) · [GitHub](https://github.com/ZainabMaher)

</div>
