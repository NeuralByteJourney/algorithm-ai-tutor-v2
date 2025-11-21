# 🧠 Algorithm AI Tutor — Agentic Version (V2)

A multi-agent AI tutor for learning algorithms and data structures using a fully synthetic curriculum.

**Version 2** is a complete rewrite of an earlier “ECE250 AI Tutor” project, rebuilt with an **agentic architecture** inspired by Google’s Agent Development Kit (ADK). The goal is to make the tutor more accurate, robust, and production-ready.

---

## 🚀 Overview

**Algorithm AI Tutor V2** helps students learn algorithms and data structures through:

- Adaptive explanations at different difficulty levels  
- Synthetic (non-copyright) practice problems  
- Visualizations of algorithms (sorting, graphs, recursion, DP)  
- Code evaluation with hints  
- Personalized learning paths and spaced repetition  

This project is designed for:

- Kaggle “Agents for Good” Capstone  
- A portfolio project for AI / ML / SWE roles  
- Learners who struggle with algorithm intuition    

> ⚠️ All content is synthetic. No university assignments, slides, or copyrighted course materials are used.

---

## 🧩 Architecture (High-Level)

The system is organized around **multiple cooperating agents** plus shared workflows and memory.

**Core components:**

- `agents/` – Individual agents (concept, problem generation, grading, visualization, diagnostics, orchestrator)
- `workflows/` – Long-running multi-step processes (tutoring, grading, visualization, diagnostic)
- `memory/` – Student profiles, mastery tracking, spaced repetition logic
- `synthetic_curriculum/` – Synthetic explanations, examples, and problem sets
- `utils/` – Logging, safety checks, schema validation, helpers
- `api/` – Backend entrypoints (HTTP or CLI-style interface)
- `ui/` – Streamlit (and optionally Flask/Tailwind) user interfaces
- `datasets/` – JSON datasets with synthetic questions and test cases
- `tests/` – Unit tests and integration tests for agents and workflows

The overall idea:

1. The **Orchestrator Agent** receives a user request (e.g., “explain Dijkstra”, “give me a quiz on DP”).
2. It decides which specialized agents to call (concept, problem generator, grader, visualization, or diagnostic).
3. A **workflow** coordinates multi-step logic (e.g., generate problem → grade answer → update mastery → recommend next step).
4. The **memory layer** stores student progress and personalizes future sessions.

---

## 🧠 Agents

Located in: `agents/`

Planned agents:

1. **Concept Agent**  
   - Explains algorithms at different levels (beginner → advanced)  
   - Produces pseudocode, intuitive explanations, and step-by-step traces  
   - Can adapt style if the user is confused

2. **Problem Generator Agent**  
   - Creates synthetic practice problems (MCQ, open-ended, coding)  
   - Adjusts difficulty (easy/medium/hard) based on mastery  
   - Avoids leaking full solutions; focuses on helpful hints

3. **Visualization Agent**  
   - Produces visual explanations (e.g., trace of BFS, recursion tree, DP table)  
   - Uses Python plotting / diagrams to render examples  
   - All examples are synthetic and safe to share

4. **Grader Agent**  
   - Evaluates student answers and code using deterministic test cases  
   - Provides structured feedback and hints  
   - Identifies common misconceptions (off-by-one, wrong complexity reasoning, etc.)

5. **Diagnostic Agent**  
   - Tracks which topics the student struggles with  
   - Updates a mastery map for core topics (sorting, graphs, DP, etc.)  
   - Schedules review using spaced repetition principles

6. **Orchestrator Agent**  
   - Main entrypoint for the system  
   - Routes user intents to the right agent(s)  
   - Composes responses from multiple agents in a coherent way

---

## ⚙️ Workflows

Located in: `workflows/`

Each workflow represents a multi-step process that may include long-running operations and needs to be robust and resumable (inspired by ADK-like patterns).

Planned workflows:

1. **Tutoring Workflow (`tutoring_workflow.py`)**
   - Parse user intent (ask, practice, debug, explain, visualize)
   - Call Concept / Problem Generator / Visualization agents as needed
   - Return a combined, structured answer

2. **Grading Workflow (`grading_workflow.py`)**
   - Receive a student answer or code solution  
   - Run grading tools (testcases, heuristic checks)  
   - Call Grader Agent to generate hints  
   - Update Diagnostic / Mastery state

3. **Visualization Workflow (`visualization_workflow.py`)**
   - Build an internal representation of an algorithm run  
   - Generate plots or diagrams  
   - Package them for the UI

4. **Diagnostic Workflow (`diagnostic_workflow.py`)**
   - Analyze historical answers and performance  
   - Update mastery scores  
   - Suggest next topics or review items

---

## 🧬 Memory & Personalization

Located in: `memory/`

Planned modules:

- `student_profile.py` – Basic info about a learner (goals, preferences)
- `mastery_tracker.py` – Topic-wise mastery scores and difficulty adaptation
- `spaced_repetition.py` – Scheduling when to review which topics/problems

Goal: over time, the tutor should **feel like it “remembers” you** and gives you the right next task at the right time.

---

## 📚 Synthetic Curriculum

Located in: `synthetic_curriculum/`

This will contain:

- Markdown explanations for each topic (e.g., recursion, sorting, graphs, DP)
- Worked-out synthetic examples (not copied from any course)
- Problem sets (stored as JSON or markdown tables)

Example modules (planned):

- `module_01_basics.md` – What is an algorithm? Basic notation  
- `module_02_complexity.md` – Big-O, Big-Theta, comparing growth  
- `module_03_recursion.md` – Recursive thinking and examples  
- `module_04_sorting.md` – Insertion sort, merge sort, quicksort (synthetic arrays)  
- `module_05_graphs.md` – BFS, DFS, shortest paths (synthetic graphs)  
- `module_06_dp.md` – Basic DP patterns (knapsack-style synthetic problems)

---

## 🛠️ Tech Stack

| Layer        | Technologies (Planned) |
|-------------|------------------------|
| Core Logic  | Python 3.x |
| LLM Access  | OpenAI API (config via `.env`) |
| Architecture | Multi-agent, ADK-inspired design |
| Backend     | Simple Python API or FastAPI (future) |
| Frontend    | Streamlit (starter), optional Flask + Tailwind later |
| Data        | JSON files for synthetic datasets & mastery data |
| Testing     | `pytest` |

---

## 🔐 Safety & Evaluation (Planned)

- Synthetic-only content (no real course materials)  
- Basic hallucination checks (e.g., verify code examples against tests)  
- Structured schemas for agent inputs/outputs  
- Test coverage for:
  - Agent behaviors  
  - Curriculum consistency  
  - Grading correctness  

Tests will live in: `tests/`

---
👤 Author

Created by NeuralByteJourney as a learning and portfolio project, inspired by the Agentic AI course and modern best practices for AI agents
