# docker

A collection of Docker containers for development environments, ML/AI workloads, web services, and production infrastructure.

## n8n-compose

Production-ready [n8n](https://n8n.io) workflow automation platform with an integrated **Whisper transcription service** for recording and transcribing live meetings.

**Services:**
* **n8n** — Workflow automation engine with 5000+ built-in nodes
* **Whisper frontend** — React + TipTap web UI for real-time audio transcription
* **Whisper database** — PostgreSQL 15 for transcription storage
* **Tailscale** — Zero-config VPN with automatic HTTPS certificates
* **Traefik** — Reverse proxy with TLS termination

The whisper frontend can **record live meetings** using BlackHole and Audio MIDI Setup to create a multi-output device, so that audio can be recorded and heard at the same time. It supports multiple Whisper model sizes, 50+ languages, stereo channel selection, AI-powered review (grammar, rephrasing, summarization via Ollama), and Obsidian integration.

The whisper backend runs on the host (not in Docker) for GPU access. Two backend options:
| Backend | Hardware | Location |
|---------|----------|----------|
| MLX-Whisper | Apple Silicon (M1-M4) | `../python/mlx_whisper/` |
| CUDA-Whisper | NVIDIA GPU (RTX 3090/4090) | `../python/cuda_whisper/` |

See `n8n-compose/whisper-project/README.md` for full documentation.

## sftp_server

Production-ready SFTP server on Alpine Linux with SSH key authentication and a Python client library.

* OpenSSH-based with chroot jail and key-based auth
* Python client library (`sftp_client.py`) with context manager API
* CLI sample app for manual operations and performance testing
* Port 2222, mounts `../python/docling_server/content` as SFTP root

## ML/AI Containers (CUDA)

GPU-accelerated containers for machine learning, all based on NVIDIA CUDA 12.8 with cuDNN:

| Container | Description |
|-----------|-------------|
| **cuda-conda** | Base image with Miniconda, PyTorch and TensorFlow conda environments |
| **cuda-conda-dev** | Extends cuda-conda with devel image + pandas, scikit-learn, graphviz |
| **cuda-conda-pytorch** | PyTorch-focused variant with data science libraries |
| **cuda-conda-tensorflow** | TensorFlow-focused variant with data science libraries |
| **opencv** | OpenCV 4.4 + GStreamer + Darknet/YOLOv4 (GPU-compiled) |
| **gstreamer** | NVIDIA DeepStream 5.0 for GPU-accelerated video/stream processing |

## Utility Containers

| Container | Description |
|-----------|-------------|
| **mediawiki** | MediaWiki + MariaDB knowledge base (port 8080) |
| **ubuntu_dev** | ARM64 Ubuntu 20.04 with build tools and utilities |
| **chrome** | Containerized Google Chrome with X11 display forwarding |
| **firefox** | Containerized Firefox with X11 display forwarding |
