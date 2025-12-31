# syntax=docker/dockerfile:1

FROM debian:bullseye-slim

ENV DEBIAN_FRONTEND=noninteractive \
    LANG=C.UTF-8 \
    FLUTTER_CHANNEL=stable \
    FLUTTER_VERSION=3.32.0

# Install only required dependencies (no Java)
RUN apt-get update && apt-get install -y --no-install-recommends \
    curl git unzip xz-utils zip libglu1-mesa ca-certificates lcov openssh-client \
    && rm -rf /var/lib/apt/lists/*

# Install Flutter (only the required version)
RUN git clone --branch $FLUTTER_VERSION --depth 1 https://github.com/flutter/flutter.git /opt/flutter \
    && /opt/flutter/bin/flutter --version \
    && /opt/flutter/bin/flutter doctor -v \
    && /opt/flutter/bin/flutter pub global activate junitreport \
    && rm -rf /opt/flutter/bin/cache/artifacts/engine

ENV PATH="/opt/flutter/bin:/opt/flutter/bin/cache/dart-sdk/bin:${PATH}"

WORKDIR /workspace

CMD ["bash"]
