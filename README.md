# OpenCV on Debian [Bullseye stable]

## Images

In this repo you'll find:

- `ghcr.io/denismakogon/opencv-debian:4.5.5-build` as an OpenCV build environment
- `ghcr.io/denismakogon/opencv-debian:4.5.5-runtime` as an OpenCV runtime for applications from the build stage


### Build image

```shell
podman build -t ghcr.io/denismakogon/opencv-debian:4.5.5-build -f build/4.5.5/Dockerfile .
```

### Runtime image

```shell
podman build -t ghcr.io/denismakogon/opencv-debian:4.5.5-runtime -f runtime/Dockerfile \
  --build-arg "BUILD_IMAGE_DIGEST_TAG=ghcr.io/denismakogon/opencv-debian:4.5.5-build" \
  .
```
