# docker-ecal
Inofficial Dockerfiles for [eCAL](https://github.com/continental/ecal).

Prebuilt docker images are available from [here](https://hub.docker.com/u/blutkoete).

Please note that the _ecal-base_ image install the prerequisites and then *clones* the full repository, the _ecal_ image then checkouts the requested tag, builds it and install the resulting DEB package. You will probably get a much smaller and faster-to-rebuild image by using the official DEB images from the eCAL release page.

The _ecal-base-bionic_ and _ecal-base-focal_ Dockerfiles use no ARGs.

The _ecal_ Dockerfile uses the following ARGs (--build-arg):

- *OS*: Used as the second part of the version to pull the _ecal-base_ image, e.g. _bionic_.
- *ARCH*: Used as the third part of the version to pull the _ecal-base_ image, e.g. _arm_.
- *TAG*: The eCAL repository tag to check out, e.g. _v5.7.1_.
