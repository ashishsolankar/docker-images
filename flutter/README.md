# Flutter Docker Image

Optimized Docker image for Flutter development, testing, and CI/CD automation. This image is lightweight (~500MB) and contains only the essential tools needed for Flutter unit testing and code coverage.

## Features
- **Flutter 3.32.0** (stable channel)
- **junitreport** - Pre-installed for test result reporting
- **lcov & genhtml** - For code coverage generation
- **SSH client** - For private repository access during `flutter pub get`
- **No Android SDK or Java** - Keeps image size minimal
- **Debian bullseye-slim** base for security and performance

## Quick Start

### Pull from GitHub Container Registry
```bash
docker pull ghcr.io/ashishsolankar/docker-images/flutter:latest
```

### Build Locally
```bash
docker build -t flutter-image .
```

### Run Container
```bash
# Basic usage
docker run --rm -it flutter-image bash

# With private repo access (mount SSH keys)
docker run --rm -it \
  -v ~/.ssh/id_ed25519:/tmp/id_ed25519:ro \
  -v ~/.ssh/known_hosts:/tmp/known_hosts:ro \
  flutter-image bash -c "
    mkdir -p /root/.ssh && \
    cp /tmp/id_ed25519 /root/.ssh/id_ed25519 && \
    cp /tmp/known_hosts /root/.ssh/known_hosts && \
    chmod 600 /root/.ssh/id_ed25519 && \
    chmod 644 /root/.ssh/known_hosts && \
    git clone git@github.com:your-org/your-repo.git && \
    cd your-repo && \
    bash"
```

## Common Use Cases

### Running Flutter Tests
```bash
# Inside container
flutter test

# With coverage
flutter test --coverage
genhtml coverage/lcov.info --output-directory=coverage/html
```

### Generating Test Reports
```bash
# Flutter tests with JUnit output
flutter test --machine > test-results.json
junitreport test-results.json --output TEST-report.xml
```

### Working with Private Dependencies
```bash
# The image includes SSH client for private repository access
# Ensure SSH keys are properly mounted and configured
flutter pub get  # Works with private git dependencies
```

## Directory Structure
- `Dockerfile` – Optimized Flutter image definition
- `scripts/` – Helper scripts (currently empty)
- `config/` – Configuration templates (currently empty)
- `README.md` – This documentation

## Image Details
- **Base**: debian:bullseye-slim
- **Size**: ~500MB (optimized)
- **Flutter Version**: 3.32.0 stable
- **Available Tools**: flutter, dart, lcov, genhtml, junitreport, git, curl, ssh

## Contributing
When making changes to this image:
1. Update the Dockerfile
2. Test the build: `docker build -t flutter-test .`
3. Update this README if adding new features
4. Tag and push to registry if approved
