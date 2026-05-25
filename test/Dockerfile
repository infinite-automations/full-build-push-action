# checkov:skip=CKV_DOCKER_7:Test image, pinning not needed
# hadolint global ignore=DL3007
# trivy:ignore:DS001
FROM busybox:latest
HEALTHCHECK --interval=30s --timeout=3s CMD true
USER 1000