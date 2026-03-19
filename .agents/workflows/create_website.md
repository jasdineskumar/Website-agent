---
description: Create a website locally based on requirements
---
# Create Website Workflow

1.  **Gather Requirements via Questionnaire**
    Before writing any code or deciding the architecture, you MUST present the following structured questionnaire to the user in the chat interface (acting as the GUI input form). Wait for their response before proceeding.
    
    **Website Generation Questionnaire:**
    *   **Project Name:** (What should we name the folder/project?)
    *   **Purpose & Features:** (What is the core function of this site?)
    *   **Target Audience / Tone:** (Who is this for? e.g., enterprise B2B, creative agency, personal blog)
    *   **Tech Stack:** (Standard HTML/JS/CSS or a framework like Vite/Next.js?)
    *   **Aesthetics & Vibe:** (Color scheme, typography feeling, animations?)
    *   **UI Inspiration (Optional):** (Drop any URLs, references, or attach images/files here)

2.  **Prepare the Directory**
    After gathering the requirements, create the standard project folder structure (see `CLAUDE.md`):
    ```
    <website-name>/
    ├── inspiration/       ← copy any user-provided images/references here
    ├── scraped/           ← save any scraped website content here
    └── test-variants/
        └── v1/            ← (or vX if iterating)
    ```
    - Use lowercase-kebab-case for the project folder name (e.g., `acme-landing/`).
    - Always create all three subfolders, even if `inspiration/` and `scraped/` start empty.
    - If the user provided inspiration images, move/copy them into `<website-name>/inspiration/` now.
    - If the user provided a URL to scrape, fetch and save relevant content (copy, layout notes, color palette) to `<website-name>/scraped/` before building.
    - Ask the user if this is a brand new project (`v1`) or an iteration (`v2`, `v3`, etc.).

3.  **Run UI/UX Pro Max Design System (REQUIRED)**
    Before writing any code, generate a design system recommendation using the installed skill:

    ```bash
    python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<project keywords>" --design-system -p "<Project Name>" --persist
    ```

    This produces a `design-system/<project-name>/MASTER.md` with the recommended style, color palette, typography, layout pattern, and anti-patterns. Read it before writing any code.

    If you need deeper guidance on a specific aspect, run domain searches:
    ```bash
    # Examples:
    python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<keywords>" --domain style
    python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<keywords>" --domain color
    python3 .claude/skills/ui-ux-pro-max/scripts/search.py "<keywords>" --domain ux
    ```

    Also read `.claude/skills/ui-ux-pro-max/SKILL.md` and apply the 10-priority rule table before generating code.

4.  **Generate Files**
    Write the code to the workspace in the created directory structure. Use pure HTML/CSS/JS or a modern framework based on the request. Apply all rules from the generated design system and SKILL.md — rich aesthetics, accessible, responsive, no emoji icons, proper transitions.

5.  **Serve Locally**
    Navigate into the `test-variants/vX` directory and use a local web server (like `npx serve`) to host the website on a localhost port. Test that it is running properly.
    // turbo

6.  **Notify User**
    Provide the localhost URL so the user can see the website. Ask for feedback to determine if deploying or iterating is required.
