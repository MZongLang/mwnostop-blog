# Homepage Welcome Animation Design

## Goal

Replace the current blog homepage with an animated welcome experience based on the provided blue-sky image. The first screen should feel like a living version of the image: slow floating clouds, birds in flight, and a large code-rendered `welcome` word. On click, the `welcome` word enlarges and fades as the visitor enters the blog content screen.

## Scope

- Use the supplied image as the first-screen sky background.
- Render the main `welcome` text in HTML/CSS so it can animate independently from the image.
- Add lightweight cloud drift and bird flight using CSS animations and small inline SVG/CSS shapes.
- Add a click transition from the welcome screen to the second screen.
- Replace the current homepage body with a first-screen animation and a second-screen blog template.
- Keep the implementation static-site friendly for Astro and GitHub Pages.

## Architecture

The implementation will stay in the existing Astro structure:

- `src/pages/index.astro` will define the homepage markup, blog post lookup, first-screen welcome stage, and second-screen blog template.
- `src/styles/global.css` will define the animation, layout, responsive behavior, and transition states.
- `public/images/` will hold the supplied sky image so Astro can serve it as a static asset.
- A small inline script on the homepage will add an `entered` state after click or keyboard activation.

No animation library is needed. CSS keyframes are enough for this effect and keep the page fast.

## Interaction

The first screen fills the viewport. It contains the background image, soft moving cloud overlays, several animated birds, and the centered `welcome` text. The screen acts like a button with keyboard support.

When the visitor clicks the first screen, presses Enter, or presses Space:

- the homepage root receives an `entered` class;
- `welcome` scales up and fades;
- the hero overlay fades back;
- the second screen becomes the active visual focus;
- the page scrolls smoothly to the second screen after the transition begins.

## Second Screen Template

The second screen will be a simple personal blog landing layout:

- a short intro block for the blog;
- primary links to posts and about pages;
- latest post card if a post exists;
- a compact empty state if there are no posts.

The template should be polished but easy to revise later.

## Accessibility And Motion

- The welcome screen must be keyboard reachable.
- The clickable stage must have an accessible label.
- Users with `prefers-reduced-motion: reduce` should see a static or near-static version, with the click transition shortened.
- The second screen content must remain readable without JavaScript.

## Verification

- Run the Astro build.
- Start the local dev server and inspect the homepage.
- Check desktop and mobile widths for text fit, non-overlap, and a visible first-screen image.
- Click the welcome screen and confirm the transition reaches the second screen.

