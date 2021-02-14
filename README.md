# docker-ecal
Inofficial Dockerfiles for [eCAL](https://github.com/continental/ecal).

Prebuilt docker images for *x86_64* and *armv7l* are available from [here](https://hub.docker.com/u/blutkoete).

Please note that the _ecal-base_ image install the prerequisites and then *clones* the full repository, the _ecal_ image then checkouts the requested tag, builds it and calls *make install*. You will probably get a much smaller and faster-to-rebuild image by using the official DEB images from the eCAL release page.

The _ecal-base-bionic_, _ecal-base-focal_ and _ecal-base-archlinux_ Dockerfiles use no ARGs.

The _ecal_ Dockerfile uses the following ARGs (--build-arg):

- *OS*: Used as the second part of the version to pull the _ecal-base_ image, e.g. _bionic_.
- *ARCH*: Used as the third part of the version to pull the _ecal-base_ image, e.g. _armv7l_.
- *TAG*: The eCAL repository tag to check out, e.g. _v5.8._.

The _ecal_base-archlinux-aur_ container pulls in the [AUR package](https://aur.archlinux.org/packages/ecal/) and is meant as a clean build environment for pushing new AUR package versions.

## Note on package managers
The _ecal_ image uses *make install* instead of the package manager of the base OS; this makes the Dockerfile easier, but is of course no clean way to provide a dependency if a dependent program or image relies on an installed Debian or Arch Linux package. In such cases, you will need to either install a dummy package yourself or call your package manager with the correct flag to make it assume a package as installed.
