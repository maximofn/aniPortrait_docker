FROM nvcr.io/nvidia/cuda:11.8.0-cudnn8-devel-ubuntu22.04

RUN apt-get update \
    && apt-get install -y git git-lfs python3 python3-pip \
    && apt-get install -y libgl1-mesa-glx libglib2.0-0 \
    && curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | bash \
    && git lfs install \
    && rm cuda-keyring_1.0-1_all.deb \
    && ln -s /usr/bin/python3 /usr/bin/python \
    && rm -rf /var/lib/apt/lists/*

RUN apt-get update \
    && apt-get install -y --no-install-recommends wget ffmpeg \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install --no-cache-dir torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118 \
    && git clone --depth 1 https://github.com/Zejun-Yang/AniPortrait.git \
    && cd AniPortrait && pip3 install --no-cache-dir -r requirements.txt
    # && pip3 install --no-cache-dir gradio==3.23.0

RUN cd AniPortrait \
    && wget -q https://huggingface.co/ZJYang/AniPortrait/resolve/main/denoising_unet.pth -P /AniPortrait/pretrained_model \
    && wget -q https://huggingface.co/ZJYang/AniPortrait/resolve/main/reference_unet.pth -P /AniPortrait/pretrained_model \
    && wget -q https://huggingface.co/ZJYang/AniPortrait/resolve/main/pose_guider.pth -P /AniPortrait/pretrained_model \
    && wget -q https://huggingface.co/ZJYang/AniPortrait/resolve/main/motion_module.pth -P /AniPortrait/pretrained_model \
    && wget -q https://huggingface.co/ZJYang/AniPortrait/resolve/main/audio2mesh.pt -P /AniPortrait/pretrained_model \
    && wget -q https://huggingface.co/ZJYang/AniPortrait/resolve/main/audio2pose.pt -P /AniPortrait/pretrained_model \
    && wget -q https://huggingface.co/ZJYang/AniPortrait/resolve/main/film_net_fp16.pt -P /AniPortrait/pretrained_model

RUN cd AniPortrait \
    && mkdir stable-diffusion-v1-5 && mkdir stable-diffusion-v1-5/feature_extractor && mkdir stable-diffusion-v1-5/unet \
    && wget -q https://huggingface.co/runwayml/stable-diffusion-v1-5/raw/main/feature_extractor/preprocessor_config.json -P /AniPortrait/pretrained_model/stable-diffusion-v1-5/feature_extractor \
    && wget -q https://huggingface.co/runwayml/stable-diffusion-v1-5/raw/main/model_index.json -P /AniPortrait/pretrained_model/stable-diffusion-v1-5 \
    && wget -q https://huggingface.co/runwayml/stable-diffusion-v1-5/raw/main/unet/config.json -P /AniPortrait/pretrained_model/stable-diffusion-v1-5/unet \
    && wget -q https://huggingface.co/runwayml/stable-diffusion-v1-5/resolve/main/unet/diffusion_pytorch_model.bin -P /AniPortrait/pretrained_model/stable-diffusion-v1-5/unet \
    && wget -q https://huggingface.co/runwayml/stable-diffusion-v1-5/raw/main/v1-inference.yaml -P /AniPortrait/pretrained_model/stable-diffusion-v1-5

RUN cd AniPortrait \
    && mkdir sd-vae-ft-mse \
    && wget -q https://huggingface.co/stabilityai/sd-vae-ft-mse/raw/main/config.json -P /AniPortrait/pretrained_model/sd-vae-ft-mse \
    && wget -q https://huggingface.co/stabilityai/sd-vae-ft-mse/resolve/main/diffusion_pytorch_model.bin -P /AniPortrait/pretrained_model/sd-vae-ft-mse \
    && wget -q https://huggingface.co/stabilityai/sd-vae-ft-mse/resolve/main/diffusion_pytorch_model.safetensors -P /AniPortrait/pretrained_model/sd-vae-ft-mse

RUN cd AniPortrait \
    && mkdir image_encoder \
    && wget -q https://huggingface.co/lambdalabs/sd-image-variations-diffusers/raw/main/image_encoder/config.json -P /AniPortrait/pretrained_model/image_encoder \
    && wget -q https://huggingface.co/lambdalabs/sd-image-variations-diffusers/resolve/main/image_encoder/pytorch_model.bin -P /AniPortrait/pretrained_model/image_encoder

RUN cd AniPortrait \
    && mkdir wav2vec2-base-960h \
    && wget -q https://huggingface.co/facebook/wav2vec2-base-960h/raw/main/config.json -P /AniPortrait/pretrained_model/wav2vec2-base-960h \
    && wget -q https://huggingface.co/facebook/wav2vec2-base-960h/raw/main/feature_extractor_config.json -P /AniPortrait/pretrained_model/wav2vec2-base-960h \
    && wget -q https://huggingface.co/facebook/wav2vec2-base-960h/raw/main/preprocessor_config.json -P /AniPortrait/pretrained_model/wav2vec2-base-960h \
    && wget -q https://huggingface.co/facebook/wav2vec2-base-960h/resolve/main/pytorch_model.bin -P /AniPortrait/pretrained_model/wav2vec2-base-960h \
    && wget -q https://huggingface.co/facebook/wav2vec2-base-960h/raw/main/README.md -P /AniPortrait/pretrained_model/wav2vec2-base-960h \
    && wget -q https://huggingface.co/facebook/wav2vec2-base-960h/raw/main/special_tokens_map.json -P /AniPortrait/pretrained_model/wav2vec2-base-960h \
    && wget -q https://huggingface.co/facebook/wav2vec2-base-960h/raw/main/tokenizer_config.json -P /AniPortrait/pretrained_model/wav2vec2-base-960h \
    && wget -q https://huggingface.co/facebook/wav2vec2-base-960h/raw/main/vocab.json -P /AniPortrait/pretrained_model/wav2vec2-base-960h

WORKDIR /AniPortrait