FROM debian:jessie

RUN apt-get update && apt-get install -y \
        curl \
        g++ \
        gfortran \
        libreadline6-dev \
        make \
        rsync \
        xorg-dev \
        --no-install-recommends \
        && rm -rf /var/lib/apt/lists/*

ENV R_MAJOR 3
ENV R_VERSION 3.1.2

RUN curl -sSL http://cran.r-project.org/src/base/R-$R_MAJOR/R-$R_VERSION.tar.gz \
        | tar -vxzC /usr/src \
        && cd /usr/src/R-$R_VERSION \
        && ./tools/rsync-recommended \
        && ./configure \
        && make \
        && make check-all \
        && make install \
        && apt-get purge -y --auto-remove \
            curl \
            make

# Set the default CRAN Repo
RUN mkdir -p /etc/R \
    && echo 'options(repos = list(CRAN = "http://cran.rstudio.com/"))' >> /etc/R/Rprofile.site

CMD ["R"]
