FROM node:9.5.0-alpine@sha256:50ae5f22356c5a0b0c0ea76d27a453b0baf577c61633aee25cea93dcacec1630

USER root

RUN apk update && \
    apk upgrade && \
    apk add git && \
    apk add openssh

RUN mkdir ~/.ssh

WORKDIR /workspace/

