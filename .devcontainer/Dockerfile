FROM ghcr.io/astral-sh/uv:latest AS uv

FROM node:22-bookworm-slim AS node

FROM mcr.microsoft.com/devcontainers/python:1-3.13-bookworm

COPY --from=uv /uv /uvx /usr/local/bin/
COPY --from=node /usr/local/bin/node /usr/local/bin/node
COPY --from=node /usr/local/lib/node_modules /usr/local/lib/node_modules

RUN ln -sf /usr/local/lib/node_modules/npm/bin/npm-cli.js /usr/local/bin/npm \
    && ln -sf /usr/local/lib/node_modules/npm/bin/npx-cli.js /usr/local/bin/npx \
    && npm install --global @google/gemini-cli @openai/codex \
    && npm cache clean --force

ENV UV_LINK_MODE=copy \
    PYTHONUNBUFFERED=1
