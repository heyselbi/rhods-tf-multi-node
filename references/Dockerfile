FROM nvcr.io/nvidia/cuda:11.4.0-base-ubi8

MAINTAINER Selbi Nuryyeva <selbi@redhat.com>

ENV NCCL_VERSION 2.10.3

RUN yum install -y \
    cuda-libraries-11-4-11.4.0-1 \
    cuda-nvtx-11-4-11.4.43-1 \
    libcublas-11-4-11.5.2.43-1 \
    libcufft-11-4-10.5.0.43-1 \
    libcurand-11-4-10.2.5.43-1 \
    libcusolver-11-4-11.2.0.43-1 \
    libcusolver-devel-11-4-11.2.0.43-1 \
    libcusparse-11-4-11.6.0.43-1 \
    libcudnn8-8.2.2.*-1.cuda11.4 \
    libcudnn8-devel-8.2.2.*-1.cuda11.4 \
    libnccl-2.10.3-1+cuda11.4 \
    libnpp-11-4-11.4.0.33-1 \
    && yum clean all \
    && rm -rf /var/cache/yum/*

# TensorFlow version
ENV TF_VERSION=2.5.0

RUN yum -y install python3-devel \
                   python3-pip && \
    yum -y update && \
    yum clean all

# Install TensorFlow and TensorFlow GPU (since TensorFlow GPU is now combined with the original TensorFlow package)
RUN pip3 install --upgrade pip && \
    pip3 install tensorflow==${TF_VERSION}