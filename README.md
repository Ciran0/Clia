![CliaLogo](https://github.com/user-attachments/assets/cb4a758b-be16-4c11-acb8-e6f5d83f6856)

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
Worldbuilding is the act of creating fictional settings. It is most often used by writers, DMs, game makers and artists to ground the stories they create, but a lot of other projects can benefit from well crafted settings and some people (like me) just practice worldbuilding in itself for fun. 
But worldbuilding is in itself an aglomeration of many other, more specific practices like conlanging (creating languages), neography (creating writing systems) or mapmaking (creating fictional maps) and many more.
One pretty well known tricks that can be used to impart complexity, richess and a sens of belivablitly to any worldbuilding project is to make it's history. Instead of building the thing only at the state that matters to you, you create it at an arbitrary point in the past and artificially simulate it's evolution up until the point that interests you. This process is way more time consuming but also more complicated as you have to understand how things like languages, alphabets, ecosystems or geology evolve over time. 
But for some worldbuilders this extra effort is worth it.
For simulating the evolution of a lot of things, paper, motivation and a great amount of knowledge is enough. But when we talk about the evolution of the geography of a planet, it get's way more complicated as the finaly product is basically a small film of continents moving on a sphere (anybody that can make that with paper get's my undying respect).

Making geological history of maps is still, even in the worldbuilding hobby, a pretty niche subject, despite the fact that geography is probably one of the highest building block of any worldbuilding projects.

## 1.2 The Gap in Existing Tools
The main reason, in my opinion, that geological histories are sadly not as common in the worldbuilding community is because there curently is a gap in the existing available tools to do so :

- **Fantasy map tools** (World Anvil, Wonderdraft, Inkarnate):
   These tools are mostly made for artistic design and story building. They can be very usefull to anotate maps or follow the progression in a story but they provide very few ways to animate the map, draw it directly on a sphere and absolutely no way to manipulate the geography of the map like real techtonic plates.
- **Scientific software** (GPlates):
   This is a professional-level application for real plate tectonics. It is extremely powerful but geared toward Earth’s data and workflows. It might be too technical for most worldbuilders and it is not designed to handle fictional mapmaking. Using it in this way has its own quirks.

I feel like there is a real need and a real opportunity for a tool geared towards fictional mapmaking that helps worldbuilder make scientifically grounded geographic histories without having to deal with the quirks and complexity of current scientific software and therefore help them make their setting more rich and more belivable.
This is this objective that this project is going to pursue.

## 1.3 Project Overview
Clia (from the contraction of *Clymene* and *Lapetus*, the parents of the titan Atlas) will be a web application that allows users that are not familiar with advanced scientific tooling to easily make geological histories of fictional maps.

The **lack of a specialized tool** for **fictional geologic history animation** presents an opportunity to:
- **Simplify** advanced scientific tools (like GPlates) into a **streamlined** web app suited for non-experts.  
- Provide an **educational bridge** between fantasy creation and real science, helping worldbduilders **enriching** their fictional settings
- Explore new and exciting technologies to solve technical challenges, be it in methematics and geometry or in user interaction.

---

# Identification of Major Agents

## 2.1 Overview of main agents
1. **Users** :
      **Worldbuilders**:
         Worldbuilders are simply people that want to create worlds, for any reason. They are the main target for this tool and while the worldbuilding community is quite large, making geological history is still a niche topic. This is why this project has to cater to both the casual worldbuilder that want to try their hand at geologic histories and the hardcore user who want to explore alternatives to GPlates.
      **Educators**:
         While this application is mainly targetted at worldbuilders, the opportunity of having an easy to use tool to represent techtonic interaction can be really usefull for anybody wanting to teach the basics of techtonic principles.
2. **Worldbuilding Pasta**:
   Worldbuilding Pasta is the name of a blog focused on scientifically acurate worldbuilding. This blog is by far the best ressource on the use of GPlates as a tool for fantasy geological history making [Making an apple pie from scratch V](https://worldbuildingpasta.blogspot.com/2020/06/an-apple-pie-from-scratch-part-v.html). The writer of the blog has been contacted and has expressed interest in the project but is currently waiting for the project to be better defined in order to decide if they want to involve themselves in the project. Their input on this project could be an amazing asset and they will be recontacted as the project develop in order to keep them informed.
3. **Artifexian**:
   Artifexian is a worldbuilding youtuber that has made a video serie based on Worldbuilding Pasta's blog. They have been contacted a year ago when this project was in its infancy and they expressed interest in it. I have try to recontact him to no avail but I will try to do so again as the project develops. The experience of Artifexian on worldbuilding could be really helpfull and this project could possibly also benefit from the exposure to his community.
4. **Me / Project Owner**  
   Since I have failed to convince the interested parties in taking the role of clients for this project, this role will have to be filled by myself for the time beeing. I nonetheless consider myself to be a worldbuilder and this project is one that is truely near and dear to my heart and I am not unhappy to keep ownership over it. Furthermore, the real client, in the end, is the worldbuilding community.

## 2.2 Potential Clients and Their Roles
| **Agent**  | **Background** | **Interest & Status** | **Role** |
|:--------------|:----------------------|:------------|---|
| **Artifexian**   | Produces worldbuilding, cartography, and conlang videos on Youtube | Showed interest in the project a year ago, but has not been reachable since the project has started | None currently but might act as an expert or help expose the project to a wider audience. Furethermore, the Worldbuilder's log video serie is used as one of the main ressources for the worldbuilding/geologic side of the app|
| **WorldbuildingPasta**      | Blogger focused on advanced worldbuilding and specialist in the use of GPlates for fictional geologic history | Enthusiastic but wants more details before involving themselves more in the project.| None currently but might act as an expert once the project becomes more defined, the Worldbuilding Pasta blog is a really important inspiration for this project.|
| **Me**| Student at Ephec with an interest in web developement| Amateur worldbuilder | current developer and owner of the project, will act as main client for the time beeing |
| **The worldbuilding community** (target users)| Anybody that has interest in worldbuilding | the few contacts I had with members of the community were positive, The project will have to be in a more advanced state before expositing it to the broader community | the project purpose is to be shared and used by as many people as possible, but setting ways of involving the community in the feedback process (discord server) is prematured |

---

## 3.1 Basics

### User account management
> "As a user, I want to have access to all the usual account managements features expected from modern web applications"

**Acceptance Criteria**:
- [ ] Create account
- [ ] Log in
- [ ] Log off
- [ ] Modify account informations
- [ ] Recover account

**Importance**: Must have
**Complexity**:very low

### Startup & Project Creation
> “As a user, I want to initialize a new tectonic project so I can begin designing a planet’s geologic timeline from scratch.”

**Acceptance Criteria**:  
- [ ] Create a new project.  
   - [ ] Give the project a name
   - [ ] Set various project settings (gravitational constant, planet radius)
- [ ] Display the blank default globe to start working

**Importance**:Critical
**Complexity**:Low

### Saving the Project
> “As a user, I want to save my current project data so I can reopen it later.”

**Acceptance Criteria**:  
- [ ] ‘Save Project’ action storing the various features of the project
- [ ] If the project already exists, update its state
- [ ] Create a new entry in the database if the project is new


**Importance**: Should have
**Complexity**: Low

### Load Project
> “As a user, I want to be able to open one of my saved projects"

**Acceptance Criteria**:  
- [ ] A ‘Load project’ action to open an existing project
- [ ] Displays a list of the user's current projects

**Importance**: Should have
**Complexity**: Low

---
## 3.2 Drawing on the sphere

### Node by node drawing
> "As a user, I want to be able to put down a series of nodes that gets connected into a polygon"

**Importance**: Critical
**Complexity**: Medium

### Node by node editing
> "As a user, I want to be able to displace or delete existing nodes and add a node between two existing nodes in order to change the shape of a feature"

**Importance**: Critical
**Complexity**: Medium

### Logic feature editing
> "As a user, I want to be able to edit a feature by drawing an other feature and applying a logical opperation between the two (additive, substrative, ...)"

**Importance**: Should have
**Complexity**: Medium-high

### Pencil drawing
> "As a user, I want to be able to draw a line on the globe and have it automatically convert in a serie of points"

**Importance**: Good to have
**Complexity**: Medium

---
## 3.3 Project, feature data and tools

### Measuring tool
> "As a user, I want to have access to a tool that allows me to measure the distance between two points"

**Acceptance Criteria**
- [ ] the measuring tool can be used to acurately measure distances on the sphere

### Project data
> "As a user, I want to be able to track multiple informations about the world"

**Acceptance Criteria**
- [ ] Tracking the total land coverage of the planet

### Feature data
> "As a user, I want to be able to click on a feature to see multiple informations about it"

**Acceptance Criteria**
- [ ] Get the age of the feature
- [ ] Get the current speed of the feature
- [ ] Get the area of the feature (if pertinent)
- [ ] Get various geometric informations about the feature

### Feature history
> "As a user, I want to be able to access a small history of the various events that have happened to a feature"

---
## 3.4 Making & Moving Plates

### Creating initial cratons
> “As a user, I want to be able to draw cratons on the sphere to lay out the base of the initial supercontinent"

**Acceptance Criteria**:  
- [ ] A craton option that allows the user to add a new craton on the sphere
- [ ] Confirming the shape of the craton

### Creating the initial supercontinent
> "As a user, I want to be able to surround the cratons with the initial continental crust"

- [ ] A continental crust option that allows the user to surroung the cratons with a new polygon
- [ ] Check if the supercontinent correctly surrounds every cratons

### Flowlines and mid ocean ridges
> "As a user, I want to see flowlines between diverging plates as well as the mid ocean ridge"

**Acceptance Criteria**:  
- [ ] flowlines appear between divergent plates
- [ ] notify the use if the flowlines cross each other (bad practices)
- [ ] keep track of the mid ocean ridge as the plates moves

### Defining Rifts
> “As a user, I want to draw a rift line across a continent so it can split into two separate plates.”

**Acceptance Criteria**:  
- [ ] draw a polyline through a plate
- [ ] extrapolate the polyline to features that needs to be split too (island arcs, oceanic plate)
- [ ] check that the rift doesn't goes through any cratons

### adding failed rifts
> "As a user, I want to draw a polyline comming from either a node of a rift or the side of a plate to define a failed rift. This failed rift can be used as the template for full rifts"

**Acceptance Criteria**:  
- [ ] I can draw a polyline with a node of a continental plate or rift as starting point
- [ ] I can reactivate a failed rift and extend it into a full rift

### Splitting a Feature
> “As a user, I want to split an existing plate along the rift line so each side can be considered as different plates and move independently"

**Acceptance Criteria**:  
- [ ] the two split plates are considered as two and move independently
uu
### Making the plates drift
> "As a user, I want to define a direction, rotation and a speed in order to make a plate drift over a set period of time"

**Acceptance Criteria**:
- [ ] inputing a speed, a rotation, a direction and a length of time to correctly displaces the plate
- [ ] every features that are associated to the plate move in sinc with the plate

### Adding Ocean Crust
> “As a user, i want the space between diverging plates to be filled with oceanic crust"

**Acceptance Criteria**:  
- [ ] oceanic crust get's created between divergent plates
- [ ] the new oceanic crust get's added to the plate on their side of the mid ocean ridge
- [ ] the age of the oceanic crust is kept track off

### Adding subduction zones
> "As a user, I want to mark convergent boundaries as subduction zones that will inform the movement of the plates"

**Acceptance Criteria**:  
- [ ] I can draw a polyline that is considered as a subduction zone

### Subduction of oceanic crust and other features
> "As a user, I want to see features like the oceanic crust disapear as they get subducted"

**Acceptance Criteria**:
- hen a feature that would not create collisions (oceanic plates, mid ocean rifts ...) crosses a subduction zone, it's geomtry get's updated in order to give the impression that it "dissapears" under the subduction zone

---
## 3.5 Colliding
### Collision detection
> "As a user, I want to be notified when major features collide (mainly island arcs and plates)"

**Acceptance Criteria**:
- [ ] the application correctly notifies the user when a collision happens
- [ ] the time of the collision is recorded
- [ ] the animation creates a step at the time of the collision

### Small collision management
> "As a user, when a minor collision occurs (island arc vs plate), i want the island arc to automatically be added as "accreted terrain" to the plate"

**Acceptance Criteria**:
- [ ] the island arc turns into accreted terrain
- [ ] the new accreted terrain is added as a feature of the colliding plate
- [ ] the surface of the accreted terrain correspond to the expected surface of the island arc at the time of collision

### Major collision management
>"As a user, when a major collision occurs (plate vs plate), i want to be able to keep track of the features the "disapear in this collision" as well as manage the various deformations of geometry that occurs in the collision."

**Acceptance Criteria**:
- [ ] the features caugh in the collision are remembered (for things like tracking fossils)
- [ ] a zone of orogenie is suggested 
- [ ] the user can define a collision rift between the two colliding plates
- [ ] the user can modify the geometry of the newly formed plate

---
## 3.6 Feature indications

### Island Arcs indication
>"As a user, I want to be able to see the expected location and size of island arcs as oceanic crust get subducted"

**Acceptance Criteria**:
- [ ] a zone is correctly displayed behind a subduction zone to indicate the location of expected island arcs
- [ ] with the simulation the area of the zone (in km^2) correctly evolves based on the formula : length of the IA (km) x age of IA (in Mya))/2

### Hotspot placement and trail indication
> "As a user, I want to be able to place hotspots on the globe and to see the zone of the expected trails of the volcanic activity"

**Acceptance Criteria**:
- [ ] I can correctly see the path of volcanic activity left by the hotspot
- [ ] The expected location of remaining geologic traces of the hotspot are indicated with a sort of "teardrop" shape

### Large ignious provinces
> "As a user, I want to be able to draw a large ignious province and choose if the province is active or inactive"

**Acceptance Criteria**:
- [ ] have access to a large ignious province tool
- [ ] the large ignious province can be set as active or inactive
- [ ] the age of the ignious province is remembered

### Orogenies indications
> "As a user, I want to be informed of the expected locations of the various orogenies of the plates based on their movements"

**Acceptance Criteria**:
- [ ] locations of expected orogenies are dispayed on the plates
- [ ] active/passive state of the orogenies can be set
- [ ] the age of the orogenies is kept track of as well as the time since the orogenie was active

## 3.7 Static tools
those are options that are not relevant in the actual simulation process but allows the user to polish a specific state of the map.

### automatic oceanic shelf carving
> "As a user, I want to have an option to autmatically carve the appropriate depth into the oceanic shelf in order to have a more accurate picture of the actual landmasses

### dynamic feature detailing
> "As a user, I want to be able to easilly detail the features of my project"

### dynamic topology generation
> "As a user, I want the application to be able to give me a rough idea of the topology of the continents and the ocean 

### Expanded topologic tools
> "As a user, I want to be able to draw the topology of my map directly on the sphere with a set of vector tools"


---
## 3.8 Options and export

### switch between 3D and projection
> "As a user, I want to be able to switch my view between the 3D view of the globe and a projection, as well as change the origin point of the projection"

**Acceptance Criteria**:
- [ ] switch between 3D view and projection view
- [ ] change the type of projection
- [ ] change the origin point of the projection

### change color settings
> "As a user, I want to be able to change the fill and outline colors of different features as well as enable a heatmap colloration for features where age are important"

**Acceptance Criteria**:
- [ ] modify the fill color of a feature
- [ ] modify the outline color of a feature
- [ ] color features based on their age with a heatmap

### Importing reference
> “As a user, I want to overlay an equirectangular image on the globe for reference.”

**Acceptance Criteria**:  
- Upload an image.  
- Overlay toggles (opacity, visibility).  
- Aids in aligning features to real or custom maps.

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

1. **3D Globe Visualization**  
   - Basic globe in Three.js

2. **Polygon and Polyline Drawing & Storage**  
   - Draw polygonal features on the globe in a "node by node" fashion.  
   - Store data
   - edit a created poligon by adding, deleting

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
- Improvement over GPlates
   - not having to create collections
   - not having to save manually each collection
   - not having to manage IDs
   - not having to manually clone and modify plate once split happens
   - not having to specify start time and end time for every feature
   - not having to maintain the rotation.rot file
   - not having to manually manage flowlines, mid ocean ridges and newly created ocean crust
   - Informing the user of where features should go based on their decisions (subduction zones, island arcs, orogenies)
   - automatically delete subducted features
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

## 6.0 Key Challenges and objectives
- Balancing **Accessibility** and **Scientific accuracy** : This project should be available and usable by the largest number of worldbuilder while still beeing a real help to making scientifically robust geologic history. Things like the UI and the workflow should not hinder the accuracy of the tool while still having a small learning curve and encouraging an iterative process and experimentation.
- Balancing **Performance** and **Complexity** : The hardware of the user should not be a roadblock to them using the service, it should feel fast in order to not stop the creative process. At the same time, things like manipulation and colision checks of polygons on a sphere can be complexe and computationally heavy. Solutions have to be found in order to manage those two aspects of the project.
- Focusing on what is important : The premice of this project is quite complexe, therefore an effort should be made in order to avoid unnecessary complexity where it is possible.

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
