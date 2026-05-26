# Kudanil-Inspired Homepage Design

## Goal

Transform the Halo `theme-company-site` homepage into an immersive luxury expedition yacht
landing page inspired by the public structure and visual language of Kudanil: cinematic imagery,
editorial serif typography, spacious pacing, and a narrative progression from destination to
charter enquiry.

## Reference Boundary

The live reference URL timed out repeatedly in the local browser and command-line network path.
The design is based on the publicly discoverable Kudanil page structure and the full-page concept
approved by the user in the local visual companion on 2026-05-26. Implementation will be original
Thymeleaf, HTML, CSS, and TypeScript; it will not copy third-party source code, logos, or original
site image files.

## Approved Direction

Use the full immersive long-page approach:

1. Transparent navigation over a full-viewport photographic hero with the headline
   `Adventure For The Restless Soul`.
2. Editorial introduction framing private voyages through Indonesia's islands.
3. Four photographic destination panels: Raja Ampat, Komodo, Banda Sea, and Forgotten Islands.
4. A yacht feature block with a large vessel photograph.
5. Three life-aboard experiences: unwind, dine, explore.
6. A split image/story section introducing family-led crew expertise.
7. A `Journal` section populated from Halo homepage `posts` data rather than static cards.
8. Press-style recognition band followed by a photographic charter call to action and footer.

## Visual System

- Palette: deep ocean navy `#0d2225`, warm ivory `#f6f2e9`, sand `#ebe4d6`, muted brass
  `#bd9970`, and off-white text.
- Typography: serif display headings with tight leading; small uppercase navigation and section
  labels with wide tracking; restrained sans-serif body text.
- Imagery: large expedition, island, yacht, dining, diving, and crew photographs using externally
  licensed/publicly hosted imagery selected for the approved concept. No Kudanil original image
  files are redistributed.
- Motion: subtle reveal-on-scroll and header background transition; no animation may interfere
  with content access or mobile reading.

## Theme Architecture

- Keep existing article and archive pages on `src/partials/layout.html`.
- Add `src/partials/home-layout.html` exclusively for `src/index.html`, so overlay navigation and
  the voyage footer cannot regress content pages.
- Replace the starter list in `src/index.html` with the approved long-page markup.
- Extend `src/css/main.css` with homepage-prefixed classes while preserving existing content-page
  rules.
- Replace the placeholder `src/js/index.ts` log with small progressive-enhancement behavior for
  scroll reveals and sticky navigation state.

## Halo Data Flow

The homepage receives `posts` from Halo. The Journal cards iterate through `posts.items`, showing
up to three entries using fields already exercised by the starter theme:
`post.status.permalink`, `post.spec.title`, `post.spec.publishTime`,
`post.status.excerpt`, and `post.categories`. If no posts exist, show an intentional editorial
empty state rather than leaving a blank section.

## Responsive Behaviour

- Desktop: centered wordmark and split navigation, four destination columns, three Journal cards.
- Tablet: compressed navigation and two-by-two destination cards.
- Mobile: menu anchors condensed, single-column sections, readable display type, and stacked
  cards while keeping hero impact.

## Verification

Run `pnpm build-only`, then load
`http://localhost:8090/?preview-theme=theme-company-site` in the in-app Browser at desktop and
mobile widths. Verify content is rendered, navigation anchors work, no relevant console warnings
or errors occur, the homepage retains Halo post rendering, and inner article/archive pages still
use the unchanged standard layout.
