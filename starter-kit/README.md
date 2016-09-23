# AIG Planning Starter Kit

[![](https://images.microbadger.com/badges/image/aigupf/starter-kit.svg)](https://microbadger.com/images/aigupf/starter-kit "")

This directory contains the Docker definition for an image 
with a number of planners, planning domains and planning tools compiled and ready to be used.


## Available Tools

As of now, the image features the following planners:

* The [Pyperplan](https://bitbucket.org/malte/pyperplan) lightweight Python STRIPS planner.
* The [Fast Downward](http://www.fast-downward.org/) planner.
* The [Mercury](https://helios.hud.ac.uk/scommv/IPC-14/repo_planners/Mercury-fixed.zip) planner, namely, the patched version that can be downloaded
from the [IPC'14 website](https://helios.hud.ac.uk/scommv/IPC-14/errPlan.html).
* The [PROBE](https://github.com/aig-upf/probe) planner.
* The [LAPKT](http://lapkt.org/) planning toolkit.

Additionally, the image also features:

* The [VAL plan validation system](https://github.com/KCL-Planning/VAL).
* The full suite of benchmarks from the [Planning.Domains project](http://planning.domains/).


Each of the previous tools lies on a separate subdirectory under `/root/projects`.


## Basic Usage
In order to use the docker images, you need to [have Docker installed on your machine](https://docs.docker.com/engine/installation).
Once that is done, you can pull the image with

```shell
docker pull aigupf/starter-kit
```

Then start the container interactively:

```shell
docker run -it aigupf/starter-kit
```

and use any of the provided tools, e.g.

```shell
./pyperplan/src/pyperplan.py planning-researchers-classical-domains/classical/blocks/probBLOCKS-6-0.pddl
```


## Advanced Usage


Assuming we have, say, some benchmarks on a `~/benchmarks` directory on the host machine, and we want to run some planner
in the starter kit on those benchmarks.
We can start the docker container [mounting the desired directory](https://docs.docker.com/engine/tutorials/dockervolumes/#mount-a-host-directory-as-a-data-volume)
as follows:

```shell
docker run -it -v ~/benchmarks:/root/projects/benchmarks aigupf/starter-kit
```

and the desired benchmarks will be accessible under `/root/projects/benchmarks`.

Alternatively, we can use the same technique in order to have some planner output its results to a directory from the host machine:

```shell
docker run -it -v ~/output:/root/projects/output aigupf/starter-kit
./pyperplan/src/pyperplan.py planning-researchers-classical-domains/classical/blocks/probBLOCKS-6-0.pddl > ./output/
```

which lets us work with the output from the host machine

```shell
$ cat ~/output/out.txt 
2016-09-23 13:31:56,345 INFO     Found domain /root/projects/planning-researchers-classical-domains/classical/blocks/domain.pddl
2016-09-23 13:31:56,350 INFO     using search: breadth_first_search
2016-09-23 13:31:56,351 INFO     using heuristic: None
```


## Extending the image


