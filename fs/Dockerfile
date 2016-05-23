
FROM ubuntu:xenial
MAINTAINER Guillem Francès guillem.frances@upf.edu

# setup environment
RUN locale-gen en_US.UTF-8
ENV LANG en_US.UTF-8

# Set up some environment variables
ENV HOME /root
ENV BASE_DIR "${HOME}/projects"
ENV LAPKT_PATH "${BASE_DIR}/lapkt"
ENV LAPKT2_PATH "${LAPKT_PATH}/aptk2"
ENV FS_PATH "${BASE_DIR}/fs"
ENV FSBENCHMARKS "${BASE_DIR}/fs-benchmarks"
ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:${FS_PATH}/lib
ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:${LAPKT2_PATH}/lib
ENV LD_LIBRARY_PATH $LD_LIBRARY_PATH:${HOME}/local/lib
ENV FD_AIG_PATH "${HOME}/projects/downward-aig"
ENV PYTHONPATH "${FD_AIG_PATH}/src/translate:$PYTHONPATH"


# Create required directories
RUN mkdir -p $BASE_DIR && mkdir -p ~/local
WORKDIR $BASE_DIR

# Install required packages
# We install only those boost packages that are required by the project, 
# otherwise the image grows too large.
RUN apt-get update && apt-get install --no-install-recommends -y \
	build-essential \
	python3 \
	git \
	scons \
	openssh-client \
	ca-certificates \
	curl \
	mercurial \
	less \
	libboost-program-options-dev libboost-filesystem-dev libboost-system-dev \
	libboost-chrono-dev libboost-timer-dev libboost-serialization-dev \
    && rm -rf /var/lib/apt/lists/*


#################################
# Install & build the LAPKT toolkit
#################################
RUN git clone --depth 1 --single-branch --branch=v2-work https://github.com/miquelramirez/LAPKT-public.git lapkt \
	&& cd lapkt && git pull && cd aptk2 \
	&& scons

#################################
# Install & build Gecode 
#################################
# We install from source rather than use the package to minimize the bloat,
# since the official package installs by default all Gecode modules, including visualization tools, etc.
# We configure the build with only the strictly required modules
RUN curl -SL http://www.gecode.org/download/gecode-4.4.0.tar.gz | tar xz \
	&& cd gecode-4.4.0 \
	&& ./configure --prefix=$HOME/local \
	--disable-minimodel \
	--disable-examples \
	--disable-flatzinc \
	--disable-gist \
	--disable-driver \
	--disable-qt \
	--disable-mpfr \
	--disable-set-vars \
	--disable-float-vars \
	--disable-doc-tagfile \
	--disable-doc-dot \
	--disable-thread \
	&& make && make install

#################################
# Install & build the AIG fork of Fast Downward's PDDL parser
#################################
RUN hg clone https://gfrances@bitbucket.org/gfrances/downward-aig

ENV FS0_PATH "${FS0_PATH}"

#################################
# Install & build the FS planner
#################################
RUN git clone --depth 1 https://github.com/aig-upf/fs.git \
	&& cd fs \
	&& git pull \
	&& python ./build.py


#################################
# Download some benchmarks
#################################
RUN git clone --depth 1 https://gfrances@bitbucket.org/gfrances/fs-benchmarks.git \
	&& cd fs-benchmarks/generators \
	&& python3 generate.py --problems all


WORKDIR $BASE_DIR/fs
CMD ["bash"]
