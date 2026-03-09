---
description: How to deploy the current project to Netlify
---
# Deploy to Netlify Workflow

1.  **Preparation**
    Ensure the website locally in `test-variants/<version>` is fully built, functioning, and approved by the user for deployment. If you need to build the project, keep in mind this step will happen in the deployed directory.

2.  **Use the `netlify_deployer` skill**
    Invoke the `netlify_deployer` skill procedures. It will handle copying the contents from `test-variants/<version>` into `deployed-variants/<version>` to maintain an accurate deployment history.

3.  **Run the deployment command**
    Run the deployment via `npx -y netlify-cli deploy --prod --dir <directory_name>` FROM inside the `deployed-variants/<version>` directory.
    - Note that `<directory_name>` is typically `.` for static HTML, or `dist` / `.next` for frameworks.
    // turbo
    
4.  **Confirm the deployment URL**
    Once the command finishes, test the production URL and provide it to the user.
