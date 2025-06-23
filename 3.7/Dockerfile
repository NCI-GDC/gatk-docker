FROM quay.io/ncigdc/bio-ubuntu:20.04

MAINTAINER Charles Czysz <czysz@uchicago.edu>

LABEL version="nightly-2016-02-25-gf39d340"
LABEL description="GATK3 nightly-2016-02-25-gf39d340"

RUN apt-get update -y \
    && apt-get install -y \
    openjdk-8-jre-headless

ADD https://nexus.osdc.io/repository/misc/gatk/GenomeAnalysisTK.jar /usr/local/bin/GenomeAnalysisTK.jar
#COPY GenomeAnalysisTK.jar /usr/local/bin

RUN ln -s /usr/local/bin/GenomeAnalysisTK.jar /usr/local/bin/gatk.jar

ENTRYPOINT ["java", "-jar", "/usr/local/bin/gatk.jar"]

CMD ["--help"]
