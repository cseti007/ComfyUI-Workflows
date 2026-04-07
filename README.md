# ComfyUI Workflows

**[!] This repository is no longer maintained. All new workflows and updates are published on HuggingFace:**
**https://huggingface.co/datasets/Cseti/ComfyUI-Workflows**

---

A personal collection of ComfyUI workflows for AI video generation, upscaling, and video editing.
Each workflow entry includes a description, example output, requirements, and usage notes.

Drag-and-drop any `.json` file directly into ComfyUI to load the workflow.

---

## Posts

| Post | Date |
|---|---|
| [MOMENTS — Making of](posts/2026-03-30-moments-short-film/) | 2026-03-30 |

---

## LTX Video 2.3

| Workflow                                          | Description                                                                      | Type      | Updated    |
| ------------------------------------------------- | -------------------------------------------------------------------------------- | --------- | ---------- |
| [I2V Two-Pass](ltx/2.3/i2v-two-pass/)            | Two-pass I2V with start/end guide images, 720p→1080p upscale, and audio support  | Video gen | 2026-03-30 |

## WAN 2.2

| Workflow                                                  | Description                                                               | Type       | Updated    |
| --------------------------------------------------------- | ------------------------------------------------------------------------- | ---------- | ---------- |
| [T2V A14B](wan/2.2/t2v-a14b/)                             | Text-to-video with the WAN 2.2 A14B model, GGUF quantized                 | Video gen  | 2025-07-30 |
| [Lightning GGUF](wan/2.2/lightning-gguf/)                 | Fast T2V with cached T5 encoding and Lightning-tuned steps                | Video gen  | 2025-08-09 |
| [VACE](wan/2.2/vace/)                                     | Video-to-video with automatic subject segmentation and depth conditioning | Video edit | 2025-07-15 |
| [VACE Endless Extension](wan/2.2/vace-endless-extension/) | Extend a video indefinitely using VACE looping                            | Video gen  | 2025-11-10 |
| [Upscaling v1](wan/2.2/upscaling/)                        | Per-subject crop upscaling with VFI frame interpolation                   | Upscaling  | 2025-10-13 |
| [Face Detailer](wan/2.2/face-detailer/)                   | SAM2-based segmentation and WAN 2.2 detail pass on existing video         | Video edit | 2026-03-29 |

## HunyuanVideo

| Workflow                                                    | Description                                                                  | Type       | Updated    |
| ----------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------- | ---------- |
| [RF-Inversion](hunyuanvideo/rf-inversion/)                  | Video editing via RF-inversion — relight, restyle, or modify existing video  | Video edit | 2025-01-23 |

## Z-Image

| Workflow                        | Description                                             | Type      | Updated    |
| ------------------------------- | ------------------------------------------------------- | --------- | ---------- |
| [Two-Stage](z-image/two-stage/) | Two-pass T2I workflow with refinement and color grading | Image gen | 2026-03-29 |
