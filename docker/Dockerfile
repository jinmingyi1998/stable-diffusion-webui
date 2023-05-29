FROM nvidia/cuda:11.8.0-runtime-ubuntu20.04
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
    wget curl git \
    software-properties-common libsm6 libxext6 ffmpeg libfontconfig1 libxrender1 libgl1-mesa-glx                                                                                                                  curl
WORKDIR /tmp
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh && sh Miniconda3-latest-Linux-x86_64.sh -b && rm Miniconda3-latest-Linux-x86_64.sh

WORKDIR /app
COPY docker/requirements.txt /app/docker/requirements.txt
RUN  --mount=type=cache,target=/root/.cache \
    /root/miniconda3/bin/pip install torch==2.0.0+cu118 torchvision pip setuptools cython wheel -U \
    --index-url https://download.pytorch.org/whl/cu118 \
    --extra-index-url https://mirrors.ustc.edu.cn/pypi/web/simple \
    && /root/miniconda3/bin/pip install \
    --no-dependencies -v \
    -r docker/requirements.txt \
    --index-url https://download.pytorch.org/whl/cu118 \
    --extra-index-url https://mirrors.ustc.edu.cn/pypi/web/simple
COPY configs/ configs/
COPY extensions-builtin/ extensions-builtin/
COPY html/ html/
COPY javascript/ javascript/ 
COPY modules/ modules/ 
COPY repositories/ repositories/ 
COPY scripts/ scripts/ 
COPY test/ test/ 
COPY textual_inversion_templates/ textual_inversion_templates/ 
COPY docker/launch.py launch.py 
COPY package.json package.json 
COPY script.js script.js 
COPY style.css style.css 
COPY webui.py webui.py 
ENTRYPOINT ["/root/miniconda3/bin/python", "launch.py"]

CMD ["--listen","--skip-prepare-environment"]
