# Kata Containers snap package

> **WARNING:**
>
> The Snap package method is **unmaintained** and only provides an old
> version of Kata Containers:
> The [latest Kata Containers snap](https://snapcraft.io/kata-containers)
> provides Kata Containers
> [version 2.4.2](https://github.com/kata-containers/kata-containers/releases/tag/2.4.2)
> but the latest stable Kata Containers release at the time of writing is
> [version 3.1.0](https://github.com/kata-containers/kata-containers/releases/tag/3.1.0).
>
> We recommend strongly that you switch to an alternative Kata Containers installation method.
>
> See: https://github.com/kata-containers/kata-containers/issues/6769
> for further details.

## Install Kata Containers

Kata Containers can be installed in any Linux distribution that supports
[snapd](https://docs.snapcraft.io/installing-snapd).

Run the following command to install **Kata Containers**:

> **WARNING:**
>
> The Snap package method is **unmaintained** and only provides an old
> version of Kata Containers:
> The [latest Kata Containers snap](https://snapcraft.io/kata-containers)
> provides Kata Containers
> [version 2.4.2](https://github.com/kata-containers/kata-containers/releases/tag/2.4.2)
> but the latest stable Kata Containers release at the time of writing is
> [version 3.1.0](https://github.com/kata-containers/kata-containers/releases/tag/3.1.0).
>
> We recommend strongly that you switch to an alternative Kata Containers installation method.
>
> See: https://github.com/kata-containers/kata-containers/issues/6769
> for further details.

```sh
$ sudo snap install kata-containers --stable --classic
```

## Configure Kata Containers

By default Kata Containers snap image is mounted at `/snap/kata-containers` as a
read-only file system, therefore default configuration file can not be edited.
Fortunately Kata Containers supports loading a configuration file from another
path than the default.

```sh
$ sudo mkdir -p /etc/kata-containers
$ sudo cp /snap/kata-containers/current/usr/share/defaults/kata-containers/configuration.toml /etc/kata-containers/
$ $EDITOR /etc/kata-containers/configuration.toml
```

## Integration with shim v2 Container Engines

The Container engine daemon (`cri-o`, `containerd`, etc) needs to be able to find the
`containerd-shim-kata-v2` binary to allow Kata Containers to be created.
Run the following command to create a symbolic link to the shim v2 binary.

```sh
$ sudo ln -sf /snap/kata-containers/current/usr/bin/containerd-shim-kata-v2 /usr/local/bin/containerd-shim-kata-v2
```

Once the symbolic link has been created and the engine daemon configured, `io.containerd.kata.v2`
can be used as runtime.

Read the following documents to know how to run Kata Containers 2.x with `containerd`.

* [How to use Kata Containers and Containerd](../how-to/containerd-kata.md)
* [Install Kata Containers with containerd](./container-manager/containerd/containerd-install.md)


## Remove Kata Containers snap package

Run the following command to remove the Kata Containers snap:

```sh
$ sudo snap remove kata-containers
```
