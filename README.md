# Rakudo NoStar

[![Build Status](https://travis-ci.com/JJ/rakudo-nostar.svg?branch=master)](https://travis-ci.com/JJ/rakudo-nostar)

This Docker image has been forked from  [Rakudo Star](https://github.com/perl6/docker), which is a Perl 6 compiler distribution that includes MoarVM
virtual machine, Rakudo Perl 6 compiler, a suite of modules that users
may find useful, and language documentation. Instead of limiting
itself to the Star builds, it's got images for every monthly
release. It does not include most of the modules Rakudo does, limiting
itself to the most needed ones.

> If you need some other module to be added, just raise an issue
> here. 

Project homepage: https://rakudo.org

GitHub repository: https://github.com/rakudo/rakudo

The Dockerfile responsible: https://github.com/JJ/rakudo-nostar/tree/master/Dockerfile

Perl 6 Language Specification: https://github.com/perl6/roast

Perl 6 Language Documentation: https://docs.perl6.org/

# Build

You can build an image from this Dockerfile as indicated below:

    $ docker build -t rakudo-nostar /path_to_dockerfile/

In addition, you can specify the version of Rakudo Star that you want at build time:

    $ docker build --build-arg rakudo_version=${DESIRED_VERSION} -t rakudo-nostar /path_to_dockerfile/

If no version is specified, it will default to the version listed in the Dockerfile. It is recommended that
you use the default version.

# Usage

Running a short-term foreground process with the image will launch a Perl 6 REPL:

    $ docker run --rm -it jjmerelo/rakudo-nostar
    > say 'Hello, Perl!'
    Hello, Perl!

You can also provide perl6 command line switches to a temporary container:

    $ docker run --rm jjmerelo/rakudo-nostar perl6 -e 'say "Hello!"'

In addition, you can run a script located in the current folder:

    $ docker run --rm -v "$(pwd):/script" jjmerelo/rakudo-nostar perl6 /script/my_p6_script.p6

# Contributing/Getting Help

Many Perl 6 developers are present on [#perl6 on Freenode](https://webchat.freenode.net/?channels=#perl6)

Issues for Rakudo are tracked on https://github.com/rakudo/rakudo/issues
