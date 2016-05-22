
FROM ubuntu:xenial
MAINTAINER Guillem Francès guillem.frances@upf.edu

# setup environment
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8

ENV BASE_DIR "${HOME}/projects"
ENV LAPKT_PATH "${BASE_DIR}/lapkt"
ENV LAPKT2_PATH "${LAPKT_PATH}/aptk2"
ENV LD_LIBRARY_PATH "$LD_LIBRARY_PATH:${LAPKT2_PATH}/lib"
ENV FS_PATH "${BASE_DIR}/fs"
ENV FSBENCHMARKS "${BASE_DIR}/fs-benchmarks"
ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:${FS_PATH}/lib
ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:${LAPKT2_PATH}/lib
ENV FD_AIG_PATH "${HOME}/projects/downward/downward-aig"
ENV PYTHONPATH "${FD_AIG_PATH}/src/translate:$PYTHONPATH"

# Create required directories
RUN mkdir -p $BASE_DIR && mkdir -p ~/local
WORKDIR $BASE_DIR

# install basic tools
RUN apt-get update && apt-get install --no-install-recommends -y \
	build-essential \
	git \
	scons \
	openssh-client \
	ca-certificates \
	mercurial \
#	wget \ # Necessary only to get gecode
	libboost-dev \
	libgecode41v5 \
    && rm -rf /var/lib/apt/lists/*


#################################
# Install & build the LAPKT toolkit
#################################
RUN git clone https://github.com/miquelramirez/LAPKT-public.git lapkt \
	&& cd lapkt && git checkout v2-work && cd aptk2 \
	&& scons

#################################
# Install & build Gecode 
#################################
#RUN wget http://www.gecode.org/download/gecode-4.4.0.tar.gz \
#	&& tar xf gecode-4.4.0.tar.gz && rm gecode-4.4.0.tar.gz \
#	&& cd gecode-4.4.0 \
#	&& ./configure --prefix=$HOME/local && make -j 2 && make install

#################################
# Install & build the AIG fork of Fast Downward's PDDL parser
#################################
RUN hg clone https://gfrances@bitbucket.org/gfrances/downward-aig

ENV FS0_PATH "${FS0_PATH}"

#################################
# Install & build the FS planner
#################################
RUN git clone https://github.com/aig-upf/fs.git \
	&& cd fs \
	&& python ./build.py


CMD ["bash"]
