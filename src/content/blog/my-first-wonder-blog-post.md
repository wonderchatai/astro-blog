---
title: "Bootstrapping Astro with WonderChat AI: A Journey"
pubDate: "2023-10-27"
description: "An iterative development and debugging journey to build an Astro blog using WonderChat AI."
author: "Wonder AI"
tags: ["astro", "blog", "development", "ai", "github-actions", "tailwind"]
---

Welcome! This post details the iterative process of building and deploying this Astro blog from scratch, guided entirely by **WonderChat AI**.

## 1. Project Initialization & GitHub Actions Workflow

Our goal was to set up an Astro project in the repository root via a GitHub Actions workflow. Initial prompts covered:

*   Creating a `workflow_dispatch` action.
*   Initializing Astro with Tailwind (`npm create astro@latest .` and `npx astro add tailwind`).
*   Configuring a `.gitignore`.

**Challenge:** `npm create astro`, even with `.` as a target, sometimes created a nested project directory instead of using the root.

**Solution:** Modified the workflow to:
1.  Create Astro in a `temp-astro` subdirectory.
2.  `cd` into `temp-astro`, run `npx astro add tailwind`, and crucially, `rm -rf .git` to remove the temporary Git repository.
3.  `cd` back to the root.
4.  Move all files (including hidden, excluding `.git`) from `temp-astro` to the root: `mv temp-astro/* . || true` and `mv temp-astro/.* . || true`.
5.  Recursively remove `temp-astro` with `rm -rf temp-astro`.

## 2. Git and CI/CD Permissions

Integrating with GitHub required careful permission management:

*   **Issue:** Workflow `git push` operations failed due to insufficient permissions.
*   **Solution:** Added `permissions: contents: write` to the workflow job.

*   **Issue:** `non-fastforwardable reference` errors and `git pull` failures when local and remote branches diverged.
*   **Solution:** Employed `git pull` (and occasionally `git hard reset` on the user's side) to synchronize states.

## 3. GitHub Pages Deployment & Link Resolution

Deploying to GitHub Pages as a subpath introduced URL challenges:

*   **Issue:** Blog links resulted in 404 errors (e.g., `/astro-blogblog/`).
*   **Solution:** Corrected `astro.config.mjs` to include a trailing slash in the `base` URL: `base: '/astro-blog/'`. Updated internal links in `.astro` components to use `import.meta.env.BASE_URL` for proper prefixing.

## 4. Tailwind CSS Integration

Styling initially appeared broken despite Tailwind installation:

*   **Issue:** Tailwind CSS build warnings indicated a missing `content` option in the configuration, leading to no generated styles.
*   **Solution:** Created a `tailwind.config.mjs` file in the root, explicitly defining the `content` array to scan Astro project files: `content: ['./src/**/*.{astro,html,js,jsx,md,mdx,svelte,ts,tsx,vue}']`.
*   **Issue:** Tailwind CSS version mismatch with `@astrojs/tailwind`.
*   **Solution:** Downgraded `tailwindcss` in `package.json` to a v3-compatible version (e.g., `^3.0.24`) to match the `@astrojs/tailwind` peer dependency.

---