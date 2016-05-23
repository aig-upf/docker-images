# FS Docker Image

This directory contains the Docker definition for the image of the [FS Planner](https://github.com/aig-upf/fs).



## Usage
In order to use the docker images, you need to have Docker installed on your machine.
If you still don't, you'll need to follow a few easy [Docker installation steps](https://docs.docker.com/engine/installation).

Once that is done, you can pull the image with

```shell
docker pull aigupf/fs
```

And then start the container interactively and run the planner normally:

```shell
docker run -it aigupf/fs
python3 preprocessor/runner.py --tag test --instance $FSBENCHMARKS/benchmarks/counters-fn/instance_5.pddl --run --driver=smart
```
