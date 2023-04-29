# Use an official Ubuntu 18.04 LTS as a base image
FROM ubuntu:18.04

# Install required packages for Honeyd and SCADA honeynet
RUN apt-get update \
    && apt-get install -y make \
    && apt-get install -y supervisor \
    && apt-get install -y net-tools \
    && apt-get install -y apt-utils \
    && apt-get install -y vim \
    && apt-get install -y git \
    && apt-get install -y libevent-dev libdumbnet-dev libpcap-dev libpcre3-dev libedit-dev bison flex libtool automake zlibc zlib1g zlib1g-dev \
    && apt-get install -y terminator

# Set the working directory to /scada_honeynet
WORKDIR /scada_honeynet

# Copy the Honeyd folder and its contents to /scada_honeynet/Honeyd
RUN git clone https://github.com/DataSoft/Honeyd.git

# Install Honeyd from source
WORKDIR /scada_honeynet/Honeyd
RUN ./autogen.sh && \
    ./configure && \
    make && \
    make install

# Copy the SCADA honeynet configuration files
WORKDIR /scada_honeynet
COPY winxp.conf scada.conf ./

# Start Honeyd with the SCADA honeynet configuration
CMD ["honeyd", "-d", "-f", "scada.conf"]

