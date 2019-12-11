FROM httpd:2.4.39

ENV MOD_PERL_VERSION 2.0.11
ENV PERL_VERSION 5.28.2

ENV PATH /opt/perl-$PERL_VERSION/bin:$PATH

RUN apt-get update && \
    apt-get install -yq --no-install-recommends perl ca-certificates curl build-essential && \
    curl -sfL https://raw.githubusercontent.com/tokuhirom/Perl-Build/master/perl-build | perl - $PERL_VERSION /opt/perl-$PERL_VERSION/ -Duseshrplib -j "$(nproc)" && \
    curl -sfLO http://ftp.jaist.ac.jp/pub/apache/perl/mod_perl-$MOD_PERL_VERSION.tar.gz && \
    echo "ca2a9e18cdf90f9c6023e786369d5ba75e8dac292ebfea9900c29bf42dc16f74 *mod_perl-$MOD_PERL_VERSION.tar.gz" | sha256sum -c && \
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
