# syntax=docker/dockerfile:1

FROM mambaorg/micromamba:latest AS build

RUN --mount=type=cache,target=/var/cache/conda \
    micromamba install -n base -c conda-forge -c nvidia -y \
    cudatoolkit=11.6 \
    jupyterlab \
    matplotlib \
    numpy \
    python>=3.10 \
    pip \
    scipy \
    && micromamba clean -ya

RUN /opt/conda/bin/python -m pip install --no-cache-dir --upgrade pip \
    && /opt/conda/bin/python -m pip install --no-cache-dir \
    jax[cuda]>=11.3 -f https://storage.googleapis.com/jax-releases/jax_releases.html

FROM nvcr.io/nvidia/cuda:11.6.2-devel-ubuntu20.04 AS lib

FROM debian:bullseye-slim

COPY --from=build /opt/conda /opt/conda
COPY --from=lib /usr/local/cuda/bin/ptxas /usr/bin/ptxas

ENV PATH=/opt/conda/bin:$PATH
