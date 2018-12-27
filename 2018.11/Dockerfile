FROM buildpack-deps:stretch-scm
MAINTAINER JJ Merelo

RUN groupadd -r perl6 && useradd -r -g perl6 perl6

ARG rakudo_version=2018.11
ENV rakudo_version=${rakudo_version}

RUN buildDeps=' \
        gcc \
        libc6-dev \
        libencode-perl \
        make \
    ' \
    url="https://github.com/rakudo/rakudo/archive/${rakudo_version}.tar.gz" \
    tmpdir="$(mktemp -d)" \
    && set -x \
    && export GNUPGHOME="$tmpdir" \
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
    && rm -rf $tmpdir \
    && apt-get purge -y --auto-remove $buildDeps

ENV PATH=$PATH:/usr/share/perl6/site/bin

CMD ["perl6"]
