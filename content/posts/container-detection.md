+++
title = "Detect whether you are inside a container or not"
date = 2023-07-27
template = "post.html"

[taxonomies]
categories = ["Security", "SysAdmin"]
tags = ["Container", "Docker"]
+++
Container technologies ([chroot][chroot], [LXC][lxc], …) are very common these
days, especially since the massive adoption of [Docker][docker].

One of the use cases of container technologies is to isolate services from each
others and from the host system. As a result, in case of an intrusion, the
attacker would be in theory trapped inside a container. From the attacker’s
perspective, it is important to be able to detect if a compromised service lives
in a restricted environment such as a Docker container or if it runs directly on
the host operating system.

One way to do so is to have a look at the [inode][inode] of the `/` mount point
(`ls -id /`).  On the host system it will be very low (generally 1 or 2) whereas
in a container it will generally be quite high (4851522 in the asciicast):

{{ asciinema(id="318880") }}

On Linux, one of the underlying mechanisms commonly used to create a container
is [cgroups][cgroups]. The `/proc/1/cgroup` virtual file will give you the
control groups of the `init` process which are generally `/` for the majority of
the controllers by default. However, if you have a look at `/proc/1/cgroup` from
the inside of a container, the result is likely to be different as you can see:

{{ asciinema(id="318929") }}

When containers are created by a Docker Engine, this last one adds a
[`/.dockerenv`][moby-dockerenv] file into them. The presence of this file is
even [used to this date by some underlying components of the Moby
project][moby-is-running-in-container] for the exact same purpose, knowing if
they run inside a container:

{{ asciinema(id="573103") }}

 [cgroups]: https://en.wikipedia.org/wiki/cgroups
 [chroot]: https://en.wikipedia.org/wiki/chroot
 [docker]: https://www.docker.com/
 [inode]: https://en.wikipedia.org/wiki/Inode
 [lxc]: https://linuxcontainers.org/
 [moby-dockerenv]: https://github.com/moby/moby/blob/219f21bf07502b447095649b5a2764661737f164/daemon/initlayer/setup_unix.go#L30
 [moby-is-running-in-container]: https://github.com/moby/moby/blob/219f21bf07502b447095649b5a2764661737f164/libnetwork/drivers/bridge/setup_bridgenetfiltering.go#L162-L165
