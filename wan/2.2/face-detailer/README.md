# WAN 2.2 Face Detailer

**Model:** WAN 2.2 T2V A14B (fp8 scaled)
**Type:** Video-to-Video

Face enhancement pipeline for WAN 2.2 video output. Loads an existing video, detects and segments faces using SAM2, crops each face region, runs a focused WAN 2.2 generation pass to add detail, then composites the result back into the original frame.

---

## Preview

[![Preview — meeting scene](media/preview-meeting_thumb.png)](media/preview-meeting.mp4)

[![Preview — backward look scene](media/preview-backwardlook_thumb.png)](media/preview-backwardlook.mp4)

---

## Requirements

- **ComfyUI:** recent stable build

### Models

- **Main model:** `Wan2_2-T2V-A14B-LOW_fp8_e4m3fn_scaled_KJ.safetensors` —
  [Kijai/WanVideo_comfy_fp8_scaled](https://huggingface.co/Kijai/WanVideo_comfy_fp8_scaled/resolve/main/T2V/Wan2_2-T2V-A14B-LOW_fp8_e4m3fn_scaled_KJ.safetensors)

- **VACE module:** `Wan2_2_Fun_VACE_module_A14B_LOW_fp8_e4m3fn_scaled_KJ.safetensors` —
  [Kijai/WanVideo_comfy_fp8_scaled](https://huggingface.co/Kijai/WanVideo_comfy_fp8_scaled/resolve/main/VACE/Wan2_2_Fun_VACE_module_A14B_LOW_fp8_e4m3fn_scaled_KJ.safetensors)

- **VAE:** `Wan2_1_VAE_bf16.safetensors` —
  [Kijai/WanVideo_comfy](https://huggingface.co/Kijai/WanVideo_comfy/resolve/main/Wan2_1_VAE_bf16.safetensors)

- **Text encoder:** `umt5-xxl-enc-bf16.safetensors` —
  [Kijai/WanVideo_comfy](https://huggingface.co/Kijai/WanVideo_comfy/resolve/main/umt5-xxl-enc-bf16.safetensors)

- **LoRA (step distill):** `lightx2v_T2V_14B_cfg_step_distill_v2_lora_rank64_bf16.safetensors` —
  [Kijai/WanVideo_comfy](https://huggingface.co/Kijai/WanVideo_comfy/resolve/main/Lightx2v/lightx2v_T2V_14B_cfg_step_distill_v2_lora_rank64_bf16.safetensors)

- **LoRA (reward):** `Wan2.2-Fun-A14B-InP-low-noise-HPS2.1.safetensors` — example LoRA, replace with your own if needed —
  [alibaba-pai/Wan2.2-Fun-Reward-LoRAs](https://huggingface.co/alibaba-pai/Wan2.2-Fun-Reward-LoRAs/resolve/main/Wan2.2-Fun-A14B-InP-low-noise-HPS2.1.safetensors)

- **Segmentation:** `sam2.1_hiera_small.safetensors` —
  [Kijai/sam2-safetensors](https://huggingface.co/Kijai/sam2-safetensors/resolve/main/sam2.1_hiera_small.safetensors)

### Custom nodes

- [ComfyUI-WanVideoWrapper](https://github.com/kijai/ComfyUI-WanVideoWrapper)
- [ComfyUI-KJNodes](https://github.com/kijai/ComfyUI-KJNodes)
- [ComfyUI-VideoHelperSuite](https://github.com/Kosinkadink/ComfyUI-VideoHelperSuite)
- [ComfyUI-segment-anything-2](https://github.com/kijai/ComfyUI-segment-anything-2)
- [rgthree-comfy](https://github.com/rgthree/rgthree-comfy)
- [ComfyUI-Florence2](https://github.com/kijai/ComfyUI-Florence2) — delete these nodes if you don't want to use florence2 for segmentation.
---

## Notes

- The VACE module is optional — disconnect it to run without VACE.
- SAM2 is used for face segmentation. The face bounding box index can be adjusted directly in the workflow if the wrong face is selected.

---

## Changelog

- `2026-03-29` — Initial upload
