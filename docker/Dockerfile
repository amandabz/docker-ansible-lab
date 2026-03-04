FROM ubuntu:22.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt update && \
    apt install -y sudo && \
    apt install -y python3 openssh-server sudo && \
    apt clean

CMD ["sleep", "infinity"]
