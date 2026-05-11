<div align="center">

# 🍽️ GlucoVision Food Recognition Service

**The computer vision engine that identifies food from patient photos.**  
*ResNet-50 · ViT-B16 · Sri Lankan food fine-tuning · ONNX inference · MLflow*

[![PyTorch](https://img.shields.io/badge/PyTorch-2.x-EE4C2C?style=for-the-badge&logo=pytorch)](#)
[![FastAPI](https://img.shields.io/badge/FastAPI-Python-009688?style=for-the-badge&logo=fastapi)](#)
[![ONNX](https://img.shields.io/badge/ONNX-Runtime-005CED?style=for-the-badge)](#)
[![CUDA](https://img.shields.io/badge/NVIDIA-CUDA-76B900?style=for-the-badge&logo=nvidia)](#)
[![Docker](https://img.shields.io/badge/Docker-GPU-2496ED?style=for-the-badge&logo=docker)](#)
[![Status](https://img.shields.io/badge/Status-In%20Development-f59e0b?style=for-the-badge)](#)

</div>

---

## 📌 Purpose

GlucoVision Food Recognition answers the question: *"What dish is this?"* It maps a patient's food photo to a food ID, unlocking the nutrition lookup needed for glucose prediction and personalised recommendations. Fine-tuned on a custom Sri Lankan food dataset collected by `02-data-collect-app`.

> **Research basis:** ResNet-50 (91% accuracy) and ViT-B16 (93% accuracy) from the systematic review, with domain adaptation for Sri Lankan cuisine.

---

## 📁 Project Structure

```
09-glucovision-food-recognition-service/
└── (Git repository initialised — structure to be scaffolded)
```

---

## ✨ Planned Features (by phase)

### Phase 1 — Base Classifier
- [ ] ResNet-50 pretrained on ImageNet → fine-tuned on Food-101
- [ ] FastAPI inference endpoint (image upload → food class + confidence)
- [ ] ONNX Runtime model serving

### Phase 2 — Sri Lankan Fine-tuning
- [ ] Domain adaptation on custom dataset from `02`
- [ ] ViT-B16 alternative model (93% accuracy)
- [ ] Ensemble (ResNet + ViT) for higher confidence
- [ ] Nutrition lookup: food_id → macronutrients + GI index

### Phase 3 — Multi-item & Monitoring
- [ ] YOLOv8 multi-item detection (multiple dishes per plate)
- [ ] MLflow model versioning and experiment tracking
- [ ] Model drift monitoring (MAPE via Prometheus)
- [ ] Federated learning integration → `20`

---

## 🚀 Getting Started

### Prerequisites

- Python ≥ 3.11, NVIDIA GPU (CUDA 12+), Docker & Docker Compose

### Setup (once scaffolded)

```bash
pip install -r requirements.txt
uvicorn main:app --reload --port 8004

# Or via Docker (GPU)
docker compose up --build
```

---

## 🏗️ Planned Tech Stack

| Layer | Technology |
|---|---|
| Framework | FastAPI (Python) |
| Deep Learning | PyTorch 2.x |
| Models | ResNet-50, ViT-B16 (torchvision / HuggingFace) |
| Inference | ONNX Runtime |
| Image Processing | Pillow, torchvision.transforms |
| Model Registry | MLflow |
| Storage | MinIO (model weights + images) |
| GPU | NVIDIA CUDA |
| Containerisation | Docker + NVIDIA Container Toolkit |

---

## 🔗 Backend Dependencies

| Service | Interaction |
|---|---|
| `02` data-collect-app | Training data (Sri Lankan food images) |
| `05` api-gateway | Request routing + auth |
| `10` portion-estimation | Receives bounding boxes for portion sizing |
| `15` recommendation-engine | Provides food_id for meal planning |
| `20` federated-learning | Receives aggregated model updates |
| MLflow | Model versioning and deployment |

---

## 🔐 Security Notes

- JWT validation via gateway
- Image validation: reject non-image files, 10MB size limit
- Model integrity: checksum verification on MLflow download
- Privacy: uploaded food images checked for face content

---

## 🧪 Testing (Planned)

```bash
pytest tests/model/         # Accuracy > 90% on test set
pytest tests/api/           # Endpoint upload → classification
pytest tests/latency/       # < 500ms inference target
```

---

<div align="center">

*Part of the [GlucoVision Platform](../01-glucovision-platform-architecture) — 21-Repo AI Diabetes Management System*

</div>
