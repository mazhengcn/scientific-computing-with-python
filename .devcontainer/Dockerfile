ARG VENV_PATH=/opt/venv

FROM python:3.11-slim AS pip-installs
ARG VENV_PATH

RUN python -m venv ${VENV_PATH}
ENV PATH=${VENV_PATH}/bin:$PATH
RUN python -m pip install --upgrade --no-cache-dir pip \
    && python -m pip install --no-cache-dir \
    jupyterlab \
    matplotlib \
    numpy \
    pandas \
    scipy \
    seaborn

FROM python:3.11-slim
ARG VENV_PATH

COPY --from=pip-installs ${VENV_PATH} ${VENV_PATH}
ENV PATH=${VENV_PATH}/bin:$PATH