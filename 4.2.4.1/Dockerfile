ARG REPOSITORY=docker.osdc.io
ARG BUILDER_TAG=3.1.0
ARG VERSION=4.2.4.1

FROM ${REPOSITORY}/ncigdc/amzn2023-builder:${BUILDER_TAG}

ARG VERSION

LABEL version="${VERSION}"
LABEL description="GATK4 ${VERSION} (jar from nexus maven-public, /usr/local/bin/gatk.jar)"

RUN dnf install -y java-1.8.0-amazon-corretto ca-certificates \
    && dnf clean all

ADD https://nexus.osdc.io/repository/maven-public/org/broadinstitute/gatk/${VERSION}/gatk-${VERSION}.jar \
    /usr/local/bin/gatk-${VERSION}.jar

RUN chmod a+r /usr/local/bin/gatk-${VERSION}.jar \
    && ln -sf /usr/local/bin/gatk-${VERSION}.jar /usr/local/bin/gatk.jar

CMD ["java", "-jar", "/usr/local/bin/gatk.jar", "--help"]
