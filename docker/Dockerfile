FROM nvidia/cuda:11.8.0-runtime-ubuntu20.04
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    wget curl git \
    software-properties-common libsm6 libxext6 ffmpeg libfontconfig1 libxrender1 libgl1-mesa-glx                                                                                                                  curl
WORKDIR /tmp
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh && sh Miniconda3-latest-Linux-x86_64.sh -b && rm Miniconda3-latest-Linux-x86_64.sh
COPY . /app
WORKDIR /app
RUN  --mount=type=cache,target=/root/.cache \
    /root/miniconda3/bin/pip install torch==2.0.0+cu118 torchvision pip setuptools cython wheel -U --index-url https://download.pytorch.org/whl/cu118 \
    && /root/miniconda3/bin/pip install \
    --no-dependencies -v \
    -r docker/requirements.txt \
    --index-url https://download.pytorch.org/whl/cu118

ENTRYPOINT ["/root/miniconda3/bin/python", "-c","import webui;webui.webui()"]

CMD ["--listen"]
