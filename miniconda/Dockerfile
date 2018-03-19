FROM debian:9.4
 
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
 
RUN apt-get update --fix-missing \
 && apt-get install -y \
      bzip2 \
      ca-certificates \
      git \      
      libglib2.0-0 \
      libsm6 \
      libxext6 \
      libxrender1 \
      wget

ENV MINICONDA2_VERSION 4.4.10 
 
RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh \
 && wget --quiet https://repo.continuum.io/miniconda/Miniconda2-${MINICONDA2_VERSION}-Linux-x86_64.sh -O ~/miniconda.sh \ 
 && bin/bash ~/miniconda.sh -b -p /opt/conda \
 && rm ~/miniconda.sh
 
RUN apt-get install -y \
      curl \
      dpkg \
      grep \
      sed \
 && TINI_VERSION=`curl https://github.com/krallin/tini/releases/latest | grep -o "/v.*\"" | sed 's:^..\(.*\).$:\1:'` \
 && curl -L "https://github.com/krallin/tini/releases/download/v${TINI_VERSION}/tini_${TINI_VERSION}.deb" > tini.deb \
 && dpkg -i tini.deb \
 && rm tini.deb \
 && apt-get clean
 
ENV PATH /opt/conda/bin:$PATH
 
ENTRYPOINT ["/usr/bin/tini", "--"]
 
CMD ["/bin/bash"]
