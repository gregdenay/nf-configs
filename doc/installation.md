# General installation guides

First of, this is not a specific installation guide to any of the pipelines covered by this configuration repository. 

Instead, this guide will provide some hints how best to approach the general setup, depending on what operating system you are running on. The very basic explanation is that you need two components - the Nextflow pipeline engine and some way to have Nextflow stage the relevant software packages. Since this may require slightly different steps on different platforms, we discuss them separately below. 

[Linux](#linux)

[OSX](#osx)

[Windows](#windows-11)

## Linux

If you are running on Linux, things are generally "simple" (assuming you are comfortable administrating Linux, that is).

We are testing our pipelines on Alma Linux 9.4, but the basic principle should be transferrable to other systems. 

### Software provisioning

On Linux, you have access to basically all supported software provisioning frameworks also supported by Nextflow - including Conda and several container frameworks. These all have their pros and cons, but to keep things simple, we recommend you use Singularity. Singularity is a Docker-compatible container engine, is completely free and also happens to have a dedicated repository for all the otherwise Docker-native Bioconda containers we use in this pipeline (i.e. quick start up without need for conversion of container formats).

To install Singularity on your system, the easiest option is:

On a RHEL derivative, version 9(rpm).
```bash
wget https://github.com/sylabs/singularity/releases/download/v4.1.2/singularity-ce-4.1.2-1.el9.x86_64.rpm
sudo dnf -y install ./singularity-ce-4.1.2-1.el9.x86_64.rpm
```

On Ubuntu, version 22.04 (deb)
```bash
wget https://github.com/sylabs/singularity/releases/download/v4.1.2/singularity-ce_4.1.2-jammy_amd64.deb
sudo dpkg -i singularity-ce_4.1.2-jammy_amd64.deb
```

If you running different/older/newer releases or otherwise need more information on installing Singularity, please check the official [documentation](https://docs.sylabs.io/guides/3.11/admin-guide/installation.html). 

### Installing JRE

Nextflow requires The Java JRE (>= 11, <= 21):

On a RHEL derivative, version 9
```bash
sudo dnf -y install java-21-openjdk 
sudo alternatives --config java
```

On Ubuntu, version 22.04
```bash
sudo apt install openjdk-21-jdk
sudo update-alternatives --config java
```

Use the second command to set JRE21 as your sytems default. 

### Installing Nextflow

You can follow the instructions on the official Nextflow guide [here](https://www.nextflow.io/docs/latest/getstarted.html#installation).

A simple approach would be:
```bash
mkdir -p $HOME/bin
cd $HOME/bin
wget https://github.com/nextflow-io/nextflow/releases/download/v23.10.1/nextflow-23.10.1-all
mv nextflow-23.10.1-all nextflow
chmod +x nextflow
```
And you could also make sure that $HOME/bin is in $PATH by adding the directory to your bash profile:
```bash
echo "export PATH=$PATH:$HOME/bin" >> $HOME/.bash_profile
```

## OSX

The following guide was tested on OSX 14 (Sonoma) with an Intel-based Macbook Pro. 

### Software provisioning

On Mac, we recommend you install Docker instead of Conda or any of the other container frameworks; its the simplest approach with the least amount of incompatibilies.

Luckily, Docker has a detailed installation guide [here](https://docs.docker.com/desktop/install/mac-install/).

### Installing JRE

Nextflow requires The Java JRE (>= 11, <= 21). To be able to specifically install that, we first need SDKMAN

```bash
curl -s "https://get.sdkman.io" | bash
```

Simply follow the instructions on the screen and then source your bash profile to make the changes that immediate effect:

```bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
```

Next, install JRE 21:

```bash
sdk install java 21.ea.35-open
```

You can confirm that you have installed the correct version as follows:

```bash
java -version
```

### Installing Java

You can follow the instructions on the official Nextflow guide [here](https://www.nextflow.io/docs/latest/getstarted.html#installation).

A simple approach would be:
```bash
mkdir -p $HOME/bin
cd $HOME/bin
curl -O https://github.com/nextflow-io/nextflow/releases/download/v23.10.1/nextflow-23.10.1-all
mv nextflow-23.10.1-all nextflow
chmod +x nextflow
```
And you could also make sure that $HOME/bin is in $PATH by adding the directory to your bash profile:
```bash
echo "export PATH=$PATH:$HOME/bin" >> $HOME/.bash_profile
source $HOME/.bash_profile
```

## Windows 11

Coming soon.

