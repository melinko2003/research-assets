![OQS Image](../assets/oqs-banner-logo.png)
# Open Quantum Safe Library ( liboqs )
URL: https://github.com/open-quantum-safe/liboqs  
This implementation at this point seems fairly complete.  
  
## Language/Application Bindings
[Python3](https://github.com/open-quantum-safe/liboqs-python)  
[Java](https://github.com/open-quantum-safe/liboqs-java)  
[C++](https://github.com/open-quantum-safe/liboqs-cpp)  
[DotNet/C#](https://github.com/open-quantum-safe/liboqs-dotnet)  
[Rust](https://github.com/open-quantum-safe/liboqs-rust)  
[Thales eSecurity/goliboqs](https://github.com/thales-e-security/goliboqs)  
  
## OpenSSL 
[OpenSSL 1.X Engine](https://github.com/open-quantum-safe/oqs-engine)  
[OpenSSL 3.X Provider](https://github.com/open-quantum-safe/oqs-provider)  
  
# Requirements
Liboqs requires [ Ninja-build/ninja ](https://github.com/ninja-build/ninja/releases) version 1.1.1 is in bin.  
  
# HowTo run the Demo
We require [Vagrant](https://developer.hashicorp.com/vagrant/downloads) , [Virtualbox](https://www.virtualbox.org/wiki/Downloads) , and [vagrant-vbguest](https://github.com/dotless-de/vagrant-vbguest)  
  
Alt Method ( Highly Experimental ) / Parallels  
We require [Vagrant](https://developer.hashicorp.com/vagrant/downloads) , Parallels Desktop [Buisness](https://www.parallels.com/products/business/)/[Pro](https://www.parallels.com/products/desktop/pro/) , and [vagrant-parallels](https://parallels.github.io/vagrant-parallels/docs/installation/) 
  
## Vagrant Boiler Plate

In the Demo I'll use Vagrant paired with Parallels so in order to provision I'll use:
```
cd pqc
VAGRANT_VAGRANTFILE=usr/templates/vagrant/Vagrantfile vagrant up --provider=virtualbox
```
  
### Alt Parallels Method: 
You may have to install the plugin first: `vagrant plugin install vagrant-parallels`. Sadly Virtualbox is the better provider here.
```
cd pqc
VAGRANT_VAGRANTFILE=usr/templates/vagrant/Vagrantfile vagrant up --provider=parallels
```

This should just install AlmaLinux 9, gcc, and associated Libraries for Building the OQS Libraries that enable Quantum Algos.  
  
Once the build is complete, enter Vagrant:  
```
VAGRANT_VAGRANTFILE=usr/templates/vagrant/Vagrantfile vagrant ssh
```
I would recommend at this point just performing the following as root, to become root in Vagrant do: `sudo su -`. You shouldn't be prompted for a password. Once your root proceed to the next section.

## Standard Build Practice
OQS requires Ninja-Build to be installed to support cmake/installation/packaging. This Repo ships with a copy, and it should be accessible at: `/vagrant/bin/ninja`. Lets add it to the $PATH:
```
[root@alma9 ~]# export PATH="$PATH:/vagrant/bin/ninja"
[root@alma9 ~]# ninja --version                                              
1.11.1
```
I've prepared `build_latest_oqs.sh` that will `git clone` the liboqs to your home directory, install rpms, and python modules required. 
```
[root@alma9 ~]# ./vagrant/demo/build_latest_oqs.sh
```
When the `ninja install` command finishes it should install everything to `/opt/liboqs`. There are additional scripts in the [demo](../../demo) directory and for building other components. 

# Whats next?
Pick your implementation to test functionality.
  
## Openssl Implementation details
[Openssl 3.X via Providers](OQS-PROVIDER.md)  
[Openssl 1.1.X via compilation](OQS-STATIC-111.md)  
See: [etc](../../etc) folder for Openssl 1.1.1/3.X compatible Openssl Conf files for CA/x509 operations.  

## Demo Implementations by the Open Quantum Group
https://github.com/open-quantum-safe/oqs-demos