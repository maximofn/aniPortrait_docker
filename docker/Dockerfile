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
    && apt-get install -y --no-install-recommends wget \
    && rm -rf /var/lib/apt/lists/*

RUN pip3 install --no-cache-dir torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu118 \
    && git clone --depth 1 https://github.com/Zejun-Yang/AniPortrait.git \
    && cd AniPortrait && pip3 install --no-cache-dir -r requirements.txt
    # && pip3 install --no-cache-dir gradio==3.23.0

RUN cd AniPortrait \
    && wget https://huggingface.co/ZJYang/AniPortrait/blob/main/denoising_unet.pth -P /AniPortrait/pretrained_model \
    && wget https://huggingface.co/ZJYang/AniPortrait/blob/main/reference_unet.pth -P /AniPortrait/pretrained_model \
    && wget https://huggingface.co/ZJYang/AniPortrait/blob/main/pose_guider.pth -P /AniPortrait/pretrained_model \
    && wget https://huggingface.co/ZJYang/AniPortrait/blob/main/motion_module.pth -P /AniPortrait/pretrained_model \
    && wget https://huggingface.co/ZJYang/AniPortrait/blob/main/audio2mesh.pt -P /AniPortrait/pretrained_model \
    && wget https://huggingface.co/ZJYang/AniPortrait/blob/main/film_net_fp16.pt -P /AniPortrait/pretrained_model

RUN cd AniPortrait \
    && mkdir stable-diffusion-v1-5 && mkdir stable-diffusion-v1-5/feature_extractor && mkdir stable-diffusion-v1-5/unet \
    && wget https://huggingface.co/runwayml/stable-diffusion-v1-5/blob/main/feature_extractor/preprocessor_config.json -P /AniPortrait/pretrained_model/stable-diffusion-v1-5/feature_extractor \
    && wget https://huggingface.co/runwayml/stable-diffusion-v1-5/blob/main/model_index.json -P /AniPortrait/pretrained_model/stable-diffusion-v1-5 \
    && wget https://huggingface.co/runwayml/stable-diffusion-v1-5/blob/main/unet/config.json -P /AniPortrait/pretrained_model/stable-diffusion-v1-5/unet \
    && wget https://huggingface.co/runwayml/stable-diffusion-v1-5/blob/main/unet/diffusion_pytorch_model.bin -P /AniPortrait/pretrained_model/stable-diffusion-v1-5/unet \
    && wget https://huggingface.co/runwayml/stable-diffusion-v1-5/blob/main/v1-inference.yaml -P /AniPortrait/pretrained_model/stable-diffusion-v1-5

RUN cd AniPortrait \
    && mkdir sd-vae-ft-mse \
    && wget https://huggingface.co/stabilityai/sd-vae-ft-mse/blob/main/config.json -P /AniPortrait/pretrained_model/sd-vae-ft-mse \
    && wget https://huggingface.co/stabilityai/sd-vae-ft-mse/blob/main/diffusion_pytorch_model.bin -P /AniPortrait/pretrained_model/sd-vae-ft-mse \
    && wget https://huggingface.co/stabilityai/sd-vae-ft-mse/blob/main/diffusion_pytorch_model.safetensors -P /AniPortrait/pretrained_model/sd-vae-ft-mse

RUN cd AniPortrait \
    && mkdir image_encoder \
    && wget https://huggingface.co/lambdalabs/sd-image-variations-diffusers/blob/main/image_encoder/config.json -P /AniPortrait/pretrained_model/image_encoder \
    && wget https://huggingface.co/lambdalabs/sd-image-variations-diffusers/blob/main/image_encoder/pytorch_model.bin -P /AniPortrait/pretrained_model/image_encoder

RUN cd AniPortrait \
    && mkdir wav2vec2-base-960h \
    && wget https://huggingface.co/facebook/wav2vec2-base-960h/blob/main/config.json -P /AniPortrait/pretrained_model/wav2vec2-base-960h \
    && wget https://huggingface.co/facebook/wav2vec2-base-960h/blob/main/feature_extractor_config.json -P /AniPortrait/pretrained_model/wav2vec2-base-960h \
    && wget https://huggingface.co/facebook/wav2vec2-base-960h/blob/main/preprocessor_config.json -P /AniPortrait/pretrained_model/wav2vec2-base-960h \
    && wget https://huggingface.co/facebook/wav2vec2-base-960h/blob/main/pytorch_model.bin -P /AniPortrait/pretrained_model/wav2vec2-base-960h \
    && wget https://huggingface.co/facebook/wav2vec2-base-960h/blob/main/README.md -P /AniPortrait/pretrained_model/wav2vec2-base-960h \
    && wget https://huggingface.co/facebook/wav2vec2-base-960h/blob/main/special_tokens_map.json -P /AniPortrait/pretrained_model/wav2vec2-base-960h \
    && wget https://huggingface.co/facebook/wav2vec2-base-960h/blob/main/tokenizer_config.json -P /AniPortrait/pretrained_model/wav2vec2-base-960h \
    && wget https://huggingface.co/facebook/wav2vec2-base-960h/blob/main/vocab.json -P /AniPortrait/pretrained_model/wav2vec2-base-960h

WORKDIR /AniPortrait