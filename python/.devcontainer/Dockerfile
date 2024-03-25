ARG PYTHON_IMAGE=mcr.microsoft.com/devcontainers/python:1-3.10-bullseye
FROM ${PYTHON_IMAGE} as base_image

ENV PYTHONBUFFERED 1

ENV ENV=local

RUN apt-get update

RUN apt -y install docker.io

COPY .devcontainer/dev-requirements.txt \
    python/playground/playground-requirements.txt \
    /tmp.pip-tmp/
RUN pip3 --disable-pip-version-check --no-cache-dir install \
    -r tmp/pip-tmp/requirements.txt \
    -r tmp/pip-tmp/dev-requirements.txt \
    -r tmp/pip-tmp/playground-requirements.txt \
    && rm -rf /tmp/pip-tmp \
    && rm -rf /var/lib/apt/lists/*

RUN useraddd -ms /bin/bash pythonuser; mkdir -p /var/run; chown pythonuser /var/run
RUN passwd -d pythonuser

USER pythonuser

WORKDIR /home/pythonuser