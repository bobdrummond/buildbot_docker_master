# Buildbot Master for DockerLatentWorker
[Buildbot DockerLatentWorker documentation](http://docs.buildbot.net/current/manual/cfg-workers-docker.html)

## Ubuntu 16.04 / Mint 18 systemd Setup

Steps required to expose the docker daemon on a tcp port:

* Create these files:
  * /etc/systemd/system/docker.service.d/override.conf
    ```
    [Service]
    ExecStart=
    ExecStart=/usr/bin/dockerd
    ```
  * /etc/docker/daemon.json
    ```
    {
  	"hosts": ["fd://", "tcp://0.0.0.0:2375"]
    }
    ```
* Run `sudo systemctl restart docker`
* Check with:
  * `sudo journalctl -u docker`
  * `docker -H tcp://localhost:2375 version`
