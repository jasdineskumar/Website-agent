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
    After gathering the requirements, ensure the directory structure for `<website-name>/test-variants/vX` is set up properly where `X` is the current variant version.
    - Ask the user if this is a brand new project (`v1`) or an iteration (`v2`, `v3`, etc.).

3.  **Use the `website_builder` skill**
    Invoke the `website_builder` skill procedures to generate the code for layout, logic, and styling directly into the target `test-variant` directory. Be sure to reference any UI inspiration provided by the user.

4.  **Generate Files**
    Write the code to the workspace in the created directory structure. Use pure HTML/CSS/JS or a modern framework based on the request. Make sure to adhere to modern design rules and rich aesthetics.

5.  **Serve Locally**
    Navigate into the `test-variants/vX` directory and use a local web server (like `npx serve`) to host the website on a localhost port. Test that it is running properly.
    // turbo

6.  **Notify User**
    Provide the localhost URL so the user can see the website. Ask for feedback to determine if deploying or iterating is required.
