# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

A personal collection of ComfyUI workflows for AI video generation, video editing, upscaling, and image generation. Workflows are distributed as `.json` files that can be drag-and-dropped into ComfyUI. Each workflow lives in its own directory alongside a `README.md` and a `media/` folder with preview assets.

## Directory Structure

```
<model-family>/<version>/<workflow-name>/
    <workflow-name>.json    # The ComfyUI workflow
    README.md               # Description, requirements, notes, changelog
    media/                  # Preview images/videos (thumbnails, mp4s)

posts/<date-slug>/
    README.md               # Long-form making-of post
    media/                  # Supporting media

drafts/                     # Work-in-progress workflows (not published)
```

## Workflow Families

- **ltx/** — LTX Video 2.x workflows (image-to-video, two-pass, audio support)
- **wan/** — WAN 2.2 workflows (T2V, VACE, face detailing, upscaling, Lightning GGUF)
- **hunyuanvideo/** — HunyuanVideo workflows (RF-inversion video editing)
- **z-image/** — Image generation workflows (two-stage T2I with refinement)

## README Convention for Workflows

Each workflow README must follow this structure (keep sections in order, no extras):

1. `# Title` — model name, type (Image-to-Video / Video-to-Video / etc.)
2. One-paragraph description of what the workflow does
3. `## Preview` — YouTube embed or local media link
4. `## Requirements` — ComfyUI version, models with HuggingFace download links, custom nodes with GitHub links
5. `## Notes` — key parameters, sampler settings, VRAM tips, optional nodes
6. `## Changelog` — dated entries, newest first, format: `- \`YYYY-MM-DD\` — note`

**No emojis** anywhere in README files. Use plain text markers if needed.

## Adding a New Workflow

1. Create the directory: `<model-family>/<version>/<workflow-slug>/`
2. Export and place the `.json` from ComfyUI
3. Create `README.md` following the convention above
4. Create `media/` and add at minimum one preview thumbnail
5. Add a row to the top-level `README.md` table under the correct model section (keep `| Workflow | Description | Type | Updated |` column order)

## Updating the Main README

The root `README.md` is the index. It contains one table per model family. Column order is fixed: `Workflow | Description | Type | Updated`. The `Type` column uses these values: `Video gen`, `Video edit`, `Upscaling`, `Image gen`. New rows are always inserted at the **top** of the table (newest first).

## Posts

Long-form making-of articles go under `posts/<YYYY-MM-DD-slug>/README.md`. They are linked from the `## Posts` table in the root README. Posts reference workflows via relative paths (e.g. `../../ltx/2.3/i2v-two-pass/`).
