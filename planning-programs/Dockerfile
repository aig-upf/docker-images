
FROM ubuntu:xenial
MAINTAINER Guillem Francès guillem.frances@upf.edu

# Set up environment variables
RUN locale-gen en_US.UTF-8
ENV LANG=en_US.UTF-8 \ 
	CXX=g++ \
	HOME=/root \
	BASE_DIR=/root \
	PROJECT_URL=https://bitbucket.org/sergioJimenezUPF/planning-programs/get/master.tar.gz


RUN mkdir -p $BASE_DIR
WORKDIR $BASE_DIR


# install basic tools
RUN apt-get update && apt-get install --no-install-recommends -y \
	build-essential \
	ca-certificates \
	curl \
	scons \
	gcc-multilib \
	flex \
	bison \
    && rm -rf /var/lib/apt/lists/*


#################################
# Download and build the project
#################################
RUN curl -SL $PROJECT_URL | tar -xz \
	&& mv sergioJimenezUPF* planning-programs \
	&& cd planning-programs \
	&& scons


CMD ["bash"]

curl -SL https://bitbucket.org/sergioJimenezUPF/planning-programs/get/master.tar.gz
