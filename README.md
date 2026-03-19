# ComfyUI Workflows

A personal collection of ComfyUI workflows for AI video generation, upscaling, and video editing.
Each workflow entry includes a description, example output, requirements, and usage notes.

Drag-and-drop any `.json` file directly into ComfyUI to load the workflow.

---

## Posts

| Post | Date |
|---|---|

---

## WAN 2.2

| Workflow | Description | Type |
|---|---|---|
| [T2V A14B](wan/2.2/t2v-a14b/) | Text-to-video with the WAN 2.2 A14B model, GGUF quantized | Video gen |
| [Lightning GGUF](wan/2.2/lightning-gguf/) | Fast T2V with cached T5 encoding and Lightning-tuned steps | Video gen |
| [VACE](wan/2.2/vace/) | Video-to-video with automatic subject segmentation and depth conditioning | Video edit |
| [VACE Endless Extension](wan/2.2/vace-endless-extension/) | Extend a video indefinitely using VACE looping | Video gen |
| [Upscaling v1](wan/2.2/upscaling/) | Per-subject crop upscaling with VFI frame interpolation | Upscaling |

## HunyuanVideo

| Workflow | Description | Type |
|---|---|---|
| [RF-Inversion](hunyuanvideo/rf-inversion/) | Video editing via RF-inversion — relight, restyle, or modify existing video | Video edit |
