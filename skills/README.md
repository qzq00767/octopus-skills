# Web skills

This directory is published to the public `qzq00767/octopus-skills` repository
at `skills/` and excluded from deployment images.
Skill documents include original instructions and explicitly attributed browser
adaptations of MIT-licensed upstream skills. Adapted documents retain their source,
upstream revision, modification notice and full license inside YAML frontmatter.
The model receives the instructions after that metadata is removed.

`catalog.json` contains the public directory. Publish documents first, then update their catalog version and SHA-256 checksum to offer explicit client updates. Checksums use the exact UTF-8 document bytes. Existing installed copies remain unchanged until the user updates them. Set `NEXT_PUBLIC_SKILL_CATALOG_URL` at build time to use another GitHub raw catalog.

Supported kinds: `prompt`, `image-style`, `web`, `papers`. Documents are plain instructions only; scripts, arbitrary tools, local filesystem access and arbitrary network endpoints are never executed.

Web search requires an administrator-configured SearXNG service. Paper search uses Crossref metadata, not full-text papers. Queries are sent to the selected retrieval service; downloaded skills remain in the browser.

For development only, `/api/skills/preview/...` serves this local directory so unpublished changes can be tested. This route returns 404 in production. Publish this directory to the public skills repository before deploying the marketplace; production clients download directly from GitHub.

The four external repositories in the marketplace are client resources. Their tools, licenses and runtime requirements must be checked before use in a desktop client.

## Browser Adaptations

The first common-skills expansion adds eight prompt-only skills:

| Local ID | Upstream | Browser scope |
| --- | --- | --- |
| humanizer | blader/humanizer | Rewrite supplied prose faithfully |
| copywriting | coreyhaines31/marketingskills: copywriting | Draft from supplied product context |
| copy-editing | coreyhaines31/marketingskills: copy-editing | Edit supplied copy |
| brainstorming | obra/superpowers: brainstorming | Explore ideas within the conversation |
| code-review | obra/superpowers: requesting-code-review | Review supplied snippets or diffs |
| systematic-debugging | obra/superpowers: systematic-debugging | Explain diagnostic and repair steps |
| prompt-engineer | Jeffallan/claude-skills: prompt-engineer | Produce reusable prompt templates |
| sql-assistant | Jeffallan/claude-skills: sql-pro | Write and explain SQL without executing it |

These adaptations do not run commands, dispatch agents, inspect repositories,
connect to databases, or gain network access through their prompt text.
They do not promise tested accuracy or runtime behavior.

The expanded catalog uses `writing`, `coding`, and `productivity` categories.
Publish the local `catalog.json` as `skills/catalog-v2.json` in the public
repository. The updated app reads that versioned URL. Preserve the public
`skills/catalog.json` for existing clients, whose schema rejects new categories.
The development preview route maps `catalog-v2.json` to the local `catalog.json`.
Publish documents and the v2 catalog before deploying the updated app.

## Image Styles

Image adapters use the existing `image-style` request path. Their instructions
are appended to the outbound image prompt; attachments and the user's original
message are preserved. Explicit ratio, dimensions, resolution, background,
format and image count take precedence over style defaults.
These are generative interpretations, not deterministic photo compositing or
guarantees that source pixels remain unchanged. They do not execute upstream
scripts, paid integrations or client tools.

| Local ID | Upstream |
| --- | --- |
| gc-minimal-zine-poster | LiamGvchi/gc-minimal-zine-poster |
| photo-relic-editorial | wnby/photo-relic-editorial |
| pixel-style-poster | v92388375-gif/pixel-style-poster-skill |
| kimi-inspired-poster | Fannie0715/kimi-inspired-poster |
| qiaomu-mondo-poster | joeseesun/qiaomu-mondo-poster-design |
| heytea-doodle-poster | Hchen1218/heytea-style |
| dreamcore-collage-poster | AndrwewHan/dreamcore-collage-poster |
| watercolor-travel-card | GZ-L/photo-to-poster-skills |
| impasto-miniature-landscape | GZ-L/photo-to-poster-skills |
| surreal-pop-collage | 2998980-hue/surreal-pop-collage |
| vinyl-image-generator | liigoQi/vinyl-image-generator |
| taxue-halftone | taxueseek/taxue-halftone |
| photo-to-zine-postcard | Whiplashzeb/photo-to-zine-postcard |
| neil-quentin | Nealsun1993/neil-quentin |
| neil-night | Nealsun1993/neil-night-skill |
| photo-riso-poster | luckdvr/photo-riso-poster |
| photo-stamp-archive | Dlcccc71913/skill-make-photo-stamp-archive |
| photo-memory-archive | sbj61188-lab/compose-photo-memory-archive |
| editorial-print-studio | liuzihe849-png/ai-editorial-print-studio |
| silhouette-group-collage | liuzihe849-png/silhouette-group-collage |

Each document pins the verified upstream revision and retains its MIT notice.
The existing `photo-revival` is not duplicated. `heytea-creative-style` exposes
the same `heytea-style` skill and is represented by `heytea-doodle-poster`.
The screenshot spelling `Lmnastapeiniature-Landscape` is interpreted as
`impasto-miniature-landscape`, found alongside `watercolor-travel-card`.

Not redistributed: `photo-abstract-editorial` (CC BY-NC-SA), gathered/distillation
zine skills and `scene-to-art-lab` (personal noncommercial),
`antibes-holiday` and `sunwoven-reverie` (PolyForm Noncommercial),
current `Punk-Skill` (personal-use restrictions), and `travel-photo-abstraction`
(custom restrictions on adaptation and redistribution). A fork's MIT label
does not supersede the original author's restrictions.

Hold skills without clear redistribution permission, including the checked
CRT interface, photo-distill, photo-deconstruct and soft-abstraction sources.
The eachlabs collection requires its own service and credentials, so it is
not included as a prompt-only image style.

Also held: `travel-memory-card-duo` (personal noncommercial restrictions),
`photo-ink-echo` (partly derived from restricted photo-abstract-editorial),
and ambiguous `Aigc-Skills` collections. `8bit-pixel-art` and the identified
`ink-wash-poster` are AGPL-3.0; this expansion only includes permissive MIT
adapters and does not imply those projects are unlicensed or unusable.
The checked paper-spirit, daily-photo, minimal-magazine, material-art and
eastern-ink sources do not provide clear redistribution permission.

## Style Previews

Optional `preview` metadata contains up to four immutable GitHub raw image URLs,
captions, asset credit, asset license and its source notice. Asset permissions
are checked separately from the skill's software license. For example,
heytea-style examples use CC BY 4.0; its private reference cutouts are excluded.
Taxue visual examples explicitly reserve rights and are not embedded.

The marketplace loads original examples directly in the browser, with lazy
loading, no referrer and fixed thumbnail dimensions. It does not proxy images
through the app server or embed them in model instructions. Images without
verified previews retain the text listing. The enlarged view shows complete
images, individual captions, provenance and the asset license. Network failures
show a stable fallback without blocking skill enablement.
