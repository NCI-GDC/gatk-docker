 FROM quay.io/ncigdc/bio-ubuntu:20.04 AS builder

MAINTAINER Charles Czysz <czysz@uchicago.edu>

ENV VERSION=4.2.4.1

ADD https://github.com/broadinstitute/gatk/releases/download/${VERSION}/gatk-${VERSION}.zip gatk-${VERSION}.zip

RUN apt-get update \
	&& apt-get install -y \
		build-essential \
		openjdk-8-jre-headless \
		r-base \
		unzip \
		wget \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*

RUN unzip gatk-${VERSION}.zip \
	&& mv gatk-${VERSION}/* /usr/local/bin/ \
	&& rm -rf gatk-* \
	&& ln -s /usr/local/bin/gatk-package-${VERSION}-local.jar /usr/local/bin/gatk.jar \
	&& apt-get purge -y \
		build-essential \
		unzip \
		wget \
	&& ls -l /usr/local/bin
