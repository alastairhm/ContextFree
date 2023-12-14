FROM ubuntu as builder

WORKDIR /root

RUN apt update && apt upgrade -y && \
    apt install build-essential bison flex libfl-dev libpng-dev libicu-dev git -y && \
    git clone https://github.com/MtnViewJohn/context-free.git && \
    cd context-free && \
    make && \
    cp cfdg /usr/local/bin/cfdg

WORKDIR /mnt

ENTRYPOINT ["/usr/local/bin/cfdg"]

