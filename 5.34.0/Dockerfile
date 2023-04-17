FROM httpd:2.4.57

ARG PERL_VERSION=5.34.0

ENV MOD_PERL_VERSION 2.0.12
ENV MOD_PERL_CHECKSUM f5b821b59b0fdc9670e46ed0fcf32d8911f25126189a8b68c1652f9221eee269
ENV PERL_VERSION $PERL_VERSION

ENV PATH /opt/perl-$PERL_VERSION/bin:$PATH

SHELL ["/bin/bash", "-o", "pipefail", "-c"]

RUN apt-get update && \
    apt-get install -yq --no-install-recommends perl ca-certificates curl build-essential libapr1-dev libaprutil1-dev && \
    curl -sfL https://raw.githubusercontent.com/tokuhirom/Perl-Build/master/perl-build | perl - $PERL_VERSION /opt/perl-$PERL_VERSION/ -Duseshrplib -j "$(nproc)" && \
    curl -sfLO https://dlcdn.apache.org/perl/mod_perl-$MOD_PERL_VERSION.tar.gz && \
    echo "$MOD_PERL_CHECKSUM *mod_perl-$MOD_PERL_VERSION.tar.gz" | sha256sum -c && \
    tar xzf mod_perl-$MOD_PERL_VERSION.tar.gz && \
    cd mod_perl-$MOD_PERL_VERSION && \
    /opt/perl-$PERL_VERSION/bin/perl Makefile.PL MP_NO_THREADS=1 && \
    make -j "$(nproc)" && \
    make install && \
    cd .. && \
    rm -rf mod_perl-$MOD_PERL_VERSION mod_perl-$MOD_PERL_VERSION.tar.gz && \
    apt-get remove -yq perl ca-certificates curl build-essential && \
    apt-get autoremove -yq && \
    rm -rf /var/lib/apt/lists/*
