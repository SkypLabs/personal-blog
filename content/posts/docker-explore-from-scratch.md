+++
title = "[Docker] Explore a container's file system from scratch"
date = 2022-04-13
template = "post.html"

[taxonomies]
categories = ["SysAdmin"]
tags = ["Docker"]
+++
Generally, when I want to explore the file system of a Docker container, I do it
interactively by executing a shell inside it, something like:

```
$ docker exec -it container_name sh
$ ls
...
```

But sometimes the image of the container I want to explore does not contain any
tools for this purpose. No `ls`, no `cat`, not even a shell.  It is especially
the case when building Docker images [from scratch][docker-from-scratch], which
is very common with [multi-stage builds][docker-multi-stage-builds].

One solution is to rely on the [`docker export`][docker-export] tool which
allows to "export a container's filesystem as a tar archive". By default, it
writes the tar archive to `STDOUT`, which means it can be easily piped into the
`tar` command-line tool to list its contents on the fly:

```
$ docker export 7c1f2edd42c4 | tar -tv | tee filesystem.txt
-rwxr-xr-x root/root         0 2022-04-04 09:46 .dockerenv
drwxr-xr-x root/root         0 2022-03-19 15:52 bin/
-rwxr-xr-x root/root  45687736 2022-03-19 15:52 bin/node
...
```

 [docker-export]: https://docs.docker.com/engine/reference/commandline/export/
 [docker-from-scratch]: https://hub.docker.com/_/scratch/
 [docker-multi-stage-builds]: https://docs.docker.com/develop/develop-images/multistage-build/
