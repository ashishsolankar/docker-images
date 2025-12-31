# Docker Images Collection

This repository contains a collection of Docker image definitions for various automation, build, and development scenarios. Each subdirectory is a self-contained Docker image project, following a standard structure.

## Standard Directory Structure
- `scripts/` – Helper scripts for build, test, or entrypoint
- `config/` – Configuration files or environment templates
- `README.md` – Documentation for the image
- `Dockerfile` – Complete Docker image definition

## Available Images

### Flutter (`flutter/`)
Optimized Flutter image for running unit tests, code coverage, and CI/CD automation.

**Features:**
- Flutter 3.32.0 (stable channel)
- Pre-installed `junitreport` for test reporting
- `lcov` and `genhtml` for code coverage
- `openssh-client` for private repository access during `flutter pub get`
- Lightweight (~500MB) without Android SDK or Java

**Usage:**
```bash
# Pull from GitHub Container Registry
docker pull ghcr.io/ashishsolankar/docker-images/flutter:latest

# Or build locally
docker build -t flutter-image ./flutter

# Run with SSH key mounting for private repos
docker run --rm -it \
  -v ~/.ssh/id_ed25519:/tmp/id_ed25519:ro \
  -v ~/.ssh/known_hosts:/tmp/known_hosts:ro \
  flutter-image bash
```

For more details, see the [Flutter README](flutter/README.md).

## Adding New Images

When adding new images, follow the same directory structure:
1. Create a new directory for your image
2. Add `Dockerfile`, `README.md`, `scripts/`, and `config/` subdirectories
3. Update this main README with usage instructions
