# gdoyle87.github.io

This repository hosts my **default GitHub Pages site** at:

`https://gdoyle87.github.io/`

---

## Purpose

- Acts as a **hub** for all my GitHub Pages projects.
- Serves a **custom 404 page** that can redirect users to the correct URL if they type the wrong case for a project folder.
- Keeps all *real* project content in **separate repos** so there are no path collisions.
- Publishes from the `/docs` folder so repo files (like this README) are not deployed.

---

## Structure

```
/
├── README.md        ← Repo documentation (not published)
└── docs/
    ├── index.md     ← Landing page listing projects
    └── 404.html     ← Custom 404 page with redirect logic
```

---

## Workflow

### Adding a New Project

1. **Create a separate repo** for the project.  
   - Enable GitHub Pages in that repo’s settings.
   - The published URL will follow the pattern:  
     `https://gdoyle87.github.io/<RepoName>/`

2. **Update the hub’s landing page**:  
   - Edit `/docs/index.md`.
   - Add a new list item under the relevant section:

     ```markdown
     - [PROJECT NAME](https://gdoyle87.github.io/ProjectName/) — Short description
     ```

3. **Add a redirect entry (if needed)**:  
   - If the repo name contains uppercase letters, edit `/docs/404.html`.
   - Find the `map` object in the `<script>` tag:

     ```javascript
     const map = {
       "comp2701": "COMP2701"
     };
     ```

   - Add a new lowercase→correct-case mapping:

     ```javascript
     const map = {
       "comp2701": "COMP2701",
       "projectx": "ProjectX"
     };
     ```

4. Commit and push changes to both repos. Pages will auto-deploy.

---

### Updating the 404 Redirect Logic

- `/docs/404.html` contains JavaScript that:
  - Reads the first segment of the requested URL.
  - Checks if it exists in the `map` object (case-insensitive).
  - If it finds a match, it redirects to the correct-case path.
  - If no match is found, the standard 404 message is shown.

- Only update the `map` — do **not** create folders inside `/docs` with the same name as project repos, or you will override their Pages content.

---

### Deployment

- This site is published from the `/docs` folder on the `main` branch.
- Any changes committed to `/docs` are automatically deployed within ~1 minute.
- No GitHub Actions or manual deploy steps are required.

---

## Safety Notes

- **Never** host a project’s actual content here — always in its own repo.
- Use this repo only for:
  - `/docs/index.md` — hub/landing page.
  - `/docs/404.html` — redirect logic and custom 404 display.
- Keep documentation for the hub itself in the repo root (like this README).

---
