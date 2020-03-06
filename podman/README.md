## Podman

_Podman_ besitzt für Linux Mint aktuell noch keine Paketquelle. Daher muss die Paketquelle für Ubuntu 18.04 genutzt
werden. Das funktioniert, da Linux Mint 19.3 auf Ubuntu 18.04 basiert.

### Installation von Podman

In der [offiziellen Installationsanleitung](https://podman.io/getting-started/installation.html) unter Ubuntu finden wir die folgende
Anleitung für die Installation:

```bash
. /etc/os-release
sudo sh -c "echo 'deb http://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_${VERSION_ID}/ /' > /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list"
wget -nv https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable/xUbuntu_${VERSION_ID}/Release.key -O- | sudo apt-key add -
sudo apt-get update -qq
sudo apt-get -qq -y install podman
```

Diese Kommandos funktionieren unter Linux Mint 19.3 zwar, führen aber nicht zu einer Installation von _podman_, da die
Paketquelle mit der Version von Linux Mint (19.3) und dem Ubuntu Prefix nichts anfangen kann
(`... :/stable/xUbuntu_19.3/ ...`).

Aus diesem Grund müssen die Kommandos leicht abgewandelt werden. Wir tauschen `${VERSION_ID}` gegen `18.04` für die
korrekte Ubuntu Version auf der Linux Min 19.3 basiert. Außerdem müssen wir noch die zusätzlich _Dependency_
`slirp4netns` installieren, die für das _Networking_ benötigt wird. Nach den Anpassungen sehen die abgewandelten Kommandos wie
folgt aus:

```bash
sudo sh -c "echo 'deb http://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/xUbuntu_18.04/ /' > /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list"
wget -nv https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable/xUbuntu_18.04/Release.key -O- | sudo apt-key add -
sudo apt-get update -qq
sudo apt-get -qq -y install podman slirp4netns
```

Nach der Installation der Pakete kann die Podman-Installation gestest werden, indem der _hello-world_ Container mit dem Kommando `podman run hello-world` gestartet wird:

```bash
$ podman run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```

Viel Spaß bei der Verwendung von _podman_ unter Linux Mint.

---

- [Offizielles Podman 'Getting Started'](https://podman.io/getting-started/)
- [Offizielle Installationsanleitung von Podman](https://podman.io/getting-started/installation.html)
