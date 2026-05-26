# Kudanil-Inspired Homepage Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build the approved immersive luxury expedition yacht homepage inside the existing Halo Vite theme.

**Architecture:** A new homepage-only layout owns the overlay navigation and branded footer, while
all existing content routes retain their starter layout. The homepage is mostly editorial static
content, with the Journal card row driven by Halo's existing `posts` view model and minimal
TypeScript progressive enhancement.

**Tech Stack:** Halo 2 Thymeleaf templates, `@halo-dev/vite-plugin-halo-theme`, CSS, TypeScript,
Vite Plus, in-app Browser validation.

---

### Task 1: Isolate the homepage presentation shell

**Files:**

- Create: `src/partials/home-layout.html`
- Modify: `src/index.html`

- [ ] **Step 1: Add a homepage-only HTML shell**

Create `home-layout.html` with the regular head script inclusion, absolute voyage header,
anchor navigation, `<slot />` content position, and voyage footer. It must not replace
`partials/layout.html`, because post, page, and archive templates need their existing document
shell.

- [ ] **Step 2: Replace the index starter markup**

Write semantic sections with ids `destinations`, `yacht`, `experiences`, `story`, `journal`, and
`contact`. Use the approved headline and section content; loop over:

```html
<article
  class="voyage-journal-card"
  th:each="post, postStat : ${posts.items}"
  th:if="${postStat.index < 3}"
>
  <a th:href="@{${post.status.permalink}}" th:text="${post.spec.title}"></a>
</article>
```

Add a `th:if="${#lists.isEmpty(posts.items)}"` empty state.

- [ ] **Step 3: Build to check template preprocessing**

Run: `pnpm build-only`

Expected: build exits `0` and writes `templates/index.html` with the voyage sections.

### Task 2: Implement the approved visual system and motion

**Files:**

- Modify: `src/css/main.css`
- Modify: `src/js/index.ts`

- [ ] **Step 1: Add homepage CSS tokens and section layouts**

Add `.voyage-*` rules for the approved palette, serif display typography, overlay header, full
viewport hero, destination panels, yacht block, experience cards, story split, Journal row, press
band, charter CTA, footer, and breakpoints. Keep existing non-home CSS rules usable by the other
templates.

- [ ] **Step 2: Add progressive enhancement**

Replace the placeholder log in `index.ts` with:

```ts
const header = document.querySelector<HTMLElement>(".voyage-header");
const reveals = document.querySelectorAll<HTMLElement>("[data-reveal]");

const updateHeader = () => header?.classList.toggle("is-scrolled", window.scrollY > 32);
updateHeader();
window.addEventListener("scroll", updateHeader, { passive: true });

if ("IntersectionObserver" in window) {
  document.documentElement.classList.add("has-reveal-motion");
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add("is-visible");
          observer.unobserve(entry.target);
        }
      });
    },
    { threshold: 0.14 },
  );
  reveals.forEach((element) => observer.observe(element));
}
```

- [ ] **Step 3: Build to validate CSS and TypeScript**

Run: `pnpm build-only`

Expected: TypeScript and Vite complete without errors.

### Task 3: Rendered Halo verification

**Files:**

- Verify: `templates/index.html`
- Verify: `src/partials/layout.html` remains unchanged

- [ ] **Step 1: Check generated output and local Halo response**

Run: `curl -I 'http://localhost:8090/?preview-theme=theme-company-site'`

Expected: `HTTP/1.1 200 OK`.

- [ ] **Step 2: Inspect the rendered homepage in Browser**

Open the preview route at desktop and mobile widths; confirm meaningful first-viewport content,
the complete section sequence, the Journal article card populated from Halo, navigation anchor
interaction, and no relevant console errors or framework overlay.

- [ ] **Step 3: Compare to accepted concept**

Capture final screenshots outside committed source and directly inspect them beside the approved
concept screenshot. Fix material hierarchy, spacing, image, typography, or responsive mismatches
before reporting completion.
