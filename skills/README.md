# Web skills

This directory is published to the public `qzq00767/octopus-skills` repository
at `skills/` and excluded from deployment images.
Skill documents are original MIT-licensed instructions. They are not copies of the linked upstream projects.

`catalog.json` contains the public directory. Publish documents first, then update their catalog version and SHA-256 checksum to offer explicit client updates. Checksums use the exact UTF-8 document bytes. Existing installed copies remain unchanged until the user updates them. Set `NEXT_PUBLIC_SKILL_CATALOG_URL` at build time to use another GitHub raw catalog.

Supported kinds: `prompt`, `image-style`, `web`, `papers`. Documents are plain instructions only; scripts, arbitrary tools, local filesystem access and arbitrary network endpoints are never executed.

Web search requires an administrator-configured SearXNG service. Paper search uses Crossref metadata, not full-text papers. Queries are sent to the selected retrieval service; downloaded skills remain in the browser.

For development only, `/api/skills/preview/...` serves this local directory so unpublished changes can be tested. This route returns 404 in production. Publish this directory to the public skills repository before deploying the marketplace; production clients download directly from GitHub.

The four external repositories in the marketplace are client resources. Their tools, licenses and runtime requirements must be checked before use in a desktop client.
