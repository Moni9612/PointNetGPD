FROM ubuntu:focal AS base

RUN apt-get update && \
    apt-get upgrade -y

RUN apt-get update && \
    apt-get install -y --no-install-recommends python3 \
                                               libpython3-dev \
                                               python3-pip \
                                               libx11-6 \
                                               libgl1 \
                                               git \
                                               build-essential

RUN python3 -m pip install --no-cache-dir networkx==3.1

RUN python3 -m pip install --no-cache-dir torch==2.4.1 \
                                          torchvision==0.19.1 \
                                          torchaudio==2.4.1 \
                                          --index-url https://download.pytorch.org/whl/cu121

RUN rm -rf /var/lib/apt/lists/*

WORKDIR /home/code

ENV PointNetGPD_FOLDER=/home/code/PointNetGPD

RUN git clone https://github.com/Moni9612/PointNetGPD.git

WORKDIR /home/code/PointNetGPD

RUN python3 -m pip install --no-cache-dir -r requirements.txt

WORKDIR /home/code/PointNetGPD/meshpy

RUN python3 setup.py develop

WORKDIR /home/code/PointNetGPD/dex-net

RUN python3 setup.py develop

WORKDIR /home/code/PointNetGPD/PointNetGPD