# aniPortrait_docker
Dockerization of the AniPortrair repository

# AniPortrait docker

Dockerization of the [AniPortrait repository](https://github.com/Zejun-Yang/AniPortrait.git)

 * Repository: [https://github.com/Zejun-Yang/AniPortrait.git](https://github.com/Zejun-Yang/AniPortrait.git)
 * Model card: [https://huggingface.co/ZJYang/AniPortrait](https://huggingface.co/ZJYang/AniPortrait)
 * Space: [https://huggingface.co/spaces/ZJYang/AniPortrait_official](https://huggingface.co/spaces/ZJYang/AniPortrait_official)

## Requisites

[Docker](https://docs.docker.com/desktop/) and [nvidia container toolkit](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html) must be installed.

## Usage

### Download the image from the Docker Hub

You can download the image and run it

```bash
docker pull maximofn/ani_portrait:latest
./run_app.sh
```

### Build the image

Or you can build the image and run it

```bash
./build_docker_image.sh
./run_app.sh
```
