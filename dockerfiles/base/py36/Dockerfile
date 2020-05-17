ARG PYTHON_VER=3.6

FROM python:${PYTHON_VER}-slim-buster

ENV PYTHON_VER=$PYTHON_VER

LABEL maintainer="yashab@iguazio.com"
LABEL org="iguazio.com"

ARG REPO=mlrun

ARG MLRUN_TAG=development
ENV MLRUN_TAG=${MLRUN_TAG}

RUN apt update -qqq \
    && apt -y upgrade \
    && apt install -y \
    git \
    curl \
    build-essential \
    cmake \
    ca-certificates \
    && update-ca-certificates --fresh \
    && apt clean \
    && apt autoremove \
    && rm -rf /var/lib/apt/lists/*

ENV SSL_CERT_DIR /etc/ssl/certs

RUN python -m pip install git+https://github.com/${REPO}/mlrun.git@${MLRUN_TAG}

RUN python -m pip install urllib3==1.25.8  kubernetes==10.0.1

RUN python -m pip install scikit-learn

RUN python -m pip install \
        dask-kubernetes dask-ml \
        dask-xgboost \
        dask[complete] \
        distributed

RUN python -m pip install --no-cache-dir \
        blosc==1.7.0 \
        cloudpickle==1.1.1 \
        dask==2.12.0 \
        distributed==2.14.0 \
        lz4==2.2.1 \
        msgpack==1.0.0 \
        tornado==6.0.4 \
        numpy==1.18.1