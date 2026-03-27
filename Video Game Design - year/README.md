# Video Game Design (Traditional Schedule) — Full Year Course Materials

A complete, standards-aligned Unity game development course for high school students. Built for a full academic year (36 weeks) meeting 5 days per week (180 total class sessions), covering Unity game development from the editor interface through capstone game project.

---

## Course Overview

| | |
|---|---|
| **Engine** | Unity (2022.3 LTS recommended) |
| **Language** | C# |
| **Duration** | 36 weeks · 5 days/week · 55 min/session |
| **Total Sessions** | 180 class days |
| **Standards** | Tennessee Video Game Design Standards (9-12.VGD.1–8) |
| **Units** | 8 |

---

## Folder Structure

Each unit folder contains the same set of materials:

```
Unit N - [Name]/
├── Daily Lesson Plans
    ├── Word/                   Daily lesson plan .docx files + unit assessment .docx
    ├── PDF/                    Daily lesson plan .pdf files + unit assessment .pdf
├── ReferenceGuide.md       Key concepts, C# syntax, Unity tips, common mistakes
├── UnitPractice.md         Practice challenges based on unit topics
├── UnitAssessment.md       Unit assessment with answer key
└── Daily Notes/            Complete student study guide materials
```

The root folder also contains `TN_VGD_Trad_Full_Year_Standards_Alignment.pdf` — a full-year standards mapping document.

---

## Getting Started — Installing Unity

Before students can create games, they need Unity and supporting tools set up. Here's what to do.

### On a Windows, Mac, or Linux Machine

1. **Download Unity Hub** — Free from [unity.com/download](https://unity.com/download)
   - Click "Download for [your OS]"
   - Follow the installer instructions

2. **Install Unity 2022.3 LTS** (Long Term Support)
   - Open Unity Hub
   - Go to **Installs** → **Install Editor**
   - Search for **2022.3 LTS** (Latest Stable Release)
   - Click **Install**
   - When prompted, install support for your target platform (Windows/Mac/Linux)

3. **Create a Unity Project**
   - Open Unity Hub
   - Go to **Projects** → **New Project**
   - Choose **2D** or **3D** template (depends on your game design)
   - Name your project and create

4. **Install Visual Studio Code** (for scripting)
   - Free from [code.visualstudio.com](https://code.visualstudio.com)
   - Install the **C# Dev Kit** extension from the VS Code marketplace

### On a Chromebook or Low-Spec Device

Unity does **not** run on Chromebooks or very low-spec devices. However, you have options:

- **School Laptops:** If available, this course requires traditional laptops (Windows, Mac, Linux)
- **Unity Play in Browser:** For simple 2D games, students can use [Unity Play](https://play.unity.com/) — a browser-based game creation tool (limited features, but good for small projects)
- **Alternative Game Engines:** Godot Engine (free, lightweight) runs on lower-spec machines if Unity is unavailable

**Note for your school:** If students don't have access to capable devices, coordinate with IT to ensure they have appropriate workstations for game development.

---

## Units at a Glance

| Unit | Title | Days | Class Days |
|------|-------|------|------------|
| 1 | Unity Interface & Game Design Thinking | 18 | 1–18 |
| 2 | C# Scripting Fundamentals | 25 | 19–43 |
| 3 | Physics & Collision | 22 | 44–65 |
| 4 | Player Controls & Input | 22 | 66–87 |
| 5 | Game Design Principles & UI | 20 | 88–107 |
| 6 | 2D Game Development | 25 | 108–132 |
| 7 | Game Systems & Enemies | 23 | 133–155 |
| 8 | Capstone Project | 25 | 156–180 |

---

## Unit Descriptions

### Unit 1 — Unity Interface & Game Design Thinking (Days 1–18)
Students are introduced to the Unity editor, navigating the Scene view, Hierarchy, Inspector, and Project folders. Topics: GameObjects, components, transforms, prefabs, and the fundamentals of game design thinking (player experience, core mechanics, themes). Extended instruction explores the design process and how constraints drive creativity. Ends with a "make a simple interactive scene" mini-project.

### Unit 2 — C# Scripting Fundamentals (Days 19–43)
Deep dive into C# syntax and Unity scripting. Topics: variables, data types, operators, control flow (`if`/`else`, `for`/`while` loops), functions, arrays, lists, and the MonoBehaviour lifecycle (`Awake`, `Start`, `Update`). Expanded practice reinforces object-oriented concepts, debugging, and writing clean, maintainable code. Ends with a data-management project.

### Unit 3 — Physics & Collision (Days 44–65)
Making objects interact with physics. Topics: Rigidbodies, gravity, forces, velocity, collision detection, OnCollisionEnter/OnTriggerEnter, raycasting, and 2D vs 3D physics. Extended exploration includes advanced force calculations, optimization, and complex multi-body interactions. Ends with a physics-based puzzle or arcade game.

### Unit 4 — Player Controls & Input (Days 66–87)
Translating player input into game actions. Topics: `Input.GetKey()`, `Input.GetMouseButtonDown()`, mapping controls, character movement, jumping, camera following, and state machines. Expanded instruction emphasizes responsive feel, polish, and accessibility. Ends with a playable character controller with smooth movement and animation.

### Unit 5 — Game Design Principles & UI (Days 88–107)
Designing engaging gameplay and professional user interfaces. Topics: the MDA framework (Mechanics, Dynamics, Aesthetics), Canvas and UI prefabs, TextMeshPro, buttons, sliders, health bars, pause menus, PlayerPrefs for saving/loading, audio systems, and particle effects. Extended practice includes flow state theory, difficulty curves, and complete UI systems. Ends with a game featuring a polished UI and sound design.

### Unit 6 — 2D Game Development (Days 108–132)
Building complete 2D games in Unity. Topics: 2D sprites, sprite sheets and animation, tile-based level design, cameras and parallax scrolling, sorting layers, 2D colliders, and 2D physics. Extended unit covers advanced techniques like procedural level generation and dynamic camera effects. Ends with a complete 2D platformer or top-down adventure game.

### Unit 7 — Game Systems & Enemies (Days 133–155)
Advanced systems that make games feel alive. Topics: enemy AI (patrol, chase, attack), state machines, coroutines and timers, spawn systems, power-ups and pickups, scoring and progression, and game state management. Expanded instruction emphasizes balance, challenge design, and emergent gameplay. Ends with a game featuring intelligent enemies and dynamic systems.

### Unit 8 — Capstone Project (Days 156–180)
Student-designed original game projects applying all skills. Topics: game design documents (GDD), project planning, bottom-up development, playtesting and iteration, code organization and documentation, polishing, and professional presentation. Students work independently or in small teams to design, develop, playtest, and present a complete original game. Ends with student presentations and peer evaluation.

---

## File Types Explained

### Daily Lesson Plans (Word & PDF)
One file per class session. Each lesson plan follows a consistent format:
- **Objective** — what students will be able to do by the end
- **Warm-Up** — brief review or hook activity
- **Direct Instruction** — new concept with code examples and visual demos
- **Guided Practice** — teacher-led Unity exercise
- **Independent Practice** — student coding/design challenges
- **Closure** — exit ticket or reflection

### Unit Assessments (Word and PDF)
Each unit includes a comprehensive assessment in two formats:
- **.docx / .pdf** — printable version for traditional testing

Assessment question types include multiple choice, short answer, coding challenges, and design questions.

### Daily Notes & Study Guides
Comprehensive materials for each day and unit, including:
- Unit overview and learning targets
- Day-by-day key concepts with annotated code examples
- Practice problems at three tiers (Beginner / Intermediate / Challenge)
- C# syntax reference and Unity API quick reference
- Common mistakes tables
- Vocabulary and concept definitions
- Code snippets for copy-paste learning

These are designed for student self-study, review, code reference, and test prep.

---

## Materials Count

| Material | Count |
|----------|-------|
| Daily lesson plan .docx files | 180 |
| Daily lesson plan .pdf files | 180 |
| Unit assessment .docx files | 8 |
| Unit assessment .pdf files | 8 |
| Unit reference guides | 8 |
| Unit practice banks | 8 |
| Daily notes/study guides | 180 |
| Standards alignment document | 1 (.pdf) |
| **Total files** | **~592** |

---

## Standards Alignment

All materials are aligned to the **Tennessee Video Game Design Standards** (grades 9–12). The full mapping is in `TN_VGD_Trad_Full_Year_Standards_Alignment.pdf` at the root of this folder. Key standard areas covered:

- **9-12.VGD.1:** Navigate the Unity development environment and apply game design principles
- **9-12.VGD.2:** Write C# scripts to implement game logic and interactive behavior
- **9-12.VGD.3:** Implement physics simulation and collision detection systems
- **9-12.VGD.4:** Design and implement responsive player control systems
- **9-12.VGD.5:** Apply game design principles and create user interface systems
- **9-12.VGD.6:** Develop complete 2D game environments using Unity's 2D toolset
- **9-12.VGD.7:** Implement advanced game systems including AI, saving, and game flow
- **9-12.VGD.8:** Design, develop, and present a complete original game project

---

## How to Use These Materials

**For daily instruction:** Open the `Word/Day N.docx` (or the matching PDF) for the current class session. Each lesson is self-contained and designed for a 55-minute period. Provide the corresponding "Daily Notes" file to students for reference and note-taking.

**For assessments:** Print the `.pdf` version from the `PDF/` folder, or use the `.docx` version to customize for your students.

**For student reference:** Share the unit's Daily Notes or ReferenceGuide with students — they're the go-to resources for understanding concepts, syntax, and common mistakes.

**For sub plans:** The PDF lesson plans are fully self-contained. A substitute can run any lesson directly from the PDF with no additional context needed.

**For capstone projects:** Unit 8 materials include comprehensive rubrics, self-assessment forms, and peer evaluation sheets to guide student projects from concept to presentation.

---

## Student Learning Outcomes

By the end of this course, students will be able to:

- **Navigate Unity** confidently and understand the relationship between GameObjects, components, and scenes
- **Write C# scripts** that implement game logic, including variables, control flow, functions, and object-oriented programming
- **Implement physics** systems including forces, collisions, and raycasting for interactive games
- **Design responsive player controls** with smooth movement, jumping, and camera following
- **Create engaging UIs** using Canvas, buttons, text, and state management with proper visual and audio feedback
- **Develop 2D games** including sprite animation, level design, and layered visual composition
- **Implement game systems** including enemy AI, scoring, progression, and win/lose conditions
- **Design and develop** an original game from concept through polished, presentable final product
- **Apply design principles** from MDA framework and flow state theory to create engaging, balanced gameplay
- **Document and present** their work professionally, explaining design choices and technical implementation

---

*Tennessee Video Game Design · Full Year (Traditional Schedule) · Course Materials*
