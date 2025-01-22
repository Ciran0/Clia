# Clia

## Table of Contents
1. [Problem and Context](#problem-and-context)  
   1.1. [Background](#11-background)  
   1.2. [The Gap in Existing Tools](#12-the-gap-in-existing-tools)  
   1.3. [Stakeholders and Their Objectives](#13-stakeholders-and-their-objectives)  
   1.4. [Key Challenges and Motivations](#14-key-challenges-and-motivations)  
   1.5. [Project Rationale](#15-project-rationale)  
2. [Identification of Major Agents](#identification-of-major-agents)  
   2.1. [Potential Clients and Their Roles](#21-potential-clients-and-their-roles)  
   2.2. [Tutors and Academic Support](#22-tutors-and-academic-support)  
   2.3. [Broader User Community (Future End Users)](#23-broader-user-community-future-end-users)  
   2.4. [Stakes and Functional Impact](#24-stakes-and-functional-impact)  
3. [Identification of Functionalities](#identification-of-functionalities)  
   3.1. [Basics](#31-basics)  
   3.2. [Making & Moving Plates](#32-making--moving-plates)  
   3.3. [Complex Plate Interactions](#33-complex-plate-interactions)  
   3.4. [Marking Resulting Features](#34-marking-resulting-features)  
   3.5. [Finishing & Exporting](#35-finishing--exporting)  
4. [Methodology, Organization of the Project](#methodology-organization-of-the-project)  
   4.1. [Minimum Viable Product (MVP)](#41-minimum-viable-product-mvp)  
   4.2. [Phases of Development](#42-phases-of-development)  
   4.3. [Agile Tooling](#43-agile-tooling)  
   4.4. [Flexibility and Risk Management](#44-flexibility-and-risk-management)  
5. [Position of the Solution](#position-of-the-solution)  
   5.1. [Existing Solutions: Strengths, Weaknesses, and Gaps](#51-existing-solutions-strengths-weaknesses-and-gaps)  
   5.2. [Why a New Solution?](#52-why-a-new-solution)  
   5.3. [Advantages of Developing a Dedicated New Tool](#53-advantages-of-developing-a-dedicated-new-tool)  
   5.4. [Conclusion: The Relevance of a New Solution](#54-conclusion-the-relevance-of-a-new-solution)  
6. [Technical Analysis](#technical-analysis)  
   6.1. [High-Level Architecture Overview](#61-high-level-architecture-overview)  
   6.2. [Back-End Layer (Django + HTMX)](#62-back-end-layer-django--htmx)  
   6.3. [3D Rendering & Front-End Visualization (Three.js)](#63-3d-rendering--front-end-visualization-threejs)  
   6.4. [High-Performance Geometry: Rust → WebAssembly](#64-high-performance-geometry-rust--webassembly)  
   6.5. [Supporting Tools & Methodologies](#65-supporting-tools--methodologies)  
   6.6. [Comparison of Final Stack vs. Potential Alternatives](#66-comparison-of-final-stack-vs-potential-alternatives)  
   6.7. [Justification of Each Final Choice](#67-justification-of-each-final-choice)  
   6.8. [Potential Limitations & Future Enhancements](#68-potential-limitations--future-enhancements)  
7. [Conception of the Solution](#conception-of-the-solution)  
8. [Validation Strategy](#validation-strategy)  
9. [Security & GDPR](#security--gdpr)

---

# Problem and Context

## 1.1 Background
In the realm of **worldbuilding**—whether for novels, role-playing games, video games, or academic exercises—map creation is a central and often **time-consuming** task. While many tools exist for drawing fantasy maps (e.g., Wonderdraft, Inkarnate), they typically focus on **visual design** without accounting for **geological plausibility**. Meanwhile, **scientific-grade** programs, such as **GPlates**, are powerful for modeling real-world tectonic data but can be intimidating or cumbersome for creative users who want to craft entirely new planets.

## 1.2 The Gap in Existing Tools
- **GPlates**: A professional-level application for **real** plate tectonics. Extremely powerful but geared toward Earth’s data and workflows, making it too technical for many creative users.  
- **Fantasy map tools** (Wonderdraft, Inkarnate): Great for artistic design, but lack any **geophysical realism** such as subduction zones or mountain-building from collisions.

Hence, there is a **gap**: a **user-friendly** yet **technically grounded** application that helps **worldbuilders** generate maps with a **solid geological foundation**—complete with cratons, continental drift, collision events, subduction zones, etc.

## 1.3 Stakeholders and Their Objectives
1. **Worldbuilders (Primary Users)**  
   - **Objective**: Craft imaginary worlds with realistic tectonic motion and landforms.  
   - **Challenge**: Must be able to **draw** and **animate** plates easily, without deep knowledge of real-world geophysics.

2. **Geology Enthusiasts / Educators**  
   - **Objective**: Demonstrate or teach plate tectonics in a more playful, interactive tool.  
   - **Challenge**: Existing professional software can be overkill or too complex for introductory lessons.

3. **Software / Game Developers**  
   - **Objective**: Integrate realistic planet generation into their engines or interactive stories.  
   - **Challenge**: Need an **exportable** system (meshes, images, data) that can plug into their pipelines.

4. **The Student / Project Owner**  
   - **Objective**: Deliver a final-year project (TFE) that addresses this unmet need, bridging **scientific** and **creative** requirements.  
   - **Challenge**: Must demonstrate the capacity to analyze the context, plan the architecture, justify design choices, and produce a workable prototype.

## 1.4 Key Challenges and Motivations
- **Accessibility vs. Scientific Rigor**: Balancing a **user-friendly** interface with enough **realism** to produce valid geologic results.  
- **Technical Complexity**: Handling **spherical geometry**, plate rotations, splitting/merging polygons, and time-based animation.  
- **Performance**: Ensuring the application can run smoothly **in the browser**, even with large data sets or complex plate boundaries.  
- **Data Management**: Storing multiple timelines, user-drawn plates, or collisions.  
- **User Engagement**: Making the system **intuitive**, encouraging iterative drawing and experimentation with minimal learning curve.

## 1.5 Project Rationale
The **lack of a specialized tool** for **imaginative geologic modeling** presents a unique opportunity to:
- **Simplify** advanced scientific tools (like GPlates) into a **streamlined** web app suited for non-experts.  
- Provide an **educational bridge** between fantasy creation and real science, **enriching** fictional settings while maintaining internal consistency.  
- Demonstrate strong **engineering skills** in both **software architecture** (Django, HTMX, Rust→WASM) and **geometric computations** (plate tectonics on a sphere).

By designing and implementing this tool, we aim to **empower creators** to produce **scientifically plausible** worlds, benefiting both academic and creative communities.

---

# Identification of Major Agents

## 2.1 Potential Clients and Their Roles

| **Potential Client**        | **Background**                                                       | **Interest & Status**                                                                                                             |
|-----------------------------|-----------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------|
| **Artifexian (YouTuber)**   | Produces worldbuilding, cartography, and conlang videos              | Showed interest in a fictional plate-tectonics tool but currently inactive. Might become a “client” once a working prototype exists |
| **WorldbuildingPasta**      | Blogger focused on advanced worldbuilding (tectonics, GPlates tips)  | Enthusiastic but wants more details. May serve as an expert consultant or user validating scientific credibility once the scope is clearer |

**The Student (Me) – Actual Client for Now**  
- Acts as both **developer** and **client**, shaping the project to meet academic and personal expectations.  
- Aims to create a proof of concept that can eventually incorporate external stakeholder feedback.

## 2.2 Tutors and Academic Support

1. **School’s Math Teacher (Tutor)**  
   - **Expertise**: Advanced mathematics (geometry, spherical trigonometry).  
   - **Role**: Ensures **mathematical correctness** (Euler rotations, polygon intersections).  
   - **Impact**: Guides formula verification and numeric stability.

2. **School’s Web Developer Teacher (Tutor)**  
   - **Expertise**: Full-stack web dev (Django, WebAssembly, front-end best practices).  
   - **Role**: Advises on architecture, performance, and security.  
   - **Impact**: Aligns project with modern web standards and helps debug server/WASM integration issues.

## 2.3 Broader User Community (Future End Users)
- **Worldbuilding Enthusiasts** (writers, RPG GMs)  
- **Educators / Students** learning plate tectonics.  
- **Indie Game Developers** needing realistic planet data.

## 2.4 Stakes and Functional Impact
- **Project Viability**: My progress will determine if external contributors (Artifexian, WorldbuildingPasta) become more involved.  
- **Quality of Features**: Tutors influence mathematical accuracy and usability.  
- **Scientific Credibility**: Approval from known worldbuilders could enhance the tool’s reputation.  
- **Timeline**: Must balance external feedback with final-year academic milestones.

---

# Identification of Functionalities

Below are the **key features** needed to replicate (and improve upon) GPlates-like functionality, framed as **user stories** with acceptance criteria.

## 3.1 Basics

### Startup & Project Creation
> “As a user, I want to initialize a new tectonic project so I can begin designing a planet’s geologic timeline from scratch.”

**Acceptance Criteria**:  
- Create a new project (with optional custom radius).  
- Name the project and store it in a dedicated folder.  
- Display a blank 3D globe (Three.js).  
- Timescale settings (e.g. 2000 Ma to 0 Ma) to define the timeline range.

### Timescale Management
> “As a user, I want to define a timescale in millions of years to reconstruct plate movement from a starting geologic point.”

**Acceptance Criteria**:  
- A timescale bar or input to set start/end times.  
- A slider or numeric field to jump to specific times.  
- Globe updates to show plate positions (once plates exist).

### Creating Initial Continents (Supercontinent)
> “As a user, I want to create polygonal features on the globe so I can define my initial supercontinent layout.”

**Acceptance Criteria**:  
- Draw polygons (click to place vertices).  
- Each polygon has a feature type (e.g., Craton, ContinentalCrust) and unique Plate ID.  
- Color-coded by Plate ID; editable vertices.  
- Stored in the project.

### Saving the Project
> “As a user, I want to save my current project data so I can reopen it later.”

**Acceptance Criteria**:  
- A ‘Save Project’ action storing feature collections, rotation data, etc.  
- Reloading the project restores the globe state.

---

## 3.2 Making & Moving Plates

### Defining Rifts
> “As a user, I want to draw a rift line across a continent so it can split into two separate plates.”

**Acceptance Criteria**:  
- Ability to create a ‘rift’ (polyline) with a specified start time.  
- Splits the affected polygon(s) into two new polygons, each possibly with a new Plate ID.

### Splitting a Feature (Continent)
> “As a user, I want to split an existing polygon along the rift line so each side can move independently.”

**Acceptance Criteria**:  
- System clones the original polygon into two polygons.  
- Original polygon ends at rift time; new polygons begin at that time.

### Managing Plate Rotations (Euler Poles)
> “As a user, I want to define rotation parameters over time so plates can drift realistically.”

**Acceptance Criteria**:  
- User can set plate rotation axes/angles at specific timestamps.  
- The system interpolates positions for continuous motion.  
- Rotations stored in a back-end structure.

### Moving Plates Over Time
> “As a user, I want to move plates step-by-step so I can visualize continental drift.”

**Acceptance Criteria**:  
- Timeline increments (e.g. 50 My).  
- Reposition plates via 3D controls.  
- Automatic data updates; optional playback mode.

### Flowlines (Mid-Ocean Basins)
> “As a user, I want to generate flowlines showing new oceanic crust forming at diverging boundaries.”

**Acceptance Criteria**:  
- User selects plates + time interval.  
- Multi-point flowlines appear, updating when plate motion changes.

### Adding Ocean Crust
> “As a user, I want to fill newly opened gaps with ‘OceanicCrust’ polygons.”

**Acceptance Criteria**:  
- Polygons labeled as OceanicCrust.  
- Start time matches the formation step.  
- Assigned to the appropriate Plate ID.

### Subduction Zones & Island Arcs
> “As a user, I want to mark convergent boundaries and generate island arcs.”

**Acceptance Criteria**:  
- Draw a polyline for subduction zone.  
- Island arcs form behind the trench after some delay.  
- Arcs share the overriding plate’s ID.

---

## 3.3 Complex Plate Interactions

### Importing Custom Rasters
> “As a user, I want to overlay an equirectangular image on the globe for reference.”

**Acceptance Criteria**:  
- Upload an image.  
- Overlay toggles (opacity, visibility).  
- Aids in aligning features to real or custom maps.

### Splitting Co-Moving Plates
> “As a user, I want to rift two plates that used to move as one.”

**Acceptance Criteria**:  
- Draw a rift.  
- System splits polygons, updates the rotation data.  
- One part keeps the old plate motion; the other gets a new ID.

### Creating Entirely New Plates
> “As a user, I want to define a new microplate from an existing land or ocean region.”

**Acceptance Criteria**:  
- User selects a region, chooses a new Plate ID, sets time.  
- Baseline rotation entries are created.  
- Updated polygons belong to the new plate from that time onward.

### Subducting Ocean Crust & Collisions
> “As a user, I want to mark where older ocean crust subducts or where plates collide.”

**Acceptance Criteria**:  
- New subduction lines in the ocean.  
- Retire polygons once fully subducted.  
- Collisions cause overlapping polygons to be merged or adjusted.

### Splitting Plates After Collision
> “As a user, I want to form new rifts along old collision sutures.”

**Acceptance Criteria**:  
- Rifts drawn along collision lines.  
- Polygons are partially split.  
- Rotation data updated for new plate motion.

---

## 3.4 Marking Resulting Features

### Orogenies (Mountain Belts)
> “As a user, I want to place orogenies (mountain belts) along convergent boundaries.”

**Acceptance Criteria**:  
- User selects subduction/collision boundary.  
- The system records start time for the orogeny.  
- Orogenies can become “former” after a set time.

### Large Igneous Provinces (LIPs)
> “As a user, I want to mark brief episodes of large igneous outpourings.”

**Acceptance Criteria**:  
- Create a polygon labeled “LargeIgneousProvince.”  
- Defined start/end times.  
- Marked as “former LIP” once ended.

### Hotspots & Island Chains
> “As a user, I want stationary hotspots under the crust to generate volcanic island chains.”

**Acceptance Criteria**:  
- Place a hotspot point (lat/long).  
- A motion path forms as plates drift over the hotspot.  
- Island polygons can be placed at each timestep along this path.

### Mid-Ocean Ridges & Plate Topologies
> “As a user, I want to mark mid-ocean ridges and auto-generate a closed plate boundary.”

**Acceptance Criteria**:  
- Define a “MidOceanRidge” polyline.  
- The system builds/updates a plate topology from rifts, subduction zones, ridges.  
- Boundaries evolve as user changes plate configurations.

---

## 3.5 Finishing & Exporting

### Final Display Adjustments
> “As a user, I want to toggle/hide features to produce a clear map.”

**Acceptance Criteria**:  
- Layers panel for show/hide (continents, orogenies, hotspots, etc.).  
- Opacity controls.  
- Option to remove lat/long grid or switch projection.

### Exporting Maps & Timelapse
> “As a user, I want to export snapshots or timelapses of the planet’s tectonic evolution.”

**Acceptance Criteria**:  
- Single snapshot exports (image/vector).  
- Time-sequence exports (e.g., every 10 My).  
- Common projections (Equirectangular, Mollweide) or 3D globe.  
- Preserves layer colors and time-based geometry.

---

# Methodology, Organization of the Project

## 4.1 Minimum Viable Product (MVP)
This **MVP** ensures that all major layers (Django, HTMX, Rust→WASM, Three.js) function together:

1. **3D Globe Visualization**  
   - Basic globe in Three.js (orbit, zoom).  
   - Minimal visual theme.

2. **Polygon Drawing & Storage**  
   - Draw polygonal features on the globe.  
   - Store data (coords, plate ID) in Django.  
   - Basic create/delete operations.

3. **Translation & Rotation of Polygons**  
   - Select a polygon to **translate** or **rotate** on the globe.  
   - Rust→WASM handles geometry calculations, returning updated vertices.  
   - Immediate feedback in the 3D scene.

4. **Project Management**  
   - Create and name multiple projects.  
   - Each project can have multiple polygons.  
   - Load/save projects in the DB.

5. **Basic UI & HTMX**  
   - Partial updates for data changes.  
   - Avoid full-page reloads; everything integrated in a fluid web interface.

## 4.2 Phases of Development

### Phase 1: Project Setup & MVP Definition
- **Goals**: 
  - Repo structure on GitHub, Django + HTMX skeleton, Rust→WASM toolchain, minimal Three.js globe, etc.  
  - Document the MVP scope in GitHub issues.

### Phase 2: MVP Implementation
- **Goals**: 
  - Implement polygon drawing on the globe, storing to DB.  
  - Connect Rust→WASM for basic rotations.  
  - Basic UI for project management.

### Phase 3: Core Tectonic Features
- **Goals**: 
  - Rifting, polygon splitting, subduction, collisions (basic).  
  - Interactive timeline or rotation controls.  
  - Validate data flow and geometry.

### Phase 4: Feedback, Polishing & Extended Features
- **Goals**:
  - Gather input from WorldbuildingPasta / Artifexian if possible.  
  - Optimize performance.  
  - Add advanced geometry (flowlines, orogenies), map exporting, etc.

### Phase 5: Finalization & Documentation
- **Goals**: 
  - Wrap up features, fix bugs.  
  - Comprehensive documentation and user guide.  
  - Final testing and demonstration.

## 4.3 Agile Tooling

- **Git + GitHub**:  
  - Branching, pull requests, issues, GitHub Projects.  
- **Clockify (Optional)**:  
  - Time tracking for productivity if helpful.  
- **Frequent Commits & Iteration**:  
  - Each phase yields a working build.  
  - Re-prioritize tasks as needed.

## 4.4 Flexibility and Risk Management
- **Agile, incremental** approach allows re-scoping if complexities arise (math, performance).  
- MVP ensures a baseline deliverable; phases accommodate new ideas or user feedback.

---

# Position of the Solution

## 5.1 Existing Solutions: Strengths, Weaknesses, and Gaps

Use this **comparison table** for a quick overview:

| **Tool**           | **Focus**       | **Strengths**                                                    | **Weaknesses**                                                                                                         |
|--------------------|-----------------|------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|
| **GPlates**        | Scientific, Earth-based plate reconstructions | - Accurate for real Earth<br>- Powerful advanced features        | - Complex UI<br>- Steep learning curve<br>- Earth-centric<br>- Not art-oriented                                         |
| **Artistic Tools** (Wonderdraft, Inkarnate) | Fantasy map drawing | - Very easy to use<br>- Beautiful output, many assets           | - No geophysical realism<br>- 2D-only<br>- No plate animation                                                           |
| **Blender**        | 3D modeling & animation                        | - Extremely flexible<br>- Professional rendering                 | - No native tectonic logic<br>- High learning curve<br>- Manual rigging for plate motions                               |

## 5.2 Why a New Solution?
- **GPlates** is scientific but too specialized for imaginary worlds.  
- **Artistic Tools** are visually appealing but lack tectonic realism.  
- **Blender** can do anything in 3D but lacks built-in geologic processes.

A **hybrid approach** is needed: an intuitive “draw-and-animate” tool with core geoscience logic.

## 5.3 Advantages of Developing a Dedicated New Tool
1. **User-Centric Interface** (simple “draw & move” approach).  
2. **Focus on Fictional Workflows** (imagined tectonic histories, quick plate splits).  
3. **Dynamic Evolution** (animate entire planet histories).  
4. **Web-Based Integration** (Django, HTMX, Rust→WASM).  
5. **Community Involvement** (lower barrier than GPlates for hobbyists).

## 5.4 Conclusion: The Relevance of a New Solution
A **custom** application merges **intuitive map creation** with **authentic tectonic logic**, bridging the gap between specialized scientific software and purely artistic tools. It’s more than a novelty—serving as a platform for **learning**, **experimentation**, and **collaboration** in fictional geoscience.

---

# Technical Analysis

## 6.1 High-Level Architecture Overview
We need a browser-based solution that:
1. **Renders a 3D globe** (Three.js) for interactive plate drawing.  
2. **Computes geometry** in Rust→WASM for performance.  
3. **Stores data** in Django, employing HTMX for partial page updates.  
4. **Scales** with agile increments.

## 6.2 Back-End Layer (Django + HTMX)
A Python-based framework for robust data handling and quick partial updates:
- **Django**: Admin, ORM, security.  
- **HTMX**: Enables partial HTML updates with minimal JavaScript overhead.

## 6.3 3D Rendering & Front-End Visualization (Three.js)
- **Three.js** for an interactive 3D globe.  
- Large community, flexible scene management, easy to integrate with HTML/JS.

## 6.4 High-Performance Geometry: Rust → WebAssembly
- **WebAssembly** for near-native performance in numeric tasks.  
- **Rust** ensures memory safety and strong tooling.  
- Handles polygon splitting, Euler rotations, collisions, etc.

## 6.5 Supporting Tools & Methodologies
- **Database & ORM**: Likely PostgreSQL for multi-user or advanced queries.  
- **Synchronous Django** acceptable for a single-user or small group.  
- **Security**: Django’s built-in session/auth + standard web best practices.

## 6.6 Comparison of Final Stack vs. Potential Alternatives

| **Layer**         | **Chosen**                         | **Alternatives**                            | **Reason**                                                 |
|-------------------|------------------------------------|---------------------------------------------|------------------------------------------------------------|
| Back End          | Django + HTMX                      | Flask, FastAPI, Node.js                     | Built-in admin, robust security, partial updates w/ HTMX.  |
| Front End         | Three.js + minimal JS + HTMX        | React/Vue SPAs, Babylon.js, CesiumJS        | Straightforward 3D rendering, no heavy SPA needed.         |
| Geometry          | Rust → WASM                        | C/C++ → WASM, AssemblyScript, Go → WASM     | Safe concurrency, performance, mature Rust→JS ecosystem.   |
| 3D Visualization  | Three.js                           | Babylon.js, raw WebGL, other 3D engines     | Large community, flexible, examples for custom geometry.   |

## 6.7 Justification of Each Final Choice
1. **Django + HTMX**: Quick to set up, proven reliability, partial updates.  
2. **Rust → WASM**: Safe, high-performance math for plate-tectonic logic.  
3. **Three.js**: Well-documented 3D library for a custom globe approach.  

## 6.8 Potential Limitations & Future Enhancements
- **Large Data Sets**: Could require LOD strategies.  
- **Collaboration**: Real-time might need Django Channels or websockets.  
- **WebGPU**: Future improvement for massive polygons or advanced rendering.

---

# Conception of the Solution


---

# Validation Strategy
1. **User Types**: Validate with beginner worldbuilders vs. advanced tectonics enthusiasts.  
2. **Precision & Relevance**: Ensure plausible geophysics but not necessarily at the highest geoscientific detail.  
3. **Complexity**: Focus on correct polygon splitting/animation first, advanced processes next.  
4. **Priority**: MVP core (draw polygons, define plates, animate them), then secondary features (flowlines, orogenies).

---

# Security & GDPR
- **User Data**: Only minimal user info (e.g., logins) plus project data (polygons, timestamps).  
- **Protection**: Django’s default CSRF, session security, HTTPS.  
- **GDPR Considerations**: If storing personal data, provide user consent forms, data deletion on request, and relevant disclaimers.
