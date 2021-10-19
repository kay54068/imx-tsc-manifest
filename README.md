Use Custom repo sdk
====

Repository information about this:

- firmware-imx
- imx-atf
- imx-mkimage
- linux-imx
- uboot-imx
- build ()

## Step 0. preSteup host packages

## Install host packages 

```bash=
sudo apt-get install gawk wget git-core diffstat unzip texinfo gcc-multilib \
build-essential chrpath socat cpio python python3 python3-pip python3-pexpect \
xz-utils debianutils iputils-ping python3-git python3-jinja2 libegl1-mesa libsdl1.2-dev \
pylint3 xterm rsync curl libncursesw5-dev libncurses5-dev libssl-dev
```

## Setting up the repo utility

- Create a bin folder in the home directory.

```bash=
mkdir ~/bin
curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
chmod a+x ~/bin/repo
```
- Add the following line to the .bashrc file to ensure that the ~/bin folder is in your PATH variable.

```bash=
export PATH=~/bin:$PATH > ~/.bashrc
source ~/.bashrc
```

## Step 1. Clone Repository with repo utility


```shell=
repo init -uhttps://github.com/kay54068/imx-tsc-manifest.git -b imx-tsc-5.10.52-2.1.0 -m imx-tsc-5.10.52-2.1.0.xml
repo sync
```

## Step 2. install toolchain

```
cd imx-toolchain
chmod a+x fsl-imx-xwayland-glibc-x86_64-imx-image-core-cortexa53-crypto-imx8mp-lpddr4-evk-toolchain-5.10-hardknott.sh
```

> Default install to opt/ , you can change it.



## Step 3. Start the Build virtual environment form script

```
source /opt/fsl-imx-xwayland/5.10-hardknott/environment-setup-cortexa53-crypto-poky-linux
```


> [Restarting a build environment]  
> If a new terminal window is opened or the machine is rebooted after a build directory is set up, the setup environment script should  
> be used to set up the environment variables and run a build again.  



🎉 Now you can to build your application from build environment..


##  build u-boot source code


###  run make_uboot.sh script to build


```shell=
## Change the build directory
cd build
```

```shell=
## make config 
./make_uboot.sh config imx8mp_evk_defconfig

## make 
./make_uboot.sh build

## make menuconfig 
./make_uboot.sh menuconfig

## save config 
./make_uboot.sh saveconfig imx8mp_evk_defconfig

```


more detail can use the ./make_uboot.sh script

```shell=
./make_uboot.sh -h
```

### Required files path：

```
tools/mkimage
spl/u-boot-spl.bin
u-boot-nodtb.bin
arch/arm/dts/imx8mm-ddr4-evk.dtb
```

> You can change the binary file (*bin,*dtb) form target device


##  Build linux kernel from source code


```shell=
## Change the build directory
cd build
```

```shell=
## make config 
./make_linux.sh config imx_v8_defconfig

## make 
./make_linux.sh build

## make menuconfig 
./make_linux.sh menuconfig

## save config 
./make_linux.sh saveconfig imx_v8_defconfig
```


more detail can use the ./make_linux.sh script

```shell=
./make_linux.sh -h
```

### Required files path：

```shell=
## device tree binary
arch/arm64/boot/dts/freescale/*imx8mp*.dtb
## Kernal image
arch/arm64/boot/Image
```

> You can change the binary file (Image,*dtb) form target device

