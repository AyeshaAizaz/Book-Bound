# 🌿 Bookbound: Aesthetic Book-Tracking & Literary Journal Application

## 📋 Overview
**Bookbound** is an aesthetic, highly intentional book-tracking and literary journal application designed for passionate readers who view books as an experience rather than a mere checklist. Moving away from monotonous, text-heavy data entry apps, Bookbound leverages an organic, library-inspired interface to offer a sensory, tactile user experience reminiscent of cozy independent bookstores and premium midnight studies. 

Built using a strict, decoupled **Model-View-Controller (MVC)** state architecture in Flutter, the app integrates public book search engines, localized device caching, and an advanced dynamic bookshelf layout system to help users beautifully log current reads, plan upcoming journeys, evaluate thematic scores, and record structured literary summaries.

---

## ✨ Key Features

### 1. Dynamic Staggered Bookshelf Layout (Home Screen)
Instead of standard, rigid grid tiles, Bookbound builds a realistic, alternating library shelving matrix that expands dynamically as a user's library grows:
* **Shelf Tier A (Rows 0, 4, 8...):** Holds up to **3 Books + 1 Classic Leafy Potted Plant** aligned to the **Left**.
* **Shelf Tier B (Rows 1, 5, 9...):** Full-width expansion holding up to **4 Books** across the entire wooden beam with no decorative clutter.
* **Shelf Tier C (Rows 2, 6, 10...):** Holds up to **3 Books + 1 Trailing Jade Vine Plant Variant** shifted to the **Right**.
* **Shelf Tier D (Rows 3, 7, 11...):** Full-width expansion holding up to **4 Books**.

### 2. OpenLibrary API Search Engine
Integrates with the public OpenLibrary search engine via asynchronous HTTP channels to easily add books to shelves:
* **Direct Field Targeting:** Uses an explicit parameter pipeline (`fields=key,title,author_name,cover_i,first_sentence`) to capture book details while minimizing device bandwidth payloads.
* **Snippet Summaries:** Extracts the `first_sentence` array element directly inside the search view to act as a quick list preview.
* **Work Key Resolution:** Pulls the unique OpenLibrary Work ID (`/works/OLXXXXW`) to facilitate deep fetching for full descriptions on demand.

### 3. Comprehensive Responsive Evaluation & Review Sheet
A highly detailed, adaptive data entry workspace built for deep reading reflections that handles screen space elegantly:
* **Responsive Visual Split (`isMobile` Check):** Automatically detects viewport constraints. On tablets/wider screens, it maintains a gorgeous two-column spread (Metadata on the left, Cover/Ratings on the right). On mobile viewports (< 650px), it seamlessly collapses into a unified, stacked column layout to entirely prevent component squeezing or rating overflows.
* **Cozy Metadata Grouping:** Quick text fields for Title, Author, Genre, Page Count, and Calendar date tracking (`Started:` and `Ended:`).
* **Tactile Metric Sliders & Dynamic "Book Hangover" Scale:** Displays five-star metric sliders across criteria (*Overall Score*, *Plot Quality*, *Ending Impact*, *Characterization*, and *Spice Level*). Includes a customized **Book Hangover Slider** that dynamically maps values (1.0 to 5.0) to custom-tailored descriptions, colors, and reactive icons (e.g., *1 - Ready for the next book* 🟢 up to *5 - Completely devastated* 🔴), wrapped to stay clean on narrow mobile screens.

### 4. Interactive Cozy Journaling Logs (Prompt-Driven)
The bottom half of the review sheet hosts dedicated, themed cards leveraging beautifully styled `InteractiveLearningLogCard` shapes. Each field is bound directly to the database controller and features tailored, reflective prompt hints:
* **Book Review:** *"How did this book make you feel? Write down your raw, honest thoughts..."*
* **Summary Notes:** *"Capture the heart of this story in a few sentences..."*
* **The Learning Log:** *"A new piece of trivia, history, or insight this book gifted you..."*
* **The Vocabulary Vault:** *"Any beautiful, archaic, or unique words you discovered..."*
* **The 'Stick It' Quote (Favorite Quote):** *""That one line" that you wanted to underline twice..."*
* **Who I Became (Personal Resonance):** *"Which character felt like a mirror, or what part of yourself did you find in these pages?..."*

### 5. Dual-Layer Animated Start Sequence
* **Native Pre-Boot Loader:** Powered by `flutter_native_splash`, it locks the device screen to an exact background color hex token during the native cold start, eliminating blank white device screen flashes.
* **MVC Lottie Animated Core Splash:** Seamlessly transitions into a stylized loading sequence. It features a beautifully fluid, high-performance Lottie book animation layered with a custom `CurvedAnimation` scale and opacity fade-in, greeting the reader with a warm, tactile entrance while local repositories initialize.

### 6. Persistent Local Storage
* Utilizes key-value localized device caching (`SharedPreferences` or local JSON mapping) to permanently store user book documents, active reading states, and individual metric matrices completely offline.

---

## 🏗️ Technical Highlights & Architecture

### The MVC Structural Blueprint
The application strictly isolates state, business logic, and UI display rendering into independent architectural layers:
* **Model Layer (`ReviewModel`):** Implements an entirely immutable data blueprint where all properties are declared `final`. Includes specialized fields for aesthetic logging, such as `favQuote` and `relateToMost`. State mutations are safely processed via explicit cloning (`copyWith`) to ensure zero runtime side effects.
* **Controller Layer (`ReviewPageController`, `HomePageController`):** Encapsulates backend storage tasks, sanitizes raw text data arrays, manages state variables, and hosts text-listener bindings.
* **View Layer (`ReviewPage`, `HomePage`):** Operates as a passive UI wrapper that reacts to controller updates using performance-optimized `ListenableBuilder` widgets.

### Core Optimization Mechanisms
* **Lottie Vector Rendering Engine:** Integrated using the `lottie` package to execute lightweight, fluid micro-interactions and splash sequences without the overhead or pixelation of heavy GIF files. This guarantees 60fps rendering of intricate hand-drawn book animations.
* **The Text Cursor Guard Loop:** Inside the `ReviewPageController`, user-typed date strings (`DD/MM/YYYY`) are cleanly parsed into native `DateTime` structures without dispatching interface refresh signals, keeping the user's software keyboard cursor position perfectly stable while they type.
* **Ambient Scrunched Paper Canvas:** Implements a hardware-accelerated background texture utilizing an asset overlay blended via `BlendMode.multiply` directly on top of the design's `AppColors.background`. Transparent AppBars allow the paper texture to run cohesively behind the status bar area.
* **Wireframe Silhouette Pre-Loading:** Powered by the `Skeletonizer` package. When the application fetches data from disk, the layout places a structural blueprint layer using dummy placeholder text lengths (e.g., `"00/00/0000"` or `"000"` pages) to keep layout dimensions 100% accurate before data settles.

---

## Screenshots and Visuals Blueprint
**ANIMATED MVC SPLASH PAGE**: Smooth scale-up and fade-in reveal introducing the application title and its ambient literary subtitle, transitioning seamlessly into the home layout.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/116cf862-1afe-4697-8bca-f5c1bc675a6d" />


### 📚 DASHBOARD SHELF MANAGEMENT
**HOME PAGE (TO BE READ SHELF)**: Displays the staggered shelves with plants on alternating sides, holding books you plan to read.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8e33f386-a61c-4d65-9b7e-d21a2db6e8e3" />


**ARCHIVE VIEW (READ SHELF)**: Your library of completed journeys, cleanly organized on matching virtual wooden beams.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/21c2be70-a4de-4289-92de-bc4f29894dbc" />


**CONTEXT MENU PANE / BOTTOM MODAL SHEET**: Triggered by a long-press on any book tile. Provides clean quick-action options to move books between shelves or delete them from your library.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/cde82dc2-f8d1-42b0-aa1b-b64a33616ec2" />


### 🔎 LITERARY EXPLORATION
**SEARCH WORKSPACE INTERFACE**: A clean text entry field matching the app theme that polls the OpenLibrary engine as you type.

**SEARCH RESULTS LIST TILES**: Displays clean row items containing cover thumbnails, titles, authors, and initial sentence preview snippets.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e5290500-9184-46fc-b673-85bf7bb8b71d" />


### 📝 JOURNALING & ANALYTICS
**BOOK REVIEW PAGE (INITIAL DATA WIREFRAME)**: The clean Skeletonizer layout view displaying ambient placeholder structures while reading local database caches.

**BOOK REVIEW PAGE (ACTIVE WORKSPACE)**: The complete responsive layout, featuring the customized book hangover meter, adaptive star ratings, and the extended learning log cards with creative context guides.

**IMAGE SELECTOR / CHANGE DISPLAY PICTURE**: Clean overlay card to manually change or refresh book cover image assets.

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/7a8bec0e-b120-420f-8515-a804843d2893" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/f0aa14b6-4d94-428f-8b2d-668f6c9b4c78" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/fbc05fd8-3646-438a-8732-5e899b8b3fac" />


---

## Future Vision
**Advanced Hybrid Syncing**: Upgrade the local caching architecture to synchronize seamlessly with cloud databases for multi-device access.

**Rich Text Notes Editor**: Transform the plain-text review boxes into an advanced editor supporting markdown headers, quote blocks, and reading-progress timestamps.

**Social Reading Circles**: Introduce minimal, private reading groups where close friends can view each other’s staggered bookshelves, shared reviews, and custom metric evaluations.

**Literary Insights Dashboard**: Build an interactive data graph interface showing monthly reading streaks, favorite genres, average plot scores, and vocabulary growth over time.

---

## APP LINK

[https://drive.google.com/file/d/1811nJ5Bw0m2sThjJAxKpScltqd97k67O/view?usp=drive_link](https://drive.google.com/file/d/1ud9F_3mypca4EAO5OYHwa3uNiRYsUnZt/view?usp=sharing)

## WEB APP LINK

https://bookbound-app.netlify.app/
