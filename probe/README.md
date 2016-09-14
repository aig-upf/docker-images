# PROBE Docker Image

[![](https://images.microbadger.com/badges/image/aigupf/probe.svg)](https://microbadger.com/images/aigupf/probe "")

This directory contains the Docker definition for the image of the [PROBE](https://github.com/aig-upf/probe) planner.



## Usage
In order to use the docker images, you need to have Docker installed on your machine.
If you still don't, you'll need to follow a few easy [Docker installation steps](https://docs.docker.com/engine/installation).

Once that is done, you can pull the image with

```shell
docker pull aigupf/probe
```

And then start the container interactively and run the planner normally:

```shell
docker run -it aigupf/probe
./probe -d benchhmarks/blocksworld/domain.pddl -i benchhmarks/blocksworld/probBLOCKS-5-0.pddl -o plan.txt
```
