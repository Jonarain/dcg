FROM nvidia/cuda:10.2-cudnn7-devel-ubuntu18.04
MAINTAINER Wendelin Boehmer (of the PyMARL original: Tabish Rashid)

# CUDA includes
ENV CUDA_PATH /usr/local/cuda
ENV CUDA_INCLUDE_PATH /usr/local/cuda/include
ENV CUDA_LIBRARY_PATH /usr/local/cuda/lib64

# Ubuntu Packages
RUN apt-get update -y && apt-get install software-properties-common -y && \
    add-apt-repository -y multiverse && apt-get update -y && apt-get upgrade -y && \
    apt-get install -y apt-utils nano vim man build-essential wget sudo && \
    rm -rf /var/lib/apt/lists/*

# Install curl and other dependencies
RUN apt-get update -y && apt-get install -y curl libssl-dev openssl libopenblas-dev \
    libhdf5-dev hdf5-helpers hdf5-tools libhdf5-serial-dev libprotobuf-dev protobuf-compiler git

# This line from PyMARL's original Dockerfile has to commented out to work with the Ubuntu 18.04 image
# RUN curl -sk https://raw.githubusercontent.com/torch/distro/master/install-deps | bash && \
#     rm -rf /var/lib/apt/lists/*

# Install python3 pip3
RUN apt-get update
RUN apt-get -y install python3.6.4
RUN apt-get -y install python3-pip
RUN pip3 install --upgrade pip

# Python packages we use (or used at one point...)
RUN pip3 install numpy==1.15.2 scipy==1.1.0 pyyaml==3.13 matplotlib==3.0.0
RUN pip3 install imageio
RUN pip3 install tensorboard-logger==0.1.0
RUN pip3 install pygame==1.9.4

RUN mkdir /install
WORKDIR /install

RUN pip3 install jsonpickle==0.9.6
# install Sacred (from OxWhirl fork)
RUN pip3 install setuptools
RUN git clone https://github.com/oxwhirl/sacred.git /install/sacred && cd /install/sacred && python3 setup.py install

#### -------------------------------------------------------------------
#### install pytorch
#### -------------------------------------------------------------------
RUN pip3 install torch==1.5.0
RUN pip3 install torchvision==0.2.1 snakeviz==1.0.0 pytest==3.8.2 probscale==0.2.3

### -- This library must be added for DCG, one may need to adapt it to newer torch versions
RUN pip3 install torch_scatter -f https://pytorch-geometric.com/whl/torch-1.5.0.html

### -- SMAC
RUN pip3 install git+https://github.com/oxwhirl/smac.git
ENV SC2PATH /pymarl/3rdparty/StarCraftII

WORKDIR /pymarl
