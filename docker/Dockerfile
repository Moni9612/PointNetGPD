FROM ubuntu:jammy AS base

RUN apt-get update && \
    apt-get upgrade -y

RUN apt-get update && \
    apt-get install -y --no-install-recommends python3 \
                                               libpython3-dev \
                                               python3-pip 

RUN python3 -m pip install --no-cache-dir torch \ 
                                          torchvision \
                                          torchaudio \
                                          --index-url https://download.pytorch.org/whl/cu118

RUN rm -rf /var/lib/apt/lists/*

WORKDIR /home/code

ENV PointNetGPD_FOLDER=/home/code/PointNetGPD

RUN apt-get update && \
    apt-get install -y --no-install-recommends git \
                                               build-essential

RUN git clone https://github.com/Moni9612/PointNetGPD.git

WORKDIR /home/code/PointNetGPD

RUN python3 -m pip install --no-cache-dir -r requirements.txt

WORKDIR /home/code/PointNetGPD/meshpy

RUN python3 setup.py develop

WORKDIR /home/code/PointNetGPD/dex-net

RUN python3 setup.py develop
