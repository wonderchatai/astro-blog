**Built with [WonderChat AI](https://wonderchat.dev).**

<a href="https://apps.apple.com/us/app/wonderchat-ai/id6752497385" target="_blank">
  <img src="https://developer.apple.com/assets/elements/badges/download-on-the-app-store.svg" alt="Download on the App Store" height="50">
</a>

This Astro blog was entirely prompted, developed, and debugged through an iterative process with **WonderChat AI**. Key steps and challenges overcome include:

*   **Astro Project Setup:** Created a GitHub Actions workflow to initialize the Astro project at the repository root, addressing issues with `npm create astro` creating nested directories by using a temporary directory strategy and explicitly removing the temporary `.git` folder.
*   **GitHub Actions & Git Integration:** Debugged and resolved GitHub Actions `contents: write` permissions, and handled Git push/pull conflicts arising from workflow-initiated commits.
*   **GitHub Pages Deployment:** Fixed 404 errors by correctly configuring `site` and `base` URLs in `astro.config.mjs`, ensuring the `base` path included a trailing slash for subpath deployments.
*   **Tailwind CSS Configuration:** Resolved Tailwind CSS styling issues, including dependency version mismatches and the crucial "content option missing" warning, by creating and configuring `tailwind.config.mjs`.

This project demonstrates an AI-driven development workflow, showcasing how WonderChat AI can assist throughout the entire software engineering lifecycle.
