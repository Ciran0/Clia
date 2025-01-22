Clia

# Problem and Context

## 1. Background
In the realm of **worldbuilding**—whether for novels, role-playing games, video games, or academic exercises—map creation is a central and often **time-consuming** task. While many tools exist for drawing fantasy maps (e.g., Wonderdraft, Inkarnate), they typically focus on **visual design** without accounting for **geological plausibility**. Meanwhile, **scientific-grade** programs, such as **GPlates**, are powerful for modeling real-world tectonic data but can be intimidating or cumbersome for creative users who want to craft entirely new planets.

## 2. The Gap in Existing Tools
- **GPlates** stands out as a professional-level application that offers plate-tectonic reconstruction, subduction modeling, rifting, and more. However, it was designed for **Earth’s** geologic data and workflows, and its interface can feel too technical for a writer or game designer seeking to develop an **imaginary** planet.
- **Fantasy map tools** let creators paint landscapes freely but lack any genuine geophysical mechanics. This leads to **unrealistic geographies** and can break immersion for readers or players who value internal consistency.

Hence, there is a **gap**: a **user-friendly** yet **technically grounded** application that helps **worldbuilders** generate maps with a **solid geological foundation**—complete with cratons, continental drift, collision events, subduction zones, etc.

## 3. Stakeholders and Their Objectives
1. **Worldbuilders (Primary Users)**  
   - **Objective**: Craft imaginary worlds with realistic tectonic motion and landforms.  
   - **Challenge**: Must be able to **draw** and **animate** plates easily without deep knowledge of real-world geophysics.

2. **Geology Enthusiasts / Educators**  
   - **Objective**: Demonstrate or teach plate tectonics via a more playful, interactive tool.  
   - **Challenge**: Existing professional software can be overkill or too complex for introductory lessons.

3. **Software / Game Developers**  
   - **Objective**: Integrate realistic planet generation into their engines or interactive stories.  
   - **Challenge**: Need an **exportable** system (meshes, images, data) that can plug into their pipelines.

4. **The Student / Project Owner**  
   - **Objective**: Deliver a final-year project (TFE) that addresses this unmet need, bridging **scientific** and **creative** requirements.  
   - **Challenge**: Must demonstrate the capacity to analyze the context, plan the architecture, justify design choices, and produce a workable prototype.

## 4. Key Challenges and Motivations
- **Accessibility vs. Scientific Rigor**: Balancing a **user-friendly** interface with enough **realism** to produce valid geologic results.  
- **Technical Complexity**: Handling **spherical geometry**, plate rotations, splitting/merging polygons, and time-based animation.  
- **Performance**: Ensuring the application can run smoothly **in the browser**, even with large data sets or complex plate boundaries.  
- **Data Management**: Storing multiple timelines, user-drawn plates, or collisions.  
- **User Engagement**: Making the system **intuitive**, encouraging iterative drawing and experimentation with minimal steep learning curve.

## 5. Project Rationale
The **lack of a specialized tool** for **imaginative geologic modeling** presents a unique opportunity to:
- **Simplify** advanced scientific tools (like GPlates) into a **streamlined** web app suited for non-experts.  
- Provide an **educational bridge** between fantasy creation and real science, thus **enriching** fictional settings while maintaining internal consistency.  
- Demonstrate strong **engineering skills** in both **software architecture** (Django, HTMX, Rust→WASM) and **geometric computations** (plate tectonics on a sphere).

By designing and implementing this tool, we aim to **empower creators** to produce **scientifically plausible** worlds, benefiting both academic and creative communities.

# Identification of major agents

## Identification of Stakeholders

### 1. Potential Clients and Their Roles

1. **Artifexian (YouTuber) – Potential Client**  
   - **Background**: A content creator who produces videos about worldbuilding, map creation, and conlanging.  
   - **Interest**: Initially expressed curiosity about a plate-tectonics tool for fictional worlds but has not responded since the project started.  
   - **Status**: Currently inactive. May provide valuable feedback or function as a formal “client” once the project has a more concrete prototype.

2. **WorldbuildingPasta (Blogger) – Potential Client**  
   - **Background**: Runs a blog focused on advanced worldbuilding topics, including tectonics and GPlates tutorials.  
   - **Interest**: Showed enthusiasm but requires more detailed information before investing time.  
   - **Status**: Waiting for further progress and clearer scope to decide on involvement. Might eventually serve as an expert consultant or user who can validate the scientific credibility of the application.

3. **The Student (me) – Actual Client for Now**  
   - **Role**: Both the developer and the current “client” ensuring the project meets my own expectations and academic requirements.  
   - **Motivation**: Needs a final-year project that showcases skills in software development, mathematics, and domain analysis.  
   - **Goal**: Deliver a working proof of concept that can later be refined with feedback from external stakeholders (e.g., Artifexian, WorldbuildingPasta).

### 2. Tutors and Academic Support

1. **School’s Math Teacher (Tutor)**  
   - **Expertise**: Advanced mathematics, especially geometry, spherical trigonometry, and possibly geophysics.  
   - **Role**: Helps ensure the **mathematical correctness** of the plate-tectonic models (Euler rotations, polygon intersections on a sphere, etc.).  
   - **Impact**: Provides guidance, verifies formulas, and assists in problem-solving for complex geometry or numeric stability.

2. **School’s Web Developer Teacher (Tutor)**  
   - **Expertise**: Full-stack web development, including **Django**, **WebAssembly**, front-end best practices.  
   - **Role**: Advises on architectural choices, ensures best practices for performance and security, supports debugging server-side or WASM integration issues.  
   - **Impact**: Offers feedback on code structure and helps align the project with modern web standards.

### 3. Broader User Community (Future End Users)

Even though the project has no large user base yet, the broader **target audience** includes:

- **Worldbuilding Enthusiasts**: Writers, RPG game masters, or artists who need realistic planet formation.  
- **Educators / Students**: Those wanting a more intuitive tool than GPlates to learn or teach plate tectonics.  
- **Indie Game Developers**: Potentially interested in integrating or exporting realistic maps for game worlds.

### 4. Stakes and Functional Impact

- **Project Viability**: As I am currently the main driving force (and client), consistent progress will determine whether external contributors (Artifexian, WorldbuildingPasta) join later.  
- **Quality of Features**: The mathematic and web dev tutors can heavily influence **accuracy** (mathematical integrity) and **usability** (website performance, front-end design).  
- **Scientific Credibility**: Should the project eventually receive feedback from WorldbuildingPasta or Artifexian, their approval could strengthen the tool’s reputation in the broader worldbuilding community.  
- **Timeline**: Because this is a final-year project, academic milestones and tutor evaluations are critical. External feedback must be balanced with the school’s requirements and deadlines.

### Summary

At this stage, **I** am the only official “client” and decision-maker. Two **potential external clients** (Artifexian and WorldbuildingPasta) have shown interest but are on hold, pending clearer project scope and a functioning prototype. My **two school tutors** act as domain/technical mentors, ensuring academic rigor in both **mathematics** and **web development**.

Through these roles, the project aims to satisfy **academic standards** (demonstrating advanced technical and analytical competencies) while laying the groundwork for **future collaboration** with recognized worldbuilding figures once the prototype is compelling enough for them to invest their time.

# Identification of Functionalities

Below are the **key features** we need in order to match (and improve upon) the GPlates functionality for creating, editing, and animating tectonic plates for an imaginary world. Each feature is presented in **user story** format, with acceptance criteria.

## 1. BASICS

### 1.1 Startup & Project Creation
**User Story**:  
> “As a user, I want to initialize a new tectonic project so that I can begin designing a planet’s geologic timeline from scratch.”

- **Acceptance Criteria**:  
  - The system allows creating a new project with a chosen planetary radius or default Earth-like radius.  
  - The user can name the project and store it in a dedicated folder or workspace.  
  - A “blank globe” is presented in 3D via Three.js; no features yet exist.  
  - The project settings include a timescale range (e.g., from 2000 Ma to 0 Ma) to define the maximum “past” and “future” timeline scope.

### 1.2 Timescale Management
**User Story**:  
> “As a user, I want to define a timescale (in millions of years) so that I can reconstruct plate movement from a chosen geologic starting point up to the present (or future).”

- **Acceptance Criteria**:  
  - A timescale bar or input field to set the start (e.g. 2000 Ma) and end (0 Ma or beyond).  
  - A timeline slider or typed input that allows the user to jump to specific times.  
  - The system updates the 3D globe to show plate positions for the specified time (once plates exist).  

### 1.3 Creating Initial Continents (Supercontinent)
**User Story**:  
> “As a user, I want to create polygonal features (cratons or continental crust) on the globe so that I can define my initial supercontinent layout.”

- **Acceptance Criteria**:  
  - Ability to “draw” polygons (e.g., left-click to place vertices) directly on the 3D globe or on a 2D projection.  
  - Each polygon has a “Feature Type” (e.g., Craton, ContinentalCrust) and a unique “Plate ID” (other than 0).  
  - Polygons are color-coded by their Plate ID.  
  - The user can edit vertices (move, insert, delete) before finalizing the polygon.  
  - Once saved, the polygon is stored in the project.  

### 1.4 Saving the Project
**User Story**:  
> “As a user, I want to save my current project’s data so that I can reopen it later without losing progress.”

- **Acceptance Criteria**:  
  - A ‘Save Project’ action that stores all feature collections (cratons, continents, etc.) and any rotation data to the server/database.  
  - The project can be loaded later, restoring the globe view, polygon features, timescale settings, etc.

## 2. MAKING & MOVING PLATES

### 2.1 Defining Rifts
**User Story**:  
> “As a user, I want to draw a rift line (polyline) across a continent so that I can split one landmass into two separate plates.”

- **Acceptance Criteria**:  
  - Ability to create a ‘rift’ feature by drawing a polyline.  
  - The user can specify the time at which the rift appears (the “start time” of the rift).  
  - The rift belongs to an ‘immobile’ or neutral plate ID (e.g., 1) or can be tied to a specific plate if desired.  
  - Once the user finalizes the rift line, the system can split the affected continent polygon(s) into two new polygon features—one on each side of the rift.

### 2.2 Splitting a Feature (Continent)
**User Story**:  
> “As a user, I want to split an existing polygon (e.g., a supercontinent) along the rift line so that each side can move independently.”

- **Acceptance Criteria**:  
  - The system clones the original polygon into two separate polygons.  
  - Each resulting polygon can be assigned new or existing Plate IDs.  
  - The original polygon either ends at the time of rifting or is marked as replaced by these two new polygons.  

### 2.3 Managing Plate Rotations (Euler Poles / Rotation File)
**User Story**:  
> “As a user, I want to define and store the rotation parameters (Euler poles) for each plate over time so that plates can drift realistically.”

- **Acceptance Criteria**:  
  - The user can set or adjust a plate’s rotation axis (pole) and rotation angle at a specific time.  
  - The system interpolates plate positions between defined time-steps, displaying continuous motion.  
  - Rotations are stored in a back-end data structure (akin to a ‘rotation file’) that can be reloaded.  
  - The user can see or edit these rotation entries (time, lat, lon, angle) in a UI.

### 2.4 Moving Plates Over Time
**User Story**:  
> “As a user, I want to move plates step by step through time so that I can visualize how continents drift and reconfigure.”

- **Acceptance Criteria**:  
  - The timeline can be advanced in increments (e.g., 50 My or user-defined).  
  - At each increment, the user can reposition a plate using interactive 3D controls (rotate around a chosen pole).  
  - The software updates the stored rotation data automatically.  
  - A “playback” mode animates plate motion from the earliest time to the present.  

### 2.5 Flowlines (Mid-Ocean Basins)
**User Story**:  
> “As a user, I want to generate flowlines that trace how new oceanic crust forms between diverging plates so that I can see the mid-ocean ridge spreading pattern.”

- **Acceptance Criteria**:  
  - The user can select two diverging plates and the time interval.  
  - The system generates multi-point “flowlines” showing the progressive opening of the ocean basin.  
  - Flowlines update automatically when plate motion changes.  

### 2.6 Adding Ocean Crust
**User Story**:  
> “As a user, I want to fill newly opened gaps between diverging plates with ‘OceanicCrust’ polygons so that the ocean basin is visually defined.”

- **Acceptance Criteria**:  
  - Where flowlines indicate new ocean floor, the user can generate or draw a polygon labeled OceanicCrust.  
  - The polygon has a start time that matches the formation step.  
  - Each ocean crust polygon is assigned the Plate ID of whichever side it belongs to (or split if needed).  

### 2.7 Subduction Zones & Island Arcs
**User Story**:  
> “As a user, I want to mark convergent boundaries (subduction zones) so that I can visualize where oceanic crust is subducting and generate island arcs.”

- **Acceptance Criteria**:  
  - Draw or define a polyline for the subduction zone with a start time.  
  - The subduction zone belongs to the overriding plate’s ID.  
  - An ‘island arc’ polygon can be formed one timestep after the subduction zone appears, behind the trench line.  
  - Island arcs are assigned to the same plate ID as the subduction zone.

## 3. COMPLEX PLATE INTERACTIONS

### 3.1 Importing Custom Rasters
**User Story**:  
> “As a user, I want to import image layers (rasters) onto the globe so that I can trace or align my tectonic features with external maps or references.”

- **Acceptance Criteria**:  
  - The user can upload an equirectangular image or other recognized projection.  
  - The system can overlay that raster on the 3D globe.  
  - The user can toggle raster visibility or opacity to help with drawing tectonic boundaries.

### 3.2 Splitting Co-Moving Plates
**User Story**:  
> “As a user, I want to rift two ‘co-moving’ cratons or continents apart that previously shared the same motion so that they can move independently from a certain time onward.”

- **Acceptance Criteria**:  
  - A rift line can be drawn.  
  - The system splits any shared plate polygons crossing that rift.  
  - Updates the rotation data so that one part keeps the old plate’s motion, and the other part is given a new or separate Plate ID that can move differently after the split.

### 3.3 Creating Entirely New Plates
**User Story**:  
> “As a user, I want to create a new plate in the middle of the ocean or land so that previously uniform crust can become an independent microplate.”

- **Acceptance Criteria**:  
  - The user can select a region of crust, define a new Plate ID, and set a time it becomes ‘independent.’  
  - The rotation file auto-generates baseline entries for the new plate.  
  - Polygons are updated so that the newly defined region belongs to the new plate from that point onward.

### 3.4 Subducting Ocean Crust & Collisions
**User Story**:  
> “As a user, I want to mark where older ocean crust subducts or where plates collide so that I can keep track of the consumption of ocean floor and formation of collisions.”

- **Acceptance Criteria**:  
  - The user can define new subduction lines in the ocean.  
  - If a plate is fully subducted, the user can retire its polygons at the time they vanish.  
  - Colliding continents must be “deformed” at the boundary (the system merges or adjusts polygons so they no longer overlap).  

### 3.5 Splitting Plates After Collision
**User Story**:  
> “As a user, I want to be able to form new rifts in the suture zone of collided continents so that old collision lines can later become new weak zones and re-rift.”

- **Acceptance Criteria**:  
  - Rifts can be drawn roughly along old suture lines.  
  - The system splits or partially splits any polygon (continent or orogeny) along that line.  
  - Rotation data is updated so that the newly separated region can have its own motion after the collision.

## 4. MARKING RESULTING FEATURES

### 4.1 Orogenies (Mountain Belts)
**User Story**:  
> “As a user, I want to place orogenies (mountain belts) along convergent boundaries so that the planet’s mountainous terrain is clearly defined.”

- **Acceptance Criteria**:  
  - The user can select a subduction zone or collision boundary and define a polygon that represents the mountain belt.  
  - The system records the orogeny’s start time (when the subduction or collision began).  
  - “Active orogenies” can be converted to “former” or “old orogenies” when a set amount of time passes or the collision ends.

### 4.2 Large Igneous Provinces (LIPs)
**User Story**:  
> “As a user, I want to mark LIP events on continents so that I can record major volcanic outpourings that create new igneous plateaus.”

- **Acceptance Criteria**:  
  - The user can create a polygon labeled “LargeIgneousProvince” with a defined start time and short duration (e.g., 10 My).  
  - The LIP polygon belongs to the plate it appears on.  
  - After the LIP event ends, the user can mark it as “former LIP.”  

### 4.3 Hotspots & Island Chains
**User Story**:  
> “As a user, I want to define stationary hotspots under the crust so that as plates drift over them, they generate volcanic island chains.”

- **Acceptance Criteria**:  
  - The user can place a hotspot point at a given lat/long, stationary.
  - The system creates a ‘motion path’ or chain indicating how crust passes over the hotspot through time.  
  - The user can then draw polygonal islands over the path at each timestep if desired.

### 4.4 Mid-Ocean Ridges & Plate Topologies
**User Story**:  
> “As a user, I want to mark mid-ocean ridges (as polylines) and automatically generate a ‘plate topology’ that shows each plate’s boundary evolving over time.”

- **Acceptance Criteria**:  
  - The user can define a “MidOceanRidge” polyline between diverging plates.  
  - The system can build a “ClosedPlateBoundary” topology automatically from all ridge, subduction, and transform boundary segments.  
  - This plate boundary updates as the user changes rifts or collision lines.

## 5. FINISHING & EXPORTING

### 5.1 Final Display Adjustments
**User Story**:  
> “As a user, I want to toggle on/off or reorder different feature layers (continents, orogenies, hotspots, etc.) so that I can produce a clear, uncluttered map.”

- **Acceptance Criteria**:  
  - A layers panel to show/hide feature collections (e.g., cratons, ocean crust, orogenies, subduction zones).  
  - Opacity or color controls for each layer.  
  - Ability to remove grid lines (lat/long) or change the projection from globe (3D) to rectangular or Mollweide (2D).

### 5.2 Exporting Maps & Timelapse
**User Story**:  
> “As a user, I want to export snapshots or a series of images/videos of the world’s tectonic evolution so that I can use them in external illustrations or editing software.”

- **Acceptance Criteria**:  
  - Export a single snapshot (image or vector) at a specified time.  
  - Export an entire time-sequence (e.g., every 10 Ma) to create a timelapse.  
  - Choose from common 2D map projections (Equirectangular, Mollweide) or the 3D “globe view.”  
  - The export must preserve colors, layer visibility, and the time-based geometry of features.


# Methodology, organisation of the project

## Minimum Viable Product (MVP)

The fundamental goal of the MVP is to **demonstrate core functionality** that proves all major layers—**Django** (back end), **Rust→WASM** (geometry), **Three.js** (3D front end), and **HTMX** (partial updates)—work in concert. 

Concretely, the MVP will contain:

1. **3D Globe Visualization**  
   - A basic globe rendered in Three.js.  
   - User can **orbit** and **zoom** the camera around the globe.  
   - At least one simple **visual theme** (e.g., Earth-like texture or blank globe).

2. **Polygon Drawing & Storage**  
   - A tool for the user to **draw polygonal features** (e.g., a single continent outline or multiple polygons) directly on the globe’s surface.  
   - Each polygon is labeled with a **Plate ID** or other identifier.  
   - Polygon data (coordinates, plate ID) is **saved** to a Django database.  
     - **Technical Detail**: Coordinates or shape data might be stored as JSON or a custom format.  
     - Basic creation/deletion of polygons should be possible.

3. **Translation & Rotation of Polygons**  
   - The user can **select a polygon** and apply transformations to move it around the globe.  
   - **Translation**: Shifting the polygon’s position over the sphere’s surface. (Internally, we can represent this as a combination of small rotations around local axes, or direct lat/long offset if the sphere approach is simplified. Either approach must be handled by the geometry module in Rust→WASM.)  
   - **Rotation**: Rotating the polygon about a chosen axis (Euler rotation) to simulate plate drift.  
   - **Technical Detail**:  
     - The geometry engine in **Rust→WASM** will receive the polygon’s vertex data plus a transformation command (e.g., translation vector, rotation angle/axis).  
     - It returns the **updated vertex positions** to the front end, which updates the Three.js mesh.  
   - The user should see **immediate feedback** (or near-immediate) in the 3D scene after the transformation is applied.

4. **Project Management**  
   - Create, name, and store multiple **Projects** in the database.  
   - Each Project can have multiple polygons.  
   - Users can **load** a Project to resume editing or viewing polygons.  
   - **Technical Detail**:  
     - Django models: `Project`, `Polygon` (with references to plate ID, coordinate data).  
     - Simple UI flow (e.g., an HTMX form) to create/select a Project.

5. **Basic UI & HTMX Partial Updates**  
   - Users can perform these actions (drawing polygons, applying transformations, saving/loading) without full-page reloads.  
   - The front-end **calls** Django endpoints via HTMX, returning partial HTML or JSON fragments to update small sections of the page (like a “List of Polygons” panel).

### Justification and Technical Feasibility

- **Integration of All Layers**:  
  - Django → (HTMX) → Three.js → Rust/WASM ensures the application pipeline is validated.  
- **Demonstrable Tectonic Basis**:  
  - Even though advanced features (like splitting or collisions) aren’t in the MVP, being able to **translate** and **rotate** polygons is the fundamental building block for simulating tectonic movement.  
- **Scalability**:  
  - Once the MVP is stable, we can add rift logic, subduction, collisions, etc., building on the transformations already proven in the MVP.

By completing this **expanded MVP**, we will have a **tangible, interactive** web tool that clearly shows how user-defined polygons (representing continents or plates) can be **moved** around a globe in real time, with **all underlying technologies** (Django, HTMX, Rust→WASM, Three.js) working together. Everything beyond these core elements constitutes **further enhancements** rather than essential viability.

## 3. Phases of Development

### Phase 1: Project Setup & MVP Definition
- **Goals**:  
  1. Finalize the repository structure on GitHub.  
  2. Initialize Django + HTMX scaffolding.  
  3. Set up Rust → WASM toolchain (wasm-pack, etc.).  
  4. Integrate a minimal Three.js scene showing a globe.  
  5. Clearly document the **MVP** scope and user stories in GitHub issues.

- **Deliverables**:  
  - A bare-bones web app running on localhost, ready to host future features.  
  - A GitHub Project board with initial tasks (To Do / In Progress / Done).  
  - Definition of the MVP (as above) in the project README or wiki.

### Phase 2: MVP Implementation
- **Goals**:  
  1. Implement **polygon drawing** on the globe (via Three.js).  
  2. Create a Django model to store polygon/plate data.  
  3. Connect polygons to **Rust WASM** for simple rotation computations.  
  4. Build partial updates (HTMX) for saving/loading polygons.

- **Deliverables**:  
  - Working MVP: user can draw polygons, store them in DB, apply a rotation, and see the updated position on the globe.  
  - Basic UI for project management (create project, load project).  

### Phase 3: Core Tectonic Features
- **Goals**:  
  1. Expand **geometry logic** in Rust WASM to handle initial rifting or polygon splitting.  
  2. Add subduction zones or collision detection (basic version).  
  3. Improve the front-end UI with interactive timelines or controls for the rotation.  
  4. Validate data flow from user input → WASM calculations → database.

- **Deliverables**:  
  - Demonstration of advanced plate manipulation (partial rifts, or a simple collision).  
  - Extended data models (e.g., “Rifts,” “Subduction,” “Polygons” with timestamps).  
  - Refined UX for controlling tectonic processes.

### Phase 4: Feedback, Polishing & Extended Features
- **Goals**:  
  1. Seek **feedback** from potential stakeholders (e.g., worldbuildingpasta, Artifexian) on UI/UX and scientific plausibility.  
  2. Perform **performance optimizations** if needed (minimizing WASM-JS overhead, indexing polygons in DB, etc.).  
  3. Enhance UI controls (timeline slider, partial animations, better rendering).  
  4. Possibly add new features like exporting maps or advanced geometry (flowlines, orogenies).

- **Deliverables**:  
  - Updated, more polished interface with improved user workflows.  
  - Potential initial feedback from external “clients” integrated.  
  - Documented performance tests or code profiling results.

### Phase 5: Finalization & Documentation
- **Goals**:  
  1. Final **bug fixes** and feature refinements based on last feedback.  
  2. **Documentation**: usage guide, developer notes, diagrams, final report.  
  3. **Testing**: user acceptance tests, possible unit/integration tests for geometry correctness.  
  4. Prepare **deployment** instructions or a demonstration environment.

- **Deliverables**:  
  - Stable, presentable version of the application that meets or exceeds the MVP and core enhancements.  
  - Comprehensive documentation (install/setup guide, user manual, developer API references).  
  - Possibly a short video or demo website to showcase functionality.

## 4. Agile Tooling

- **Git + GitHub**  
  - All code changes tracked on GitHub, with branching and pull requests.  
  - GitHub Issues to describe tasks/bugs, linked to a **GitHub Projects** kanban board.

- **Clockify (Optional)**  
  - Time tracking tool for self-monitoring productivity.  
  - Used if it proves beneficial; otherwise, not mandatory.

- **Frequent Commits & Iteration**  
  - Each phase concludes with a **working build** and short reflection.  
  - Adjust or re-prioritize tasks if new insights or challenges arise.

## 5. Flexibility and Risk Management

The **Agile, incremental** structure ensures that if unforeseen difficulties arise—such as complex geometry problems or significant performance bottlenecks—phases can be **extended** or **re-scoped** without jeopardizing the entire project timeline. The MVP guarantees a minimum deliverable outcome, while subsequent phases accommodate innovation, user feedback, and refinement.

# Position of the solution 

## 1. Existing Solutions: Strengths, Weaknesses, and Gaps

### 1.1 GPlates (Scientific Tectonic Modeling)
- **Description**: A professional-grade application designed for reconstructing **Earth’s** tectonic history from geological data. It enables advanced operations like subduction modeling, rift creation, and flowline generation.  
- **Strengths**:  
  - **Scientifically accurate** for real-world plate tectonics.  
  - Rich **feature set**: rotating plates in time, drawing rifts, generating subduction zones, etc.  
  - Used by **geologists** and researchers, so it has a track record of **scientific validation**.  
- **Weaknesses** (for an imaginary map context):  
  - **Complex UI / Workflow**: Geared toward Earth-based data sets and professional geologic analysis. The article from **WorldbuildingPasta** highlights that while GPlates can be repurposed for fictional worlds, the process is **awkward** and requires multiple workarounds.  
  - **Steep Learning Curve**: Terms like “pole manipulation,” “flowlines,” and “rotation files” can be off-putting for creative users who simply want to “draw and drift” continents.  
  - **Less Focus on Artwork**: The final outputs are more scientific than aesthetic—useful for analysis, but not ideal as a “final map” for storytelling or visual appeal.  
  - **Limited “painting” approach**: In GPlates, you define polygon features in a somewhat technical manner. It’s powerful but not as intuitive as a direct “draw on sphere” approach that many worldbuilders desire.

### 1.2 Artistic Map Tools (Wonderdraft, Inkarnate, etc.)
- **Description**: Cloud-based or desktop applications that allow users to **paint** or **generate** fantasy maps with beautiful styles, icons, and landmass shapes.  
- **Strengths**:  
  - **Ease of Use**: Highly intuitive, often just point-and-click.  
  - **Artistic Control**: Users can quickly produce aesthetically pleasing maps, with stylized coastlines, terrain textures, and decorative elements.  
  - **Community Assets**: Large libraries of icons, brushes, and samples.  
- **Weaknesses**:  
  - **No Real Tectonics**: These tools don’t simulate or account for plate boundaries, subduction zones, or orogenies. They are purely **visual**.  
  - **Static 2D**: Typically, there’s no built-in concept of an evolving planet or an interactive globe in 3D.  
  - **Limited Geologic Realism**: Maps can look nice but lack internal consistency in mountain placements or continental drift unless manually planned.

### 1.3 Blender (3D Modeling & Animation)
- **Description**: A powerful, open-source 3D creation suite for modeling, animating, rendering, etc.  
- **Strengths**:  
  - **Extremely Flexible**: You can model a sphere, paint textures, animate transformations, and create stunning renders.  
  - **Robust Community**: Countless tutorials, add-ons, and user scripts.  
  - **High-Quality Visual Output**: If one invests time, Blender can produce professional-grade 3D visuals.  
- **Weaknesses**:  
  - **No Native Plate-Tectonic Logic**: Blender doesn’t inherently handle geologic or geospatial calculations. You’d need custom scripts or manual keyframing.  
  - **Steep Learning Curve**: Like GPlates, Blender is powerful but demands specialized knowledge of 3D modeling, rigging, and node-based materials.  
  - **Tedious Tectonic Workflow**: To animate continents drifting realistically, you’d have to manually define pivot points, collisions, subductions, etc. This quickly becomes complex without a dedicated plugin or script.

## 2. Why a New Solution?

Given these existing tools:

1. **GPlates** is scientifically robust but unwieldy for imaginative planet creation. Its interface is oriented toward real Earth data, and the partial solutions detailed by **WorldbuildingPasta** (in “An Apple Pie from Scratch” tutorials) underscore how **non-trivial** it is to use GPlates for purely fictional worlds. 

2. **Artistic map-making tools** (Wonderdraft, Inkarnate, etc.) excel at **visual creativity** but ignore tectonic realism. They produce attractive 2D maps but cannot animate or simulate continent drift, collisions, or rifting.

3. **Blender** can do nearly anything in 3D, but it lacks built-in geological logic. It requires a hefty learning curve and extensive manual rigging or scripting to replicate even basic tectonic processes.

To fill this **gap**, we need a **hybrid approach** that:

- **Combines** the intuitive “draw-and-animate” user experience of artistic tools with the **science-based** modeling of plate interactions seen in GPlates.  
- Operates **directly on a 3D globe** (rather than a flat map), letting creators truly think “globally.”  
- Handles **fundamental tectonic math** (rotations, translations, potential subduction lines), but without expecting the user to manipulate arcane Euler pole files or parse specialized geological data formats.

## 3. Advantages of Developing a Dedicated New Tool

1. **User-Centric Interface**:  
   - A brand-new solution can prioritize **ease of drawing** continents, selecting them, and applying straightforward transformations (“move this plate west over 50 million years”).  
   - Emphasis on a **friendly UI** rather than advanced geological nomenclature.

2. **Focused on Fictional Workflows**:  
   - The tool can incorporate features specifically for **imagined tectonic histories**—like automatically generating rough orogenies when continents collide or allowing quick “split plate” operations.  
   - No confusion about real Earth data sets or historical references.

3. **Dynamic Evolution**:  
   - Because it’s built for plate motion and timeline animation, the system can produce **animated sequences** showing landmass drift.  
   - Exports could yield multi-frame images or real-time playback for showcasing an entire planet’s history.

4. **Streamlined Integration**:  
   - By combining **Django + HTMX** (server side), **Three.js** (3D in-browser), and a **Rust→WebAssembly** geometry engine, the new tool can be **web-based** (no local installation complexity).  
   - Lowering the barrier for creative users to just “open a browser” and build worlds.

5. **Potential Community Involvement**:  
   - As the tool is more approachable than GPlates, it may attract worldbuilders, hobbyist geologists, and educators looking to illustrate basic plate tectonics in a more **fun** way.

## 4. Conclusion: The Relevance of a New Solution

A new, **dedicated application** is not just a minor convenience—it’s the **missing piece** between heavily specialized scientific software (like GPlates) and purely artistic or general-purpose 3D tools (like Wonderdraft or Blender). 

- **GPlates** demonstrates the possibility of advanced tectonic modeling, but its UI and workflow are barriers to creative adoption.  
- **Artistic tools** are simple and visually stunning but lack geological underpinnings.  
- **Blender** is too general and requires manual setup for geologic processes.

Hence, developing a **custom tool** that merges intuitive map creation with authentic tectonic logic **bridges this gap**. It can provide immediate value to any worldbuilder seeking realistic, dynamic maps without forcing them to adopt either a purely artistic or purely scientific pipeline. It also becomes **more than a novelty**: a genuine platform for **learning**, **experimentation**, and **collaboration** on fictional geosciences.

# Technical analysis

## 1. High-Level Architecture Overview

Our goal is to build a web-based application that:

1. Lets users draw and manipulate polygons on a **3D globe** (to represent continents, plates, subduction zones, etc.).  
2. Performs **complex geometry calculations** (splitting polygons on a sphere, computing plate rotations, collisions, etc.) with good performance.  
3. Stores and retrieves user data (e.g. saved tectonic projects, timestamps, transformations) in a **back-end**.  
4. Offers an incremental, flexible web interface that can be easily updated without full page reloads.  

The **final stack** decided upon:

- **Django** + **HTMX** for the web back-end and partial-page updates.  
- **Three.js** for 3D globe rendering and interaction in the browser.  
- **Rust** → **WebAssembly** for geometry and math-heavy computations (plate rotations, polygon clipping on a sphere, etc.).  

Below, we analyze the key technical choices in each layer.

---

## 2. Back-End Layer

### 2.1 Django + HTMX

**Chosen Approach**: A Python-based, server-side framework (Django) combined with **HTMX** for partial page updates.

1. **Why Django?**  
   - **Batteries-Included**: Django provides authentication, ORM, admin interface, security features (CSRF, XSS protection) out of the box. This is beneficial for a final-year project or any scenario requiring reliable user/role management.  
   - **Structured Project Layout**: Encourages a clean “apps” architecture and a well-defined approach to URLs, views, models, etc.  
   - **Mature Ecosystem**: Large community and extensive documentation. If the project expands (e.g., user profiles, multiple saved worlds, advanced features), Django scales well.

2. **Why HTMX?**  
   - **Partial Page Updates**: HTMX allows small HTML snippets to be updated on user interaction, reducing the need for a heavy SPA framework.  
   - **Minimal JS Overhead**: We can keep most of our front-end logic in the 3D scene (Three.js) and rely on HTMX for simpler form submissions, data fetches, and incremental UI updates.  
   - **Good Fit with Django Templates**: HTMX requests can return partial Django templates that inject data straight into the page.  

#### Pros of Django + HTMX

- **Integrated Admin**: Perfect for quick data management (e.g. we can handle user or plate data in the admin panel if needed).  
- **Security / Auth**: Well-tested solutions for user authentication, sessions, CSRF tokens.  
- **Less JavaScript**: HTMX avoids building a full SPA or managing complex front-end state.  
- **Compatibility with Python**: If we want to add advanced geoscience libraries in Python on the server, it’s straightforward.

#### Cons of Django + HTMX

- **Heavier Framework**: Django is more monolithic compared to microframeworks like Flask or FastAPI. For a purely API-centric approach, it can feel like overkill.  
- **Synchronous by Default**: Advanced concurrency or real-time features may require additional configuration (e.g. Django Channels).  
- **Learning Curve**: Django’s conventions, while helpful, can be time-consuming if the user simply needs a lightweight REST API.

#### Why We Ruled Out Alternatives

- **Flask or FastAPI**: These are lighter, more flexible for APIs, but they require more manual setup for user auth, database migrations, or admin tools. If the project demands a quick deployment with standard user management, Django’s built-in features are very handy.  
- **Node.js / Express**: Would unify the language (JavaScript/TypeScript) across front and back, but we lose Python’s ecosystem for potential geoscience libraries and the convenience of Django’s admin.  
- **Next.js / Vue / SvelteKit**: These meta-frameworks are excellent for advanced front-end interactivity or SSR, but might be overkill if the main complexity is in the 3D and geometry logic, rather than in many dynamic front-end components.

**Conclusion**: Django + HTMX offers a balanced, stable environment for storing user data, handling partial updates, and providing structure. It’s slightly heavier than a microframework but is worth it for built-in features and a well-tested approach to security and session management.

## 3. 3D Rendering & Front-End Visualization

### 3.1 Three.js

**Chosen Approach**: **Three.js** is the primary library to render an interactive 3D globe in the browser.

1. **Why Three.js?**  
   - **Large Community and Docs**: It’s the most widely adopted general-purpose 3D library on the web, with extensive examples.  
   - **Flexibility**: We have full control over scene, camera, and geometry, which is essential for custom features like plate boundaries, polygon splitting, and spherical transformations.  
   - **Easy Integration**: We can render the scene in a standard `<canvas>` in the Django template and control it with JavaScript while letting HTMX handle other UI parts.

#### Pros of Three.js

- **Mature Ecosystem**: Many plugins, loaders, and tutorials for advanced features (e.g. post-processing, VR, etc.).  
- **Straightforward**: Setting up a basic scene with a globe, orbit controls, and custom meshes is well-documented.  
- **Active Support**: Large user base means more community help when stuck.

#### Cons of Three.js

- **Manual Setup**: We have to code camera controls, interactions, and possibly spherical geometry.  
- **Heavier vs. Minimal WebGL**: The library itself is relatively large (although still quite acceptable for modern web).

### 3.2 Alternatives Considered

- **Babylon.js**: Another popular engine, has a more “game-engine” feel with integrated physics and advanced materials. Slightly heavier than Three.js.  
- **CesiumJS**: Designed for real-world geospatial rendering with tiles and terrain data. Might be overkill if we’re not using real Earth data. Also specialized for Earth-based lat/long.  
- **Raw WebGL**: Full control, but would require implementing our own scene graph, camera system, input handling, etc.—too time-consuming.

**Conclusion**: **Three.js** is a sweet spot of power, community support, and flexibility for custom globe-based visualizations.

## 4. High-Performance Geometry: Rust → WebAssembly

### 4.1 Why WebAssembly?

We need advanced geometry operations:

- **Spherical polygon splitting** (for rifts)  
- **Plate collision detection**  
- **Euler rotations** over large time intervals  

These are CPU- and math-intensive. **WebAssembly (WASM)** offers near-native performance in the browser, significantly outperforming pure JavaScript for heavy numeric tasks.

### 4.2 Why Rust?

1. **Memory Safety**: Rust ensures safe concurrency and prevents many classes of bugs (segfaults, data races).  
2. **Ecosystem / Tooling**: The Rust→WASM toolchain (e.g., `wasm-bindgen`, `wasm-pack`) is mature and straightforward to integrate with modern JavaScript.  
3. **Performance**: Rust often achieves performance on par with C++ in numeric tasks.  
4. **Active Community**: Many geometry crates, though we may still need to adapt or write custom code for spherical geometry.

#### Pros of Rust → WASM

- **High Performance & Safety**: Great for robust numeric code.  
- **Integration**: Straightforward bridging to JavaScript—functions can be exposed and then called from Three.js or other JS logic.  
- **Growing Ecosystem**: Good crates exist for geometry, linear algebra (e.g. `nalgebra`), robust testing frameworks, etc.

#### Cons of Rust → WASM

- **Learning Curve**: Rust is more complex than higher-level languages, and new developers must learn ownership/borrowing.  
- **Bridging Overhead**: Passing large data structures between Rust WASM and JS can incur overhead if not optimized.  
- **Less Spherical Geometry Out-of-Box**: Might need to wrap or port an existing library (like S2, CGAL, or GEOS) or write custom logic.

### 4.3 Alternatives Considered

- **C/C++ → WASM (Emscripten)**: Also viable, especially if using existing geometry libraries in C/C++. But setup can be more cumbersome, and memory safety is not guaranteed.  
- **AssemblyScript**: A TypeScript-like language for WASM. Simpler for JS devs, but less mature for advanced numeric tasks.  
- **Go → WASM**: Larger binaries, less common approach for geometry, overshadowed by Rust’s popularity in the WASM space.

**Conclusion**: **Rust → WASM** is an optimal choice for safe, fast geometry computations that integrate well with a modern JS front end. It has a steeper learning curve than JavaScript alone but offers crucial performance and reliability benefits.

## 5. Supporting Tools & Methodologies

### 5.1 Database & ORM

- **Database Choice**: Django typically defaults to **PostgreSQL** or **SQLite** for prototyping. If the project needs concurrency or scaling, PostgreSQL is robust.  
- **ORM**: Django’s built-in ORM. This handles user accounts, storing project metadata (plate definitions, times, references to geometry data). We likely store geometry “raw” in JSON or as custom references, because the main geometry computations happen in Rust/WASM.

### 5.2 Partial Updates & Interaction

- **HTMX** + **Django Templates**: Return partial HTML fragments for side panels (e.g., a list of plates, timescale controls).  
- **Three.js Canvas**: Remains active on the front end, calling WASM code for geometry updates. The user’s mouse events on the globe do not necessarily rely on HTMX—this can be direct JS.

### 5.3 Concurrency / Real-Time

- **Synchronous Django** is sufficient if the main use case is a single user or small group.  
- If real-time collaboration or heavy concurrency is desired, we might look into **Django Channels** (WebSockets) or asynchronous frameworks. For now, not strictly necessary.

### 5.4 Security

- **Django** handles sessions, CSRF tokens, user authentication.  
- **HTTPS** recommended for data in transit.  
- Basic checks on user inputs to avoid malicious data in polygons or file imports.

## 6. Comparison of Final Stack vs. Potential Alternatives

Below is a concise table of the **chosen** stack vs. the main alternatives:

| **Layer**         | **Chosen**                | **Alternatives**                                  | **Why We Chose**                                                 |
|-------------------|---------------------------|---------------------------------------------------|------------------------------------------------------------------|
| **Back End**      | Django + HTMX            | Flask / FastAPI / Node.js / Next.js / .NET Blazor | - Built-in admin & auth<br>- Strong security & structure<br>- Good synergy w/ HTMX |
| **Front End**     | Minimal JavaScript + Three.js + HTMX partials | React/Vue/Angular SPA, Babylon.js, Cesium        | - Three.js is flexible & well-documented<br>- No heavy SPA needed<br>- HTMX simplifies incremental updates |
| **Geometry Engine**| Rust → WASM             | C/C++ → WASM, AssemblyScript, Go → WASM           | - Memory safety + high performance<br>- Great Rust→JS bridging<br>- Good for advanced numeric tasks |
| **3D Visualization**| Three.js               | Babylon.js, CesiumJS, raw WebGL                   | - Large community, simpler general-purpose 3D<br>- Good performance and customizability |

---

## 7. Justification of Each Final Choice

1. **Django + HTMX**:  
   - We want user-friendly data management, an integrated admin panel for user accounts, and partial updates for forms without a full single-page app.  
   - Django provides robust foundations (ORM, security) plus a well-known structure. HTMX keeps front-end overhead minimal, since the real complexity is in the 3D scene.

2. **Rust → WASM for Geometry**:  
   - Splitting polygons on a sphere and calculating plate collisions require robust numeric routines. JavaScript alone could be slow or less reliable for complex geometry.  
   - Rust’s memory safety is an advantage over C/C++, and its ecosystem for WASM integration is well-documented.

3. **Three.js** for 3D:  
   - A widely used, flexible library for custom 3D rendering in the browser.  
   - Straightforward to integrate with the rest of the front-end.  
   - Large online community and tutorials.

4. **Why Not a Full SPA**:  
   - We primarily need advanced 3D interactions, not a huge dynamic form-based app.  
   - HTMX covers partial page updates elegantly.  
   - Minimizes front-end complexity while capitalizing on Django’s server-rendered pages for simpler forms, data retrieval, etc.

---

## 8. Potential Limitations & Future Enhancements

- **Large Data Sets**: If users create extremely high-resolution polygon features, we could face performance bottlenecks in the WASM bridging or the Three.js rendering. Possible solutions include data compression or level-of-detail (LOD) strategies.  
- **Advanced Collaborative Features**: Real-time collaboration would require more advanced async frameworks (e.g., Django Channels) or a different environment.  
- **3D Performance**: For very large or complex worlds, WebGPU (the successor to WebGL) might eventually be worth exploring, though it’s still in early adoption.

---

## Conclusion

The final technical stack—**Django + HTMX** on the server, **Three.js** for 3D rendering, and **Rust→WASM** for computational geometry—strikes a balance between **developer productivity**, **performance**, and **scalability**. Each choice is justified by:

1. **Django + HTMX**: Rapid development of a robust, secure, partial-page-updating back-end with minimal extra JavaScript.  
2. **Rust → WASM**: Reliable, high-performance numerical routines essential for plate-tectonics-style geometry calculations.  
3. **Three.js**: Familiar, well-documented 3D library that supports custom globe interactions, perfect for drawing and animating tectonic plates.

This approach positions our application as a flexible, modern web-based platform capable of replicating (and potentially improving upon) key GPlates-like functionalities for imaginary or fictional world tectonics.
# Conception of the solution 

# Validation strategy

1. **Classed by User Types**:  
   - **Beginner Worldbuilders**: Might focus on simpler rift-and-drift.  
   - **Advanced Tectonics Enthusiasts**: Will use deeper features like subducting ocean crust, orogenies, flowlines, and hotspots.  
2. **Precision & Relevance**:  
   - The system need not replicate every geophysical nuance, but must allow the creation, splitting, collision, and subduction of plates with a plausible timeline.  
3. **Complexity Estimation**:  
   - *Splitting/merging polygons on a sphere* is high complexity (must handle spherical geometry, possibly via Rust→WASM).  
   - *Animating large numbers of polygons over time* is also non-trivial.  
4. **Priority**:  
   - Core MVP: Draw polygons, define plates, move them (rift/collision), see timeline.  
   - Secondary: Flowlines, subduction arcs, orogenies, LIPs.  
   - Tertiary: Automatic plate topologies, advanced exporting, hotspot chains.

# Securisation and RGPD
