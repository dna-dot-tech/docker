FROM ubuntu:latest
ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Asia/Dubai
ENV HOME /root
WORKDIR /root

RUN  apt update && \
     apt install -y git autoconf automake make gcc perl zlib1g-dev libbz2-dev liblzma-dev libcurl4-gnutls-dev libssl-dev libncurses5-dev bcftools

RUN git clone https://github.com/samtools/htslib.git && cd htslib && \
	git submodule update --init --recursive && \
	autoreconf -i  && ./configure --enable-plugins --enable-s3 --enable-gcs --enable-libcurl && \
	make && make install >> install.txt

RUN git clone https://github.com/samtools/samtools.git && cd samtools && \
	autoheader && autoconf -Wno-syntax &&  \
	./configure --enable-configure-htslib && \
	make && make install >> install.txt

RUN apt-get clean autoclean && apt-get autoremove --yes && \
	rm -rf /var/lib/{apt,dpkg,cache,log}/
