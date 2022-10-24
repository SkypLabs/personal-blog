+++
title = "[Qubes OS] Make Docker use private storage"
date = 2023-01-20
template = "post.html"

[taxonomies]
categories = ["SysAdmin"]
tags = ["Qubes OS", "Docker"]
+++
The Docker engine stores all image layers in `/var/lib/docker` by default, which
is not compatible with Qubes OS' template system. You would lose all your saved
images each time you restart the app qube in question.

You can change the Docker engine's root data directory by editing
`/etc/docker/daemon.json` in your template:

```json
{
  "data-root": "/usr/local/lib/docker"
}
```

The list of the directories that can be used to store Docker's data persistently
across reboots can be found [here][qubes-os-persistence].

Once the configuration file in place in your template, you can then boot up any
app qube using this template and check if the new location has correctly been
taken into account:

```raw
$ sudo docker info | grep -i 'root dir'
 Docker Root Dir: /usr/local/lib/docker
```

Please note that if you already had Docker images stored in an qube app before
making this configuration change, they won't be available in Docker any more.
You would need to move them to the new location or download them again.

 [qubes-os-persistence]: https://www.qubes-os.org/doc/templates/#inheritance-and-persistence "Qubes OS - Inheritance and Persistence"
