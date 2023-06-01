# gatk-docker

[![Docker Repository on Quay](https://quay.io/repository/ncigdc/gatk/status?token=7028d589-285d-44f6-a5be-d4858c613eb6 "Docker Repository on Quay")](https://quay.io/repository/ncigdc/gatk)

Repo for Dockerizing the GATK jar.

Quay Repository: https://quay.io/repository/ncigdc/gatk

# Versions
---

| Tag                   | GATK Version | Entrypoint                          |
|-----------------------|--------------|-------------------------------------|
| 3.7                   | 3.7          | `java -jar /usr/local/bin/gatk.jar` |
| 4.2.4.1               | 4.2.4.1      | `java -jar /usr/local/bin/gatk.jar` |
| 4.2.4.1-no-entrypoint | 4.2.4.1      | `/bin/sh -c` (default)              |

Other versions of GATK were removed due to the log4j vulnerability.

## Building
---

The `build.sh` script facilitates building all images:

`bash build.sh build`

These Docker images are based on Ubuntu 20.04.

Images of GATK4 are built from the `Dockerfile.multi` file.

The GATK 3.7 image is built from the `3.7/Dockerfile` and packages the included jar file.

The Makefile in each `<version>` directory provides the `make build-docker` target which will create an image with tags:

* `gatk:<version>`
* `gatk:<version>-<short commit>`

Note: version tags are named after corresponding directories containing a `Makefile`

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

Executing `docker run gatk:<version>` will print the help text of GATK.

Extra arguments after the image tag will be passed to `GATK`:

`docker run gatk:<version> ValidateSamFile  -I input.bam -MODE SUMMARY`

NOTE: the `4.2.4.1-no-entrypoint` image does not set a default entrypoint.

## Example CommandLineTool
---

```
cwlVersion: v1.0
class: CommandLineTool
id: gatk4_calculatecontamination
requirements:
  - class: DockerRequirement
    dockerPull: docker.osdc.io/ncigdc/gatk:4.2.4.1
  - class: InlineJavascriptRequirement

inputs:
  input:
    type: File
    inputBinding:
      prefix: --input

  tmp_dir:
    type: string
    default: "."
    inputBinding:
      prefix: --tmp-dir

  bam_nameroot:
    type: string

outputs:
  output:
    type: File
    outputBinding:
      glob: $(inputs.bam_nameroot + "_contamination.table")

arguments:
  - valueFrom: $(inputs.bam_nameroot + "_contamination.table")
    prefix: --output
    separate: true

baseCommand: [CalculateContamination]
```

# Contributing
---

General contributing guide available [here](https://github.com/NCI-GDC/portal-ui/blob/develop/CONTRIBUTING.md).

# License
---

[Apache 2.0](./LICENSE)

GATK is licensed under [Apache 2.0](https://github.com/broadinstitute/gatk/blob/master/LICENSE.TXT)
