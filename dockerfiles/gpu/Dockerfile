# docker image for running DeepFigures on a gpu

FROM tensorflow/tensorflow:1.15.0-py3

ARG DEBIAN_FRONTEND=noninteractive

ENV LC_ALL C.UTF-8

# install system packages

RUN apt-get clean \
    && apt-get update --fix-missing \
    && apt-get install -y \
    git \
    curl \
    gcc \
    build-essential \
    tcl \
    g++ \
    zlib1g-dev \
    libjpeg8-dev \
    libtiff5-dev \
    libpng-dev \
    tcl-dev \
    tk-dev \
    python3 \
    python3-pip \
    python3-tk \
    ghostscript \
    openjdk-8-jre \
    poppler-utils \
    texlive-latex-base \
    texlive-fonts-recommended \
    texlive-fonts-extra \
    texlive-latex-extra

RUN git clone https://github.com/jasperproject/jasper-client.git jasper && \
    chmod +x jasper/jasper.py && \
    pip3 install -r jasper/client/requirements.txt

WORKDIR /work

# install python packages

ADD ./requirements.txt /work

RUN pip3 install --upgrade pip \
    && pip install Cython==0.25.2
RUN pip3 install -r ./requirements.txt

RUN pip3 install fastparquet

RUN pip3 install --upgrade beautifulsoup4

ADD ./vendor/tensorboxresnet /work/vendor/tensorboxresnet
RUN pip3 install -e /work/vendor/tensorboxresnet

RUN pip3 install tensorflow==1.15

RUN pip3 install scipy==1.0.1
RUN pip3 install pdf2image

RUN apt-get install -y python-poppler

ADD . /work
RUN pip3 install --quiet -e /work

CMD [ "/bin/bash" ]
