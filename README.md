# gatk-docker

[![Docker Repository on Quay](https://quay.io/repository/ncigdc/gatk/status?token=7028d589-285d-44f6-a5be-d4858c613eb6 "Docker Repository on Quay")](https://quay.io/repository/ncigdc/gatk)

Repo for Dockerizing the GATK jar.

# Versions

---

- 3.7: Repo contains jar
- 4.2.4.1
  - With and without pre-defined entrypoint

Other versions of GATK were removed due to the log4j vulnerability.

## Building
---
These Docker images are based on Ubuntu 20.04.

The Makefile in each directory provides the `make build-docker` target which will create an image with tags:

`gatk:<version>`
`gatk:<version>-<short commit>`

## Running
---
The default entrypoint of these images is

```
java -jar /usr/local/bin/gatk.jar
```

and the default command is

```
--help
```

Thus, `docker run gatk:<version>` will print the help text of GATK.

NOTE: the `4.2.4.1-no-entrypoint` image does not set a default entrypoint.

## CommandLineTool
---

