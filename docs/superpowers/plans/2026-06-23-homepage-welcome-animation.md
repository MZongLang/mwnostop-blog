# Homepage Welcome Animation Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build an animated first-screen welcome page for the Astro blog using the supplied sky image, floating clouds, flying birds, and a click-to-enter transition.

**Architecture:** Keep the feature inside the existing Astro static site. `index.astro` owns the homepage markup and tiny transition script, `global.css` owns visual layout and animations, and `public/images/` stores the supplied image.

**Tech Stack:** Astro 5, static HTML, CSS keyframes, minimal browser JavaScript.

---

### Task 1: Add Static Image Asset

**Files:**
- Create: `public/images/welcome-sky.png`

- [ ] **Step 1: Create the image directory**

Run: `New-Item -ItemType Directory -Force -Path public/images`

Expected: `public/images` exists.

- [ ] **Step 2: Copy the supplied image**

Run: `Copy-Item -LiteralPath C:/Users/ARTHUR~1/AppData/Local/Temp/codex-clipboard-8381eb60-d7e9-4bbf-829d-e1def9a09bd7.png -Destination public/images/welcome-sky.png -Force`

Expected: `public/images/welcome-sky.png` exists and is non-empty.

### Task 2: Replace Homepage Markup

**Files:**
- Modify: `src/pages/index.astro`

- [ ] **Step 1: Keep the blog collection lookup**

Use the existing `getCollection("blog")` sorting and `featured` selection.

- [ ] **Step 2: Replace the page body**

Add a `.welcome-home` wrapper with a clickable `.welcome-stage`, animated bird elements, code-rendered `welcome` text, and a `.blog-entry` second screen with intro, links, and latest post card.

- [ ] **Step 3: Add a small transition script**

The script should add `.entered` to `.welcome-home` and scroll to `.blog-entry` when the welcome stage is clicked or activated with Enter/Space.

### Task 3: Add Homepage Animation Styles

**Files:**
- Modify: `src/styles/global.css`

- [ ] **Step 1: Add immersive home layout styles**

Make `.welcome-home` full-width, let `.welcome-stage` fill the viewport, and position the supplied image as a cover background.

- [ ] **Step 2: Add cloud and bird animations**

Use CSS pseudo-elements and `.bird` spans with keyframes for gentle cloud drift and bird flight.

- [ ] **Step 3: Add click transition and responsive styles**

Scale/fade `.welcome-word`, soften the first screen after entry, and keep the second screen readable on mobile.

- [ ] **Step 4: Add reduced-motion handling**

Use `@media (prefers-reduced-motion: reduce)` to disable looping motion and shorten the click transition.

### Task 4: Verify

**Files:**
- No source changes expected.

- [ ] **Step 1: Run the production build**

Run: `npm run build`

Expected: Astro check and build complete successfully.

- [ ] **Step 2: Start the dev server**

Run: `npm run dev -- --host 127.0.0.1`

Expected: local server responds on port 4321 or the next available Astro port.

- [ ] **Step 3: Inspect the homepage**

Check desktop and mobile widths. Confirm the image renders, birds move, clouds drift, `welcome` text fits, and clicking the first screen reaches the second screen.

