From centos:centos7.6.1810
LABEL maintainer="takahiro.yamaki@example.com"

COPY google-cloud-sdk.repo /etc/yum.repos.d/

WORKDIR /tmp

RUN set -x \
    && yum update  -y \
    && yum install -y google-cloud-sdk

# Terraform
RUN yum install -y wget unzip \
    && wget  https://releases.hashicorp.com/terraform/0.12.18/terraform_0.12.18_linux_amd64.zip \
    && unzip ./terraform_0.12.18_linux_amd64.zip -d /usr/local/bin/

# firebase-tools
RUN yum install -y which \
    && curl -sL https://rpm.nodesource.com/setup_12.x | bash - \
    && yum install -y nodejs \
    && npm update  -g npm \
    && npm install -g firebase-tools

# Version info
RUN gcloud -v \
    && terraform -v \
    && node -v \
    && npm  -v \
    && firebase -V
