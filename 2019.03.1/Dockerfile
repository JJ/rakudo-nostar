FROM buildpack-deps:stretch-scm
MAINTAINER JJ Merelo

RUN groupadd -r perl6 && useradd -r -g perl6 perl6

ARG rakudo_version=2019.03.1
ENV rakudo_version=${rakudo_version}
ENV PATH=$PATH:/usr/share/perl6/site/bin

RUN buildDeps=' \
        gcc \
        libc6-dev \
        libencode-perl \
        libssl-dev \
        make \
    ' \
    url="https://github.com/rakudo/rakudo/archive/${rakudo_version}.tar.gz" \
    tmpdir="$(mktemp -d)" \
    && set -x \
    && apt-get update \
    && apt-get --yes install --no-install-recommends $buildDeps \
    && rm -rf /var/lib/apt/lists/* \
    && mkdir ${tmpdir}/rakudo \
    \
    && curl -fsSL $url -o ${tmpdir}/rakudo.tar.gz \
    \
    && tar xzf ${tmpdir}/rakudo.tar.gz --strip-components=1 -C ${tmpdir}/rakudo \
    && ( \
        cd ${tmpdir}/rakudo \
        && perl Configure.pl --prefix=/usr --gen-moar \
        && make install \
    ) \
    \
    && cd $tmpdir \
    && git clone https://github.com/ugexe/zef.git \
    && prove -v -e 'perl6 -I zef/lib' zef/t \
    && perl6 -Izef/lib zef/bin/zef --verbose install ./zef \
    && zef install Linenoise LWP::Simple\
    && rm -rf $tmpdir 


CMD ["perl6"]
