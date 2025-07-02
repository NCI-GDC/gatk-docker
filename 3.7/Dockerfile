ARG REPOSITORY=docker.osdc.io
ARG BUILDER_TAG=3.1.0

FROM ${REPOSITORY}/ncigdc/amzn2023-builder:${BUILDER_TAG} AS builder

MAINTAINER Charles Czysz <czysz@uchicago.edu>

LABEL version="nightly-2016-02-25-gf39d340"
LABEL description="GATK3 nightly-2016-02-25-gf39d340"

RUN dnf update -y \
    && dnf install -y java-1.8.0-amazon-corretto

ADD https://nexus.osdc.io/repository/misc/gatk/GenomeAnalysisTK.jar /usr/local/bin/GenomeAnalysisTK.jar
#COPY GenomeAnalysisTK.jar /usr/local/bin

RUN ln -s /usr/local/bin/GenomeAnalysisTK.jar /usr/local/bin/gatk.jar

ENTRYPOINT ["java", "-jar", "/usr/local/bin/gatk.jar"]

CMD ["--help"]
