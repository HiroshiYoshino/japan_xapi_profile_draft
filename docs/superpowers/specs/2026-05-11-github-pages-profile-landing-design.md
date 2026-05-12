# GitHub Pages Profile Landing Design

## Goal

Create a clear GitHub Pages landing page under `pages/` that introduces the xAPI Japan Profiles draft and guides readers to the four published v1.0.0 domain profiles.

## Audience

- Education DX vendors and implementers evaluating the profile documents.
- Project stakeholders who need a concise overview before reading the detailed Markdown specifications.
- Developers who need direct links to the source profile files.

## Content

The page will present:

- `xAPI Japan Profiles` as the primary brand signal.
- A short explanation that the repository manages draft xAPI profiles for Japanese education DX learning logs.
- Four domain profiles:
  - Assessment: CBT and digital drill learning logs.
  - ebook: electronic textbook and digital material operation logs.
  - LMS: learning assignment distribution, submission, and evaluation logs.
  - Group Learning Support Tool: reactions and interaction logs in collaborative learning.
- A short implementation-oriented section explaining that the profiles are based on xAPI 1.0.3, are positioned as recommended expression assets, and use StatementTemplate and Rules descriptions.
- Calls to action linking to each profile Markdown file and the repository README.

## Visual Direction

Use a quiet standards-document tone: a white surface, strong black typography, thin rule lines, and one blue-green accent. The hero should feel like a public specification entry point, with a simple line-based data-flow visual rather than a generic SaaS card grid.

## Interaction

- Hero title and visual elements enter with a short staggered animation.
- Sections reveal on scroll.
- Profile rows respond on hover and focus by strengthening the accent line and link affordance.

## Architecture

Use buildless static files so GitHub Pages can publish `pages/` directly:

- `pages/index.html`: semantic page content and links to profile Markdown files.
- `pages/styles.css`: responsive layout, typography, visual system, and motion.
- `pages/script.js`: small progressive-enhancement script for scroll reveal state.

No external build tooling, package dependencies, or generated assets are required.

## Testing

Verify with:

- File existence checks for `pages/index.html`, `pages/styles.css`, and `pages/script.js`.
- Static link checks to ensure all referenced local profile files exist.
- Basic HTML sanity check by scanning for the expected title, profile names, stylesheet, and script references.
