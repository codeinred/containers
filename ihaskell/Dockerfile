#!./docker-build -t codeinred/ihaskell:v1.0
FROM ubuntu:20.04
LABEL author "Alecto Irene Perez"

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get -y update && apt-get -y upgrade
RUN  apt-get -y install     \
    python3-pip             \
    git                     \
    libtinfo-dev            \
    libzmq3-dev             \
    libcairo2-dev           \
    libpango1.0-dev         \
    libmagic-dev            \
    libblas-dev             \
    liblapack-dev

ENV PATH="$PATH:/root/.local/bin/"
RUN apt-get -y install haskell-stack && stack upgrade --binary-only

RUN git clone https://github.com/gibiansky/IHaskell     \
        && cd IHaskell                                  \
        && pip3 install -r requirements.txt             \
        && stack install --fast                         \
        && ihaskell install --stack

# Make directory for jupyter notebooks
RUN mkdir -p /notebooks && mkdir -p /root/.jupyter

WORKDIR /notebooks

EXPOSE 8888
# Run jupyter
CMD ["stack", "exec", "jupyter", "--", "notebook", "--ip=0.0.0.0", "--allow-root"]

