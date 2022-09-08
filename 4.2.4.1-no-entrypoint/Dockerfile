FROM quay.io/ncigdc/base-u20.04-builder:latest AS builder

MAINTAINER Charles Czysz <czysz@uchicago.edu>

ARG VERSION

ENV URL=https://github.com/broadinstitute/gatk/releases/download/${VERSION}/gatk-${VERSION}.zip

RUN apt-get update \
	&& apt-get install -y \
		build-essential \
		openjdk-8-jre-headless \
		r-base \
		unzip \
		wget \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*

RUN wget $URL \
	&& unzip gatk-${VERSION}.zip \
	&& mv gatk-${VERSION}/* /usr/local/bin/ \
	&& rm -rf gatk-* \
	&& ln -s /usr/local/bin/gatk-package-${VERSION}-local.jar /usr/local/bin/gatk.jar \
	&& apt-get purge -y \
		build-essential \
		unzip \
		wget \
	&& ls -l /usr/local/bin