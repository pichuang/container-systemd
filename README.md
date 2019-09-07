# Using Systemd with Container

Container technology, also known as just a container, is a method to package an application so it can run, with its dependencies, isolated from other linux processes.

Podman works correctly when the socket is activated. Because Podman is a fork/exec model, it can pass the conntected socket down to its children container processes. Docker cannot do this because of the client/server model.

## Recommend Confiugraiton

1. Put the specific configuration into Sysconfig `/etc/sysconfig/*`

The `/etc/sysconfig` directory contains a variety of system configuration files for mostly OS.

2. Put the service unit file into `/usr/lib/systemd/system/*`
- If you are Docker fans, remember put `After=docker.service` and `Requires=docker.service` for make sure the service will be started after running docker daemond.
- If you are Podman fans, remember remove flag `--restart` within `podman run` because podman is fork/exec model, no anymore daemon in system. All process controll (e.g. restart) should be coverd by `systemd`

## References
- [Podman and Buildah for Docker users](https://developers.redhat.com/blog/2019/02/21/podman-and-buildah-for-docker-users/)

