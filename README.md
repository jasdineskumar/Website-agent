# Website Builder Agent Workspace

This repository serves as an automated environment for an AI agent to build, test, and deploy modern, aesthetically rich websites. It contains specialized sub-agents (skills) and workflows to ensure high-quality web generation and organized continuous deployment to Netlify.

## Workspace Architecture

To keep the environment clean and trackable, all websites follow a strict directory-based variant architecture:

```text
website-builder/
  ├── .agents/                    # Core AI Sub-Agent logic and workflows
  │   ├── skills/
  │   │   ├── website_builder/    # Logic for generating rich web projects locally
  │   │   └── netlify_deployer/   # Logic for deploying projects to production
  │   └── workflows/              # Defined slash commands (/create_website, /deploy_netlify)
  ├── package.json                # Local workspace tooling
  └── [your-website-name]/        # Each website gets its own directory
      ├── test-variants/
      │   └── v1/                 # Sandboxed development environments
      └── deployed-variants/
          └── v1/                 # Pristine snapshots of production code
```

## Available Agent Workflows

- **`/create_website`**: The AI will ask a series of questions (purpose, target audience, aesthetics, UI inspiration) and build a modern, interactive website into a new `test-variants` sandbox.
- **`/deploy_netlify`**: The AI will snapshot an approved test variant into the `deployed-variants` folder and automatically publish it to the live web via Netlify CLI.

## Best Practices
- Never develop directly in the root or `deployed-variants` directories.
- Provide descriptive inspiration URLs and tone requirements to the `website_builder` for the best generative results.
