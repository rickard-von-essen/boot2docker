Building boot2docker.iso for Parallels Desktop
==============================================

Preparations
------------

Before building run the following in the root of this repository:

```
open /Applications/Parallels\ Desktop.app/Contents/Resources/Tools/prl-tools-lin.iso && \
  mkdir kmods && \
  tar -C kmods -xzf /Volumes/Parallels\ Tools/kmods/prl_mod.tar.gz && \
  tar -C rootfs/rootfs/usr/local/bin/ -xzf /Volumes/Parallels\ Tools//tools/prltools.x64.tar.gz \
    --include='*/prl_nettool' --include='*/prl_snapshot' --include='*/prlhosttime' \
    --strip-components 2 && \
  tar -C rootfs/rootfs/usr/local/bin/ -xzf /Volumes/Parallels\ Tools//tools/prltools.x64.tar.gz \
    --include='*/prltoolsd' --strip-components 4
```

A ```git status``` should show the following untracked files:

        kmods/
        rootfs/rootfs/usr/local/bin/prl_nettool
        rootfs/rootfs/usr/local/bin/prl_showvmcfg
        rootfs/rootfs/usr/local/bin/prl_snapshot
        rootfs/rootfs/usr/local/bin/prlhosttime
        rootfs/rootfs/usr/local/bin/prltoolsd


Build
-----

Build as normal with:

```
$ docker build -t boot2docker . && docker run --rm boot2docker > boot2docker.iso
```

See [How to build boot2docker.iso locally](BUILD.md).

License
-------

**The resulting _boot2docker.iso_ will contain proprietary software which can NOT be distributed, see paragraph 1.7 in the [EULA](http://www.parallels.com/eu/about/legal/eula/).**
