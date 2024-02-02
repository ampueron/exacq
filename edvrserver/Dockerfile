FROM ubuntu:22.04

ARG exacq_version=23.09.6.0
ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y wget

ARG edvrserver_dpkg=exacqVisionServer_${exacq_version}_x64.deb
RUN wget --quiet https://exacq.com/reseller/23.09/${edvrserver_dpkg}

# Don't need this any more
RUN apt-get purge -y wget
RUN apt-get update && apt-get install -y file ntp ntpdate net-tools smartmontools wodim kmod dmidecode
RUN dpkg -i ${edvrserver_dpkg} && rm -f ${edvrserver_dpkg}

# Slim down the image
RUN apt-get autoremove -y && apt-get clean -y

EXPOSE 22609
ENTRYPOINT ["/usr/local/exacq/server/exacqd"]