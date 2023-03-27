virtual-dsm
=============

[![test_img]][test_url]
[![gh_last_release_svg]][gh_last_release_url]
[![Docker Pulls Count]][dsm-docker-hub]

[test_img]: https://github.com/kroese/virtual-dsm/actions/workflows/test.yaml/badge.svg
[test_url]: https://github.com/kroese/virtual-dsm/actions

[gh_last_release_svg]: https://img.shields.io/docker/v/kroese/virtual-dsm?arch=amd64&sort=date
[gh_last_release_url]: https://hub.docker.com/r/kroese/virtual-dsm

[Docker Pulls Count]: https://img.shields.io/docker/pulls/kroese/virtual-dsm.svg?style=flat
[dsm-docker-hub]: https://hub.docker.com/r/kroese/virtual-dsm

A docker container that runs Synology's Virtual DSM v7.

## Using the container

Via `docker run`:

```bash
$ docker run --rm -it \
    -p 5000:5000 \
    -e DISK_SIZE=16G \
    --cap-add NET_ADMIN \
    --cap-add SYS_ADMIN \
    --device=/dev/kvm:/dev/kvm \
    --device=/dev/fuse:/dev/fuse \
    --device=/dev/net/tun:/dev/net/tun \    
    kroese/virtual-dsm:latest
```

Via `docker-compose.yml`:

```yaml
version: "3"
services:
    vm:
        image: kroese/virtual-dsm:latest
        cap_add:
            - NET_ADMIN
            - SYS_ADMIN
        devices:
            - /dev/kvm
            - /dev/fuse
            - /dev/net/tun
        ports:
            - 5000:5000
        environment:
            DISK_SIZE: 16G
        restart: always
```

