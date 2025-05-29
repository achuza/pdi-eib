# pdi-eib
The following process will allow you to complie an image for future use. 

## Download the ISO image
Download the SL Micro image from SUSE Customer Center as an ISO. Place this file within the 'base-images' folder.

## Podman Setup
### Install podman
#### Debian/Ubuntu
```bash
sudo apt-get install -y podman
```
#### openSUSE
```bash
sudo zypper in -y podman
```

#### Homebrew on MacBook
```bash
brew install podman
```

## Initialize Podman
<pre>
podman machine init --cpus 6 --memory 4096'
podman machine start
podman pull registry.suse.com/edge/3.2/edge-image-builder:1.1.0
</pre>

## Run EIB
### Clone git repo

```bash
git clone https://github.com/achuza/pdi-eib.git
```

### Set environment variable
cd to the root of the EIB directory and run the following. 

```bash
EIB_DIR=$(pwd)
```

### Build Image
```bash
podman run --privileged --rm -it -v $EIB_DIR:/eib  registry.suse.com/edge/3.2/edge-image-builder:1.1.0  build --definition-file eib-config.yaml'
```