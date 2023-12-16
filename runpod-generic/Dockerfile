FROM runpod/pytorch:2.1.0-py3.10-cuda11.8.0-devel-ubuntu22.04

RUN apt-get update \
    && apt-get install -y vim rsync htop zsh
RUN pip install --upgrade pip \
    && pip install transformers datasets beir wandb lightning

