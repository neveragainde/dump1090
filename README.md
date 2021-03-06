# dump1090-fa Debian/Raspbian packages

This is a fork of [dump1090-mutability](https://github.com/mutability/dump1090)
customized for use within [FlightAware](http://flightaware.com)'s
[PiAware](http://flightaware.com/adsb/piaware) software.

It is designed to build as a Debian package.

## Building under stretch

```bash
$ sudo apt-get install build-essential debhelper librtlsdr-dev pkg-config dh-systemd libncurses5-dev libbladerf-dev
$ dpkg-buildpackage -b
```

## Building under jessie

### Dependencies - bladeRF

You will need a build of libbladeRF. You can build packages from source:

```bash
$ git clone https://github.com/Nuand/bladeRF.git  
$ cd bladeRF  
$ git checkout 2017.12-rc1  
$ dpkg-buildpackage -b
```

Or Nuand has some build/install instructions including an Ubuntu PPA
at https://github.com/Nuand/bladeRF/wiki/Getting-Started:-Linux

Or FlightAware provides armhf packages as part of the piaware repository;
see https://flightaware.com/adsb/piaware/install

### Dependencies - rtlsdr

This is packaged with jessie. `sudo apt-get install librtlsdr-dev`

### Dependencies - HackRF

This is packaged with jessie. `sudo apt-get install libhackrf-dev`

### Dependencies - LimeSDR

You will need a build of [LimeSuite](https://github.com/myriadrf/LimeSuite).  
See detailed instruction on [the official Wiki](https://wiki.myriadrf.org/Lime_Suite) how to build and install it.

### Actually building it

Nothing special, just build it (`dpkg-buildpackage -b`)

## Building under wheezy

First run `prepare-wheezy-tree.sh`. This will create a package tree in
package-wheezy/. Build in there (`dpkg-buildpackage -b`)

The wheezy build does not include bladeRF, HackRF, or LimeSDR support.

## Building on FreeBSD

To build, you will need librtlsdr, pkgconf and GNU Make. For users of pkg(8):
`pkg install rtl-sdr pkgconf gmake`.

Then proceed by building with `gmake`.

## Building manually

You can probably just run "make" after installing the required dependencies.
Binaries are built in the source directory; you will need to arrange to
install them (and a method for starting them) yourself.

``make BLADERF=no`` will disable bladeRF support and remove the dependency on
libbladeRF.

``make RTLSDR=no`` will disable rtl-sdr support and remove the dependency on
librtlsdr.

``make HACKRF=no`` will disable HackRF support and remove the dependency on 
libhackrf.

``make LIMESDR=no`` will disable LimeSDR support and remove the dependency on
libLimeSuite.
