FROM alpine:3.11 AS build

ARG PACKER_VERSION
ARG PACKER_VERSION_SHA256SUM

COPY packer_${PACKER_VERSION}_linux_amd64.zip .
RUN echo "${PACKER_VERSION_SHA256SUM}  packer_${PACKER_VERSION}_linux_amd64.zip" > checksum && sha256sum -c checksum

RUN /usr/bin/unzip packer_${PACKER_VERSION}_linux_amd64.zip


FROM ubuntu
RUN apt-get -y update && apt-get -y install openssh-client ca-certificates python3-pip libpq-dev && rm -rf /var/lib/apt/lists/*
RUN pip3 install ansible psycopg2
COPY --from=build packer /usr/bin/packer
ENTRYPOINT ["/usr/bin/packer"]
