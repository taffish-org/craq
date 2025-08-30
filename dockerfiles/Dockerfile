FROM ghcr.io/taffish-org/python:3.13.2

LABEL maintainer="taffish@163.com"

WORKDIR /root

RUN apt-get update && \
    apt-get install -y unzip bc perl curl git gcc g++ make zlib1g-dev bzip2 \
                       libncurses-dev liblzma-dev libbz2-dev libcurl4-gnutls-dev libcrypto++-dev libdeflate-dev && \
    cd / && \
    git clone --recursive https://github.com/samtools/htslib.git && \
    git clone --recursive https://github.com/samtools/samtools.git && \
    cd /samtools/ && make && make install && \
    cd / && \
    curl -LO https://github.com/lh3/minimap2/releases/download/v2.29/minimap2-2.29.tar.bz2 && \
    bzip2 -d /minimap2-2.29.tar.bz2 && \
    tar -xvf /minimap2-2.29.tar && rm /minimap2-2.29.tar && \
    cd /minimap2-2.29/ && \
    if [ "$(uname -m)" = "aarch64" ]; then make arm_neon=1 aarch64=1; else make; fi && \
    PATH=/minimap2-2.29:{$PATH} && \
    cd / && \
    pip install --upgrade pip && pip install python-circos requests && \
    cd / && \
    curl -LO https://github.com/JiaoLaboratory/CRAQ/releases/download/v1.0.9/CRAQ-v1.0.9.zip && \
    unzip /CRAQ-v1.0.9.zip && rm /CRAQ-v1.0.9.zip && cd /CRAQ-v1.0.9-alpha/ && \
    chmod +x /CRAQ-v1.0.9-alpha/bin/craq && \
    PATH=/CRAQ-v1.0.9-alpha/bin:{$PATH} && \
    cd /CRAQ-v1.0.9-alpha/Example/ && \
    rm -rf /CRAQ-v1.0.9-alpha/Example/Output && \
    bash run_example.sh
    
ENV PATH=/minimap2-2.29:{$PATH}
ENV PATH=/CRAQ-v1.0.9-alpha/bin:{$PATH}

ENV TAFFISH_ENV=TAFFISH
ENV TAFFISH_NAME=craq
