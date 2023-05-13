FROM nvidia/cuda:11.8.0-runtime-ubuntu20.04
RUN apt-get update && apt-get install -y --no-install-recommends \
    software-properties-common libsm6 libxext6 ffmpeg libfontconfig1 libxrender1 libgl1-mesa-glx                                                                                                                        curl
WORKDIR /tmp
RUN wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh && sh Miniconda3-latest-Linux-x86_64.sh -b && rm Miniconda3-latest-Linux-x86_64.sh
COPY . /app
WORKDIR /app
RUN /root/miniconda3/bin/pip install \
    --no-dependencies \
    -r docker/requirements.txt \
    --index-url https://download.pytorch.org/whl/cu118 \
    --extra-index-url https://mirrors.ustc.edu.cn/pypi/web/simple

ENTRYPOINT ["/root/miniconda3/bin/python", "-c" ,"import webui;webui.webui()" ]
