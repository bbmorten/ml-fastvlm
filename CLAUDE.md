# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

FastVLM is an efficient vision encoding implementation for Vision Language Models, featuring both Python inference scripts and an iOS/macOS app for on-device visual question answering. The project implements FastViTHD, a novel hybrid vision encoder designed to output fewer tokens and significantly reduce encoding time for high-resolution images.

## Repository Structure

- **Python VLM Implementation** (`/`): LLaVA-based training and inference code for FastVLM variants
- **iOS/macOS App** (`/app/`): Swift app demonstrating on-device FastVLM performance using MLX framework
- **Model Export** (`/model_export/`): Tools for exporting models to Apple Silicon format

## Common Development Commands

### Python Environment Setup
```bash
conda create -n fastvlm python=3.10
conda activate fastvlm
pip install -e .
```

### Download Pretrained Models
```bash
# Download all pretrained checkpoints (PyTorch format)
bash get_models.sh

# Download model for iOS app (Apple Silicon format)
chmod +x app/get_pretrained_mlx_model.sh
app/get_pretrained_mlx_model.sh --model 0.5b --dest app/FastVLM/model
```

### Run Python Inference
```bash
python predict.py --model-path /path/to/checkpoint-dir \
                  --image-file /path/to/image.png \
                  --prompt "Describe the image."
```

### Build iOS/macOS App
1. Ensure a model is downloaded to `app/FastVLM/model/`
2. Open `app/FastVLM.xcodeproj` in Xcode
3. Build and run (requires iOS 18.2+ or macOS 15.2+)

## Key Architecture Components

### Vision Encoding Pipeline
The FastVLM model combines:
- **FastViTHD Vision Encoder**: CoreML model (`fastvithd.mlpackage`) for efficient high-resolution image processing
- **Multimodal Projector**: Maps vision features to language model embedding space
- **Qwen2-based Language Model**: Processes merged vision-language embeddings

### iOS App Architecture
- **FastVLM.swift**: Core VLM model implementation using MLX framework
- **FastVLMProcessor**: Handles image preprocessing and prompt formatting
- **Vision.VisionModelCoreML**: Wrapper for CoreML vision encoder
- **Language.LanguageModel**: Qwen2 architecture implementation

### Model Variants
- **FastVLM-0.5B**: Optimized for mobile devices (stage2/stage3 checkpoints)
- **FastVLM-1.5B**: Balanced speed/accuracy (stage2/stage3 checkpoints)
- **FastVLM-7B**: Maximum accuracy (stage2/stage3 checkpoints)

## Development Notes

### Working with the iOS App
- Models must be in Apple Silicon format (use `model_export/` tools or pre-exported versions)
- The app uses SwiftUI for UI and MLX/CoreML for inference
- Camera integration available for real-time visual Q&A

### Python Development
- Based on LLaVA codebase for training/finetuning
- Uses transformers, torch, and custom FastViTHD implementation
- Supports MPS (Apple Silicon) acceleration when available