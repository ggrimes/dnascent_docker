# Start from a base image
FROM ubuntu:16.04

# Set up environment
# RUN is used to run commands in the container
RUN apt-get update && apt-get install -y \
    build-essential \
    zlib1g-dev \
    libncurses5-dev \
    libbz2-dev \
    liblzma-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    wget \
    git

# Install specific gcc version
RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:ubuntu-toolchain-r/test -y
RUN apt-get update
RUN apt-get install -y gcc-9 g++-9
RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 60 --slave /usr/bin/g++ g++ /usr/bin/g++-9 

# Install samtools
RUN wget https://github.com/samtools/samtools/releases/download/1.13/samtools-1.13.tar.bz2
RUN tar -vxjf samtools-1.13.tar.bz2
RUN cd samtools-1.13 && ./configure --without-curses && make && make install

# Install minimap2
# minimap2 is a tool for fast pairwise alignment of genomic and spliced DNA sequences
RUN wget https://github.com/lh3/minimap2/releases/download/v2.20/minimap2-2.20_x64-linux.tar.bz2
RUN tar -vxjf minimap2-2.20_x64-linux.tar.bz2
RUN cp minimap2-2.20_x64-linux/minimap2 /usr/local/bin/

# Install DNAscent
RUN git clone --recursive https://github.com/MBoemo/DNAscent.git
RUN cd DNAscent && git checkout 3.1.2 && make

# building on my mac
# docker buildx build --platform linux/x86_64 -t ggrimes/dnascent:3.1.2 .   

## upload to my dockerhub
# docker push ggrimes/dnascent:3.1.2

# To convert this to a singularity image, run:
# singularity build dnascent_3.1.2.sif docker-daemon://ggrimes/dnascent:3.1.2