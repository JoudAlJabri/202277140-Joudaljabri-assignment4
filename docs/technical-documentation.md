# Technical Documentation
**Student:** Joud AlJabri — 202277140
**Assignment:** 4 — Personal Web Application

---

## 1. Overview

This portfolio is a three-page static website built with plain HTML, CSS, and JavaScript. It presents my work, skills, projects, blogs, and contact information in a personal aesthetic I designed myself — dark background, soft pink and green accents, and serif typography using the Bellefair font.


---


## 2. Project Structure

```
202277140-JoudALJabri-assignment2/
├── index.html           # Main portfolio page
├── projects.html        # Full projects archive page
|── blogs.html           # Full blogs page
├── css/
│   ├── index.css        # Global styles + all index page section styles
│   └── projects.css     # Styles specific to the projects archive page
|   └── blogs.css        # Styles specific to the blogs page
├── js/
│   └── script.js        # All JavaScript features
├── assets/
│   ├── icons/           # SVG icons (GitHub, LinkedIn, Email)
│   ├── images/          # Project screenshots
│   └── sparkles/        # Decorative PNG assets
└── docs/
|    ├── technical-documentation.md
|    └── ai-usage-report.md
|-- presentation/
    ├── demo-video.mp4
    └── slides.mp4
```

**CSS is organized into two files:** `index.css` handles global resets, CSS variables, the navbar, and every section on the main page. `projects.css` handles the layout and filter bar specific to the projects archive.  `blogs.css` handles the layout and 2-level filter bar specific to the blogs archive. This avoids loading unnecessary styles on each page.

**JavaScript is centralized** in one `script.js` file, loaded at the bottom of `index.html`. `projects.html` has its own small inline script for the filter feature since it does not share the main script.

---

## 5. Pages

### index.html — Main Portfolio
Contains the following sections in order:
- **Navbar** — fixed, blurs on scroll, has section links
- **Hero** — name, title, social links, floating sparkle decorations
- **Quote of the Day** — live API fetch with a button
- **About Me** — short bio and interests
- **Tech Stack** — skills grouped into 4 cards
- **Projects** — 3 featured project cards with a link to the full archive
- **Latest Fromm Github NEW** — display the 3 latest project from github
- **Contact** — validated contact form
- **Footer**

### projects.html — Full Archive
Contains all 13 projects with a filter bar that lets visitors filter by category: All, Mobile, Web, Python & Data, OOP, and UI/UX. Each project card has tags, a description, and links.

### blogs.html - visual diary
Contains a two-level filteration of both university and travel moments. The university also contains 3 sub filters only the first (at the moment) is filled which is the computer club section, inluding a time-line style display of my favorite perosnal moments as a leader in the club. 

---

## 6. JavaScript Features

All features are in `js/script.js`.

### 6.1 Time-Based Greeting
On page load, `displayGreeting()` reads the visitor's local time using `new Date().getHours()` and updates the hero greeting text dynamically:

- Before 12:00 → "Good Morning, I'm"
- 12:00–17:59 → "Good Afternoon, I'm"
- 18:00 onward → "Good Evening, I'm"

This is a dynamic content feature that personalises the page on every visit without any user action required.

### 6.2 Quote of the Day (Public API)
A "New Quote" button triggers `getQuote()`, an `async` function that fetches a random quote from the public API `https://dummyjson.com/quotes/random`. The API requires no key and returns a JSON object with `quote` and `author` fields, which are injected into the page.

Error handling is included: if the fetch fails (e.g. no internet), the quote element displays "Failed to load quote." so the user is never left without feedback.

### 6.3 Contact Form Validation
On submit, the form is validated in JavaScript before any success state is shown:

- **Name** — must not be empty
- **Email** — must not be empty and must match the pattern `/^[^\s@]+@[^\s@]+\.[^\s@]+$/`
- **Message** — must not be empty

If validation fails, a red error message is injected directly below the offending field and the field border turns red. All errors are cleared and re-evaluated on each submission attempt. On success, the button text changes to "✓ Sent!" and the fields clear. The button resets after 3 seconds.

### 6.4 Smooth Scroll Navigation
Clicking any nav link that points to an on-page section (`#home`, `#about`, etc.) uses `smoothScrollTo()` instead of the browser default jump. The function offsets the scroll target by the navbar height (72px) so the section heading is never hidden behind the fixed navbar.

Clicking the nav logo scrolls back to the top of the page.

### 6.5 Navbar Scroll Shadow
A `scroll` event listener adds the class `.scrolled` to the navbar once the user scrolls past 20px, which applies a box shadow. This gives a visual cue that the navbar is floating above content.

### 6.6 Project Filter (projects.html)
An inline script on `projects.html` listens for clicks on the filter bar buttons. Each project card has a `data-category` attribute. When a filter button is clicked, cards that do not match are hidden with `display: none` and the active button is highlighted. The "All" filter restores all cards.


### 6.7 Loading Github Repos
loadGitHubRepos() fetches https://api.github.com/users/Joudii18/repos?sort=updated&per_page=3 and renders cards showing: Repo name (links to GitHub), description, language, star count, fork count, and error message if the API fails

---

## 7. CSS & Animations

### CSS Variables
All colours, fonts, and recurring values are defined as custom properties in `:root` inside `index.css`, making the theme easy to adjust from one place.

### Animations & Transitions
- **Hover transitions** — nav links, buttons, and project link buttons all have `transition: color/background/opacity 0.2s` for smooth hover feedback.
- **Form focus** — inputs and textareas transition their border colour to pink on focus.
- **Floating sparkles** — the decorative sparkle images in the hero section use a `@keyframes float` animation that gently moves them up and down on a 6-second loop, with staggered `animation-delay` values so they don't move in sync.
- **Form validation errors** — error messages appear and disappear dynamically, giving immediate animated feedback.

### Responsive Design
Media queries handle layout changes at three breakpoints:

| Breakpoint | Changes |
|---|---|
| `max-width: 768px` (index) | Single-column tech grid, smaller sparkles or hidden, single-column project grid |
| `max-width: 900px` (projects) | Projects grid reduces to 2 columns |
| `max-width: 600px` (projects) | Projects grid becomes single column |

---

## 8. Accessibility & Best Practices

- All decorative images use `alt=""` so screen readers skip them.
- Meaningful images (project screenshots) have descriptive `alt` text.
- Form inputs use `autocomplete` attributes (`name`, `email`) to assist browser autofill.
- External links use `target="_blank" rel="noreferrer"` to avoid security issues with opener access.
- The HTML `lang="en"` attribute is set on both pages.
- `scroll-behavior: smooth` is set in CSS as a baseline, with the JS scroll handling layered on top for navbar offset accuracy.

---

## 9. Assignement 4 Requirements 

- Added a presentation section inlcuding both the slides and demos
- Deployed the project using GitHub web pages.
- Added a feature that represents me which is the Blogs page.
- Re-checked and improved some of the performance and quality of the code, including:
1. margin-top: 0.rem — invalid CSS, silently ignored (in index.css) → Changes to 0
2. Blogs nav link pointed to index.html#blogs-placeholder (in project.html) → Fixed to blogs.html
3. Google Fonts double-loaded (HTML <link> + CSS @import) (All 3 CSS files) → Removed @import (HTML link is faster).


--- 

## 10. External Resources Used

| Resource | Purpose |
|---|---|
| Google Fonts — Bellefair | Main typeface |
| dummyjson.com/quotes/random | Public quote API (no key required) |
| GitHub, LinkedIn, App Store | External links to my profiles and published app |
