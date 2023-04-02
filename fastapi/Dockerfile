FROM python:3.11-alpine3.17

ENV APP_DIR="/app"

# Application Build
ARG USER_NAME="fastapi"
ARG USER_ID="1000"
ARG GROUP_NAME="fastapi"
ARG GROUP_ID="1000"

# Uvicorn Defaults
ENV UVICORN_HOST="0.0.0.0"
ENV UVICORN_PORT="3000"
ENV UVICORN_WORKERS="5"
ENV UVICORN_LOG_LEVEL="error"

RUN apk add --no-cache bash

SHELL [ "/bin/bash", "-c" ]

RUN addgroup -g "${GROUP_ID}" "${GROUP_NAME}" && \
    adduser -s /bin/bash -h "${APP_DIR}" -G "${GROUP_NAME}" -u "${USER_ID}" -D "${USER_NAME}"

RUN pip3 install --upgrade pip virtualenv uvicorn

USER "${USER_NAME}"
WORKDIR "${APP_DIR}"

RUN mkdir -p src log tmp && \
    python3 -m venv env

COPY ./src/ src/
COPY ./requirements.txt .
COPY ./docker-entrypoint.sh .

RUN pip install -r requirements.txt

ENTRYPOINT ["/bin/bash", "./docker-entrypoint.sh"]