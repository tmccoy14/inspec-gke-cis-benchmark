# Base Ruby image
FROM ruby:2.6

# Chef InSpec install arguments
ARG VERSION=4.37.20
ARG CHANNEL=stable

# Chef InSpec cannot execute without accepting the license
ENV CHEF_LICENSE accept-no-persist

# Install packages
RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y \
    curl \
    gcc \
    g++ \
    make \
    build-essential \
    git \
    wget \
    rpm2cpio \
    cpio

# Install Chef InSpec
RUN wget "http://packages.chef.io/files/${CHANNEL}/inspec/${VERSION}/el/7/inspec-${VERSION}-1.el7.x86_64.rpm" -O /tmp/inspec.rpm
RUN rpm2cpio /tmp/inspec.rpm | cpio -idmv
RUN rm -rf /tmp/inspec.rpm

# Install Gems
RUN gem install inspec-bin
RUN gem install train-kubernetes
RUN gem install bundler

# Install K8s plugin
RUN inspec plugin install train-kubernetes

# Set Chef InSpec entrypoint
ENTRYPOINT [ "inspec" ]
