FROM ubuntu:26.04 AS build

WORKDIR /root

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        build-essential bison flex libfl-dev libpng-dev libicu-dev git ca-certificates && \
    rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/MtnViewJohn/context-free.git && \
    cd context-free && \
    make && \
    cp cfdg /usr/local/bin/cfdg

FROM ubuntu:26.04

# Runtime shared libs linked by cfdg (see `ldd /usr/local/bin/cfdg` in the build stage):
# libpng16, libicu, libstdc++/libgcc, zlib. No build toolchain or source tree here.
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        libpng16-16t64 libicu78 libstdc++6 libgcc-s1 zlib1g && \
    rm -rf /var/lib/apt/lists/*

COPY --from=build /usr/local/bin/cfdg /usr/local/bin/cfdg

WORKDIR /mnt

ENTRYPOINT ["/usr/local/bin/cfdg"]
