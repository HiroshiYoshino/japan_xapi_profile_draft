# GitHub Pages Profile Landing Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a static GitHub Pages landing page under `pages/` that introduces the xAPI Japan Profiles draft and links to each v1.0.0 domain profile.

**Architecture:** Use plain HTML, CSS, and a tiny JavaScript enhancement so the page can be served directly from GitHub Pages without a build step. Keep content in `index.html`, presentation in `styles.css`, and scroll reveal behavior in `script.js`.

**Tech Stack:** Static HTML5, CSS3, vanilla JavaScript.

---

### Task 1: Static Page Content

**Files:**
- Create: `pages/index.html`
- Create: `pages/styles.css`
- Create: `pages/script.js`

- [ ] **Step 1: Add semantic HTML**

Create `pages/index.html` with:

```html
<!doctype html>
<html lang="ja">
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <title>xAPI Japan Profiles</title>
  <meta name="description" content="日本の教育DXにおける学習ログ標準化を目指す xAPI Japan Profiles ドラフトの紹介ページです。">
  <link rel="stylesheet" href="./styles.css">
</head>
<body>
  <main>
    <section class="hero" aria-labelledby="hero-title">
      <div class="hero__content">
        <p class="eyebrow">Draft profile collection for education data interoperability</p>
        <h1 id="hero-title">xAPI Japan Profiles</h1>
        <p class="hero__lead">日本の教育DXにおけるスタディ・ログを、領域をまたいで読み解ける共通表現へ。</p>
        <div class="hero__actions" aria-label="主要リンク">
          <a class="button button--primary" href="../README.md">概要を読む</a>
          <a class="button button--secondary" href="#profiles">Profileを見る</a>
        </div>
      </div>
    </section>
  </main>
  <script src="./script.js"></script>
</body>
</html>
```

- [ ] **Step 2: Add responsive styling**

Create `pages/styles.css` with a quiet white/black/blue-green visual system, responsive type, full-bleed hero, profile rows, implementation notes, and reduced-motion support.

- [ ] **Step 3: Add scroll reveal enhancement**

Create `pages/script.js` with an `IntersectionObserver` that adds `is-visible` to `[data-reveal]` elements and immediately reveals content when the API is unavailable.

- [ ] **Step 4: Verify local references**

Run:

```bash
test -f pages/index.html && test -f pages/styles.css && test -f pages/script.js
```

Expected: exit code `0`.

- [ ] **Step 5: Verify linked profile files**

Run:

```bash
test -f assessment/v1.0.0/assessment_profile.md && test -f ebook/v1.0.0/ebook_profile.md && test -f lms/v1.0.0/lms_profile.md && test -f group-lst/v1.0.0/group-lst_profile.md && test -f README.md
```

Expected: exit code `0`.

- [ ] **Step 6: Verify page content**

Run:

```bash
rg "xAPI Japan Profiles|Assessment|ebook|LMS|Group Learning Support Tool|styles.css|script.js" pages
```

Expected: matches in `pages/index.html` plus stylesheet/script references.
