FROM ubuntu:20.04
ENV LANG=C.UTF-8 DEBIAN_FRONTEND=noninteractive
ENV PATH /opt/conda/bin:$PATH

# Install conda
RUN apt-get update --fix-missing && \
    apt-get install --no-install-recommends -y curl ca-certificates && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
RUN curl https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -o miniconda.sh \
    && bash miniconda.sh -b -p /opt/conda\
    && rm miniconda.sh \
    && conda init \
    && conda update -n base -c defaults conda \
    && conda clean -y --all

# Setup project folder and copy environment.yml
WORKDIR /app
COPY ./environment.yml ./

# Install conda dependencies in default environment
RUN conda env update -n=base -f=environment.yml && conda clean -y --all

# Copy project to /app folder
COPY . ./

