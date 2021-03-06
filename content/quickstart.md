---
title: Quick Start
---

This chapter is for impatient people who don't like reading
documentation. For more in-depth information you are kindly referred to
subsequent chapters.

  - Install single-user Nix by running the following:

        $ bash <(curl https://nixos.org/nix/install)

    This will install Nix in `/nix`. The install script will create
    `/nix` using `sudo`, so make sure you have sufficient rights. (For
    other installation methods, see [part\_title](#chap-installation).)

  - See what installable packages are currently available in the
    channel:

        $ nix-env -qa
        docbook-xml-4.3
        docbook-xml-4.5
        firefox-33.0.2
        hello-2.9
        libxslt-1.1.28
        ...

  - Install some packages from the channel:

        $ nix-env -i hello

    This should download pre-built packages; it should not build them
    locally (if it does, something went wrong).

  - Test that they work:

        $ which hello
        /home/eelco/.nix-profile/bin/hello
        $ hello
        Hello, world!

  - Uninstall a package:

        $ nix-env -e hello

  - You can also test a package without installing it:

        $ nix-shell -p hello

    This builds or downloads GNU Hello and its dependencies, then drops
    you into a Bash shell where the `hello` command is present, all
    without affecting your normal environment:

        [nix-shell:~]$ hello
        Hello, world!

        [nix-shell:~]$ exit

        $ hello
        hello: command not found

  - To keep up-to-date with the channel, do:

        $ nix-channel --update nixpkgs
        $ nix-env -u '*'

    The latter command will upgrade each installed package for which
    there is a “newer” version (as determined by comparing the version
    numbers).

  - If you're unhappy with the result of a `nix-env` action (e.g., an
    upgraded package turned out not to work properly), you can go back:

        $ nix-env --rollback

  - You should periodically run the Nix garbage collector to get rid of
    unused packages, since uninstalls or upgrades don't actually delete
    them:

        $ nix-collect-garbage -d

This section describes how to install and configure Nix for first-time
use.
