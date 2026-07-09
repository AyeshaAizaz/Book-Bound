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

### 3. Comprehensive Book Evaluation & Review Sheet
A highly detailed, two-column data entry workspace built for deep reading reflections:
* **Metadata Grouping (Left Card):** Quick text fields for Title, Author, Genre, Page Count, and Calendar date tracking (`Started:` and `Ended:`).
* **Visuals & Metrics (Right Column):** Displays the fetched network cover image alongside an interactive five-star metric slider split across five distinct criteria: *Overall Score*, *Plot Quality*, *Ending Impact*, *Characterization*, and *Spice Level*.
* **Deep Reflections Section:** Dedicated text fields to capture long-form summary notes, favorite thoughts, newly discovered facts, and interesting vocabulary words learned during reading.

### 4. Dual-Layer Start Sequence
* **Native Pre-Boot Loader:** Powered by `flutter_native_splash`, it locks the device screen to an exact background color hex token during the native cold start, eliminating blank white device screen flashes.
* **MVC Animated Core Splash:** Seamlessly transitions into a 1.5-second `CurvedAnimation` layout sequence featuring a smooth opacity fade-in paired with a gentle scale-up effect while internal disk repositories initialize.

### 5. Persistent Local Storage
* Utilizes key-value localized device caching (`SharedPreferences` or local JSON mapping) to permanently store user book documents, active reading states, and individual metric matrices completely offline.

---

## 🏗️ Technical Highlights & Architecture

### The MVC Structural Blueprint
The application strictly isolates state, business logic, and UI display rendering into independent architectural layers:
* **Model Layer (`ReviewModel`):** Implements an entirely immutable data blueprint where all properties are declared `final`. State mutations are safely processed via explicit cloning (`copyWith`) to ensure zero runtime side effects.
* **Controller Layer (`ReviewPageController`, `HomePageController`):** Encapsulates backend storage tasks, sanitizes raw text data arrays, and manages state variables. 
* **View Layer (`ReviewPage`, `HomePage`):** Operates as a passive UI wrapper that reacts to controller updates using performance-optimized `ListenableBuilder` widgets.

### Core Optimization Mechanisms
* **The Text Cursor Guard Loop:** Inside the `ReviewPageController`, user-typed date strings (`DD/MM/YYYY`) are cleanly parsed into native `DateTime` structures without dispatching interface refresh signals, keeping the user's software keyboard cursor position perfectly stable while they type.
* **Wireframe Silhouette Pre-Loading:** Powered by the `Skeletonizer` package. When the application fetches data from disk, the layout places a structural blueprint layer using dummy placeholder text lengths (e.g., `"00/00/0000"` or `"000"` pages) to keep layout dimensions 100% accurate before data settles.

---

## Screenshots and Visuals Blueprint
**ANIMATED MVC SPLASH PAGE**: Smooth scale-up and fade-in reveal introducing the application title and its ambient literary subtitle, transitioning seamlessly into the home layout.

### 📚 DASHBOARD SHELF MANAGEMENT
**HOME PAGE (TO BE READ SHELF)**: Displays the staggered shelves with plants on alternating sides, holding books you plan to read.

<img width="1080" height="2400" alt="Screenshot_2026-07-10-00-15-24-014_com example bookbound 1" src="https://github.com/user-attachments/assets/94fd59ff-4392-4774-b750-d728c741a15b" />


**ARCHIVE VIEW (READ SHELF)**: Your library of completed journeys, cleanly organized on matching virtual wooden beams.

<img width="1080" height="2400" alt="Screenshot_2026-07-10-00-15-28-649_com example bookbound 1" src="https://github.com/user-attachments/assets/92bf2264-a4a3-4b30-9a10-593c37daaf64" />


**CONTEXT MENU PANE / BOTTOM MODAL SHEET**: Triggered by a long-press on any book tile. Provides clean quick-action options to move books between shelves or delete them from your library.

<img width="1080" height="2400" alt="Screenshot_2026-07-10-00-15-57-170_com example bookbound 1" src="https://github.com/user-attachments/assets/6942fd3e-fb86-4781-8895-37ba45e59cab" />

### 🔎 LITERARY EXPLORATION
**SEARCH WORKSPACE INTERFACE**: A clean text entry field matching the app theme that polls the OpenLibrary engine as you type.

**SEARCH RESULTS LIST TILES**: Displays clean row items containing cover thumbnails, titles, authors, and initial sentence preview snippets.

<img width="1080" height="2400" alt="Screenshot_2026-07-10-00-15-45-514_com example bookbound 1" src="https://github.com/user-attachments/assets/40efa4c6-a0f6-476a-9015-9a150befc346" />

### 📝 JOURNALING & ANALYTICS
**BOOK REVIEW PAGE (INITIAL DATA WIREFRAME)**: The clean Skeletonizer layout view displaying ambient placeholder structures while reading local database caches.

**BOOK REVIEW PAGE (ACTIVE WORKSPACE)**: The complete two-column metadata, slider metrics, and comprehensive notes dashboard.

**IMAGE SELECTOR / CHANGE DISPLAY PICTURE**: Clean overlay card to manually change or refresh book cover image assets.

<img width="1080" height="2400" alt="Screenshot_2026-07-10-00-21-58-662_com example bookbound 1" src="https://github.com/user-attachments/assets/2ad418c8-3ea6-4709-b013-4c777fc83070" />

<img width="1080" height="2400" alt="Screenshot_2026-07-10-00-16-11-716_com example bookbound 1" src="https://github.com/user-attachments/assets/52a852e0-a88d-40e3-9678-5ec81953f46a" />

## Future Vision
**Advanced Hybrid Syncing**: Upgrade the local caching architecture to synchronize seamlessly with cloud databases for multi-device access.

**Rich Text Notes Editor**: Transform the plain-text review boxes into an advanced editor supporting markdown headers, quote blocks, and reading-progress timestamps.

**Social Reading Circles**: Introduce minimal, private reading groups where close friends can view each other’s staggered bookshelves, shared reviews, and custom metric evaluations.

**Literary Insights Dashboard**: Build an interactive data graph interface showing monthly reading streaks, favorite genres, average plot scores, and vocabulary growth over time.
