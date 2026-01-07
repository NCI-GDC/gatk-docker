ARG REPOSITORY=docker.osdc.io
ARG BUILDER_TAG=3.1.0
ARG VERSION=4.2.4.1

FROM ${REPOSITORY}/ncigdc/amzn2023-builder:${BUILDER_TAG}

ARG VERSION

LABEL version="${VERSION}"
LABEL description="GATK4 ${VERSION} (standalone jar from Nexus release zip)"

RUN dnf install -y java-17-amazon-corretto-headless unzip ca-certificates \
    && dnf clean all

ADD https://nexus.osdc.io/repository/github/broadinstitute/gatk/releases/download/${VERSION}/gatk-${VERSION}.zip \
    /tmp/gatk.zip

RUN set -eux; \
    mkdir -p /opt/gatk /usr/local/bin; \
    unzip -q /tmp/gatk.zip -d /opt/gatk; \
    test -f "/opt/gatk/gatk-${VERSION}/gatk-package-${VERSION}-local.jar"; \
    cp "/opt/gatk/gatk-${VERSION}/gatk-package-${VERSION}-local.jar" "/usr/local/bin/gatk-package-${VERSION}-local.jar"; \
    chmod a+r "/usr/local/bin/gatk-package-${VERSION}-local.jar"; \
    ln -sf "/usr/local/bin/gatk-package-${VERSION}-local.jar" "/usr/local/bin/gatk.jar"; \
    rm -f /tmp/gatk.zip; \
    rm -rf /opt/gatk

ENTRYPOINT ["java", "-jar", "/usr/local/bin/gatk.jar"]
CMD ["--help"]
