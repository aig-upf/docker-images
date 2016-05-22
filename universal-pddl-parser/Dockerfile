
FROM ubuntu:xenial
MAINTAINER Guillem Francès guillem.frances@upf.edu

# setup environment
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8

ENV BASE_DIR "${HOME}/projects"

RUN mkdir -p $BASE_DIR
WORKDIR $BASE_DIR


# install basic tools
RUN apt-get update && apt-get install --no-install-recommends -y \
	build-essential \
	git \
	scons \
	openssh-client \
	ca-certificates \
    && rm -rf /var/lib/apt/lists/*


#################################
# Install & build the universal PDDL parser
#################################
RUN git clone https://github.com/aig-upf/universal-pddl-parser.git \
	&& cd universal-pddl-parser \
	&& scons


CMD ["bash"]
