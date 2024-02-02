FROM ubuntu:22.04

ENV exacq_version=23.09.1.0

ARG log_level="info"
ARG DEBIAN_FRONTEND=noninteractive

# Temporarily install wget
RUN apt-get update && apt-get install -y wget apt-utils

# Download the software package from Exacq
ARG webservice_dpkg=exacqVisionWebService_${exacq_version}_x64.deb
RUN wget --quiet https://exacq.com/reseller/23.09/${webservice_dpkg}

# Don't need this any more
RUN apt-get purge -y wget

# Prerequisites for exacqVisionWebService
#RUN apt-get install -y libreadline5

# Set password with --build-arg EVWS_PW=<password>
ARG EVWS_PW=Admin256
RUN dpkg -i ${webservice_dpkg} && rm -f ${webservice_dpkg}

# Fix up location of config directory
ARG data_dir=/usr/local/exacq/webservice/data
RUN service webservice stop \
    && mv /etc/webservice $data_dir/webservice \
    && ln -s $data_dir/webservice /etc/webservice

# Slim down the image
RUN apt-get autoremove -y && apt-get clean -y

VOLUME ["/usr/local/exacq/webservice/data"]

EXPOSE 80 443
ENTRYPOINT ["/usr/local/exacq/webservice/bin/wfe"]
CMD ["--log", ${log_level}]