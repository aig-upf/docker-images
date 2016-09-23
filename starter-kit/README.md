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
