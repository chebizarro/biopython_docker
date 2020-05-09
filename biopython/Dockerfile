FROM ubuntu:18.04
MAINTAINER Tiago Antao <tra@popgen.net>

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update \
    && apt-get upgrade -y --force-yes \
    && apt-get install -y --force-yes \
    build-essential \
    git \
    python3-numpy \
    wget \
    gcc \
    g++ \
    gcc-5 \
    g++-5 \
    python3-dev \
    unzip \
    make \
    python3.6 \
    python3-matplotlib \
    python3-reportlab \
    python3-pip r-base \
    clustalw \
    fasttree \
    t-coffee python3-pil \
    bwa \
    ncbi-blast+ \
    emboss \
    clustalo \
    phylip \
    mafft \
    muscle \
    samtools \
    phyml \
    wise \
    raxml \
    language-pack-en \
    paml \
    probcons \
    python3-pandas \
    python3.6-dev \
    libxft-dev \
    && apt-get clean

#for Phylo_CDAO
RUN pip3 install pip --upgrade
RUN pip3 install rdflib --upgrade \
    && pip3 install cython --upgrade \
    && pip3 install numpy --upgrade \
    && pip3 install Pillow --upgrade \
    && pip3 install matplotlib --upgrade \
    && pip3 install pandas --upgrade

#Manual software
RUN echo "export DIALIGN2_DIR=/tmp" >> .bashrc

#reportlab fonts
RUN wget http://www.reportlab.com/ftp/fonts/pfbfer.zip
WORKDIR cd /usr/lib/python3.6/dist-packages/reportlab
RUN  mkdir fonts
WORKDIR cd /usr/lib/python3.6/dist-packages/reportlab/fonts
RUN unzip /pfbfer.zip \
    && mkdir -p /usr/lib/python3.6/dist-packages/reportlab/fonts
WORKDIR /usr/lib/python3.6/dist-packages/reportlab/fonts
RUN unzip /pfbfer.zip
WORKDIR /
RUN rm pfbfer.zip

#genepop
RUN mkdir genepop
WORKDIR /genepop
RUN wget http://kimura.univ-montp2.fr/~rousset/sources.tar.gz \
    && tar zxf sources.tar.gz \
    && g++ -DNO_MODULES -o Genepop GenepopS.cpp -O3 \
    && cp Genepop /usr/bin
WORKDIR /
RUN rm -rf genepop

#msaprobs
RUN wget "http://sourceforge.net/projects/msaprobs/files/latest/download?source=files" -O MSA.tar.gz \
    && tar zxf MSA.tar.gz
WORKDIR /MSAProbs-0.9.7/MSAProbs
RUN make \
    && cp msaprobs /usr/bin
WORKDIR /

#fastsimcoal
RUN wget http://cmpg.unibe.ch/software/fastsimcoal2/downloads/fsc_linux64.zip \
    && unzip fsc_linux64.zip \
    && chmod a+x fsc_linux64/fsc25221 \
    && cp fsc_linux64/fsc25221 /usr/bin/fsc252 \
    && rm -rf fsc_*

#DSSP
RUN wget ftp://ftp.cmbi.ru.nl/pub/software/dssp/dssp-2.0.4-linux-amd64 \
    && mv dssp-2.0.4-linux-amd64 /usr/bin/dssp \
    && chmod a+x /usr/bin/dssp

#XXmotif
#Needs gcc/g++ 5/6
RUN update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 5
RUN update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-5 5
RUN wget https://github.com/soedinglab/xxmotif/archive/master.zip \
    && unzip master.zip \
    && rm master.zip \
    && cd xxmotif-master \
    && mkdir build \
    && cd build \
    && cmake .. \
    && make \
    && cp XXmotif $PREFIX/bin \
    && cd / \
    && rm -r xxmotif-master
        
ENV PYTHON_PATH /biopython

#Biopython
RUN git clone https://github.com/biopython/biopython.git
WORKDIR /biopython
RUN python3.6 setup.py install

#set default python version to 3.6
RUN touch ~/.bash_aliases \
	  && echo alias python=\'python3.6\' > ~/.bash_aliases
