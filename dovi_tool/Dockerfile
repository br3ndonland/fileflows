FROM alpine:edge
ARG DOVI_TOOL_VERSION=2.1.2
ARG DOVI_TOOL_ARCH=x86_64-unknown-linux-musl

LABEL org.opencontainers.image.description "This image provides a containerized version of the dovi_tool for use with Fileflows to convert Dolby Vision profile 7 to profile 8."

RUN apk add --no-cache --upgrade jq mediainfo mkvtoolnix
ADD https://github.com/quietvoid/dovi_tool/releases/download/${DOVI_TOOL_VERSION}/dovi_tool-${DOVI_TOOL_VERSION}-${DOVI_TOOL_ARCH}.tar.gz /tmp
RUN tar -xvf /tmp/dovi_tool-${DOVI_TOOL_VERSION}-${DOVI_TOOL_ARCH}.tar.gz -C /usr/local/bin
RUN mkdir /opt/media

COPY ./entrypoint.sh /usr/local/bin/entrypoint.sh
RUN chmod +x /usr/local/bin/entrypoint.sh

COPY ./dovi_tool.config.json /config/dovi_tool.config.json

RUN rm -rf /tmp/*

WORKDIR /opt/media

ENTRYPOINT ["entrypoint.sh"]
