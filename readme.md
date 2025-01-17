# John the Ripper Packages

[![License](https://img.shields.io/badge/License-GPL%20v2-blue.svg)](https://github.com/openwall/john-packages/blob/master/LICENSE.txt)
![Donation](https://img.shields.io/badge/Donate-US%24%2010-brightgreen?style=flat&logo=github-sponsors)

[Openwall's](http://openwall.com/) John the Ripper (JtR) is a fast password cracker,
currently available for many flavors of Unix, Windows, DOS, and OpenVMS. Its primary
purpose is to detect weak Unix passwords. Besides several crypt(3) password hash
types most commonly found on various Unix systems, supported out of the box are
Windows LM hashes, plus lots of other hashes and ciphers.

# Table of Contents
1. [Introduction](#introduction)
   1. [Testing, Continuous Integration, and Continuous Delivery](#testing-and-continuous-integration)
   2. [Package Building Environments](#package-building-environments)
   3. [Packaging and Application Distribution](#packaging-and-application-distribution)
   4. [Releases Feed ![New Releases Feed](https://upload.wikimedia.org/wikipedia/en/thumb/4/43/Feed-icon.svg/16px-Feed-icon.svg.png)](https://github.com/openwall/john-packages/releases.atom)
2. [Snap Package](#snap)
3. [Flatpak Package](#flatpak)
4. [Windows Package](#windows)
5. [Docker Image](#docker-image)
6. [Checksums](#packages-checksums)
7. [Package Security](#security)
8. [Contribute](#contribute)
9. [License](#license)

# Introduction

### Testing and Continuous Integration
Click on the link to learn more about our [Continuous Integration and Continuous Delivery](https://github.com/openwall/john-packages/tree/master/tests#continuous-integration-and-continuous-delivery) procedures.

[![](https://mermaid.ink/img/eyJjb2RlIjoiZ3JhcGggVERcbiAgICBBW1Vwc3RyZWFtIENvbW1pdF0gLS0-fGNoZWNrIHN1aXRhYmlsaXR5fCBCKFJ1biBhIGRvd25zdHJlYW0gcmViYXNlIHRvIGdldCB0aGUgbGF0ZXN0IGNoYW5nZXMpXG4gICAgQiAtLT4gQ3tSdW4gaW48YnI-IFBhcmFsbGVsfVxuICAgIEMgLS0-fEFwcHZleW9yIENJfCBEW2ZhOmZhLWRlc2t0b3AgPGJyPldpbmRvd3NdXG4gICAgQyAtLT58Q2lyY2xlIENJfCBFW2ZhOmZhLWRlc2t0b3AgPGJyPkRvY2tlcl1cbiAgICBDIC0tPnxDaXJydXMgQ0l8IEZbZmE6ZmEtZGVza3RvcCA8YnI-RnJlZUJTRF1cbiAgICBDIC0tPnxBenVyZSBEZXZPUFN8IEhbZmE6ZmEtZGVza3RvcCA8YnI-RnV6emluZyBUZXN0PGJyPis8YnI-SW5zcGVjdCBEZXBsb3k8YnI-UGFja2FnZV1cbiAgICBIW2ZhOmZhLWRlc2t0b3AgPGJyPkZ1enppbmcgVGVzdDxicj4rPGJyPkluc3BlY3Rpb24gb2Y8YnI-IERlcGxveW1lbnQ8YnI-UGFja2FnZV0gLS0-fG1hbnVhbCBhcHByb3ZhbHwgWChBenVyZSBEZXBsb3lzPGJyPnRoZSBSZWxlYXNlKVxuICAgIEMgLS4uLT58RGVjb21taXNzaW9uZWR8IEdbZmE6ZmEtZGVza3RvcCA8YnI-VHJhdmlzQ0ldXG4iLCJtZXJtYWlkIjp7InRoZW1lIjoiZGVmYXVsdCJ9LCJ1cGRhdGVFZGl0b3IiOmZhbHNlLCJhdXRvU3luYyI6dHJ1ZSwidXBkYXRlRGlhZ3JhbSI6ZmFsc2V9)](tests#continuous-integration-and-continuous-delivery)

### Package Building Environments

Click on the link to learn more about our packages [Building Environments](https://github.com/openwall/john-packages/tree/master/deploy#deployments).

### Packaging and Application Distribution

[Snap](https://snapcraft.io/) and [Flatpak](https://flatpak.org/) are cool new ways
of distributing Linux applications among a wide range of different distros. They
are technologies to deploy applications in a secure, sandboxed and containerised way.

A [Docker](https://www.docker.com/) image is a read-only template used to execute code in a Docker container. An image is an immutable file that contains the binaries, configuration files, libraries, dependencies, tools, and other files needed for John the Ripper application to run.

When the Docker user runs an image, it becomes one instance (it becomes a container, in other words, a running instance of the application).

## Snap

> Delivered using Launchpad [ supports up to AVX512BW ]

[**A Snap**](https://snapcraft.io/) is a fancy zip file containing an application
together with its dependencies, and a description of how it should safely be run
on your system.

You can install JtR by following the instructions at
[https://snapcraft.io/john-the-ripper](https://snapcraft.io/john-the-ripper).

Terminal-based users should [enable snap support](https://docs.snapcraft.io/core/install),
then install JtR like this:

```bash
 sudo snap install john-the-ripper
```

John runs confined under a restrictive security sandbox by default. Nevertheless,
you can access and audit any file located in your home. Below, an usage example:

```bash
 john-the-ripper -list=build-info
 john-the-ripper -list=format-tests | cut -f3 > ~/alltests.in
 john-the-ripper -form=SHA512crypt ~/alltests.in
```

For your convenience, the snap installed on your system contains the file
`/snap/john-the-ripper/current/snap/manifest.yaml` which field `build_url`
points to its build log.

The highlights:

- fallback for CPU[*] and OMP;
- prince mode available;
- OpenCL available (GPU driver installation is needed);
- also available via the alias **john**, e.g. `john -list=build-info`;
- ~~the stable John 1.9.0 Jumbo 2:~~
  - ~~is available for X86_64, armhf, arm64, ppc64el, i386, and s390x;~~
- the stable John 1.9.0 Jumbo 1:
  - is available for X86_64, armhf, arm64, ppc64el, i386, powerpc, and s390x;
  - has regex mode available;
- a development version:
  - is available for X86_64, arm64, ppc64el, and s390x.

[*] John the Ripper runs using the best SIMD instructions available on the host
it's running on.

```Text
John the Ripper snap package achieved 7 thousand active users [*].
```

[*] 7 Day Active Users: the number of unique users who had at least one session within a 7 day period.

### Running a non-OpenMP build

In some situations a non-OpenMP build may be faster. You can ask to fallback to a
non-OpenMP build specifying `OMP_NUM_THREADS=1 john <options>` in the command line.
You avail the best SIMD instructions at one's disposal without any OpenMP stuff. E.g.:

```bash
OMP_NUM_THREADS=1 john --list=build-info
```

### Enabling Aliases

You are free to pick and set up aliases. To enable the usage of aliases with John
the Ripper snap, run `sudo snap alias john-the-ripper <alias>`. For example:

```bash
 sudo snap alias john-the-ripper my-john
 sudo snap alias john-the-ripper.dmg2john dmg2john
 sudo snap alias john-the-ripper.hccap2john hccap2john
 sudo snap alias john-the-ripper.racf2john racf2john
 sudo snap alias john-the-ripper.vncpcap2john vncpcap2john
 sudo snap alias john-the-ripper.zip2john zip2john
 sudo snap alias john-the-ripper.gpg2john gpg2john
 sudo snap alias john-the-ripper.keepass2john keepass2john
 sudo snap alias john-the-ripper.putty2john putty2john
 sudo snap alias john-the-ripper.rar2john rar2john
 sudo snap alias john-the-ripper.uaf2john uaf2john
 sudo snap alias john-the-ripper.wpapcap2john wpapcap2john
```

Once enabled, John itself plus the *2john tools can be invoked using the aliases.
In the example, to run John type `my-john`.

### Acessing OpenCL

As noted at https://forum.snapcraft.io/t/snaps-and-opencl/8509/17, the use of
OpenCL by snaps is a problem. Support for NVIDIA cards is under development.

As a "general" solution (or in the case of AMD hardware), the user can run john
out of the sandbox, unconfined (e.g., run `/snap/john-the-ripper/current/run/john`).

### Snap Deployments

If you followed the above instructions, you installed the stable version of John
the Ripper Jumbo in your system. If you want to access the hot and bleeding
developing version of JtR, you must follow a development channel. For a clean
installation:

```bash
 sudo snap install --channel=edge john-the-ripper
```

If you already has JtR installed:

```bash
 sudo snap refresh --channel=edge john-the-ripper
```

If you do so, you will be running the development version available on GitHub.

## Flatpak

> Delivered using FlatHub and GitLab CI [ supports up to AVX2 ]

[**Flatpak**](http://flatpak.org//) is a new framework for desktop applications
on Linux, built to be distribution agnostic and allow deployment on any Linux
operating system out there.

Flatpak is available for the [most common Linux distributions](http://flatpak.org/getting.html).

To install JtR, simply run:

```bash
 dnf install -y flatpak # or 'yum install', 'apt-get install', etc.
 flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo # flatpak repository
 flatpak install flathub com.openwall.John
```

~~You can install JtR by following the instructions at
[https://flathub.org/apps/details/com.openwall.John](https://flathub.org/apps/details/com.openwall.John).~~

John runs confined under a restrictive security sandbox by default. Nevertheless,
you can access and audit any file located in your home. Below, an usage example:

```bash
 flatpak run com.openwall.John -list=build-info
 flatpak run com.openwall.John -list=format-tests | cut -f3 > ~/alltests.in
 flatpak run com.openwall.John -form=SHA512crypt ~/alltests.in
```

The highlights:

- fallback for CPU[*] and OMP;
- prince mode available.
- ~~the stable John 1.9.0 Jumbo 2:~~
  - ~~is available for X86_64, arm, aarch64, and i386;~~
- the stable John 1.9.0 Jumbo 1:
  - is available for X86_64, arm, aarch64, and i386;
  - has regex mode available;
- a development version:
  - is available for X86_64.

[*] John the Ripper runs using the best SIMD instructions available on the host
it's running on.

### Flatpak Deployments

If you followed the above instructions, you installed the stable version of John
the Ripper Jumbo in your system. If you want to access the hot and bleeding
developing version of JtR, you must install a bundle.

John the Ripper single-file flatpak bundle was built and tested on
[GitLab](https://gitlab.com/claudioandre-br/JtR-CI/pipelines). You can get it
[here](https://github.com/openwall/john-packages/releases).

The necessary steps to install the package are listed below. They were tested on
a clean Fedora 29 docker image, but they should work for every supported distro
out there. Don't worry, it can't hurt your Linux environment.

Install and configure flatpak itself:

```bash
 dnf install -y flatpak # or 'yum install', 'apt-get install', etc.
 flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo # flatpak repository
 flatpak install -y flathub org.freedesktop.Platform//20.08 # install the runtime (base "container")
```

Navigate to where you downloaded the john.flatpak file. Now, let's install the
software:

```bash
 flatpak --user install --bundle john.flatpak # per-user installation (not system wide)
```

Run John the Ripper and check if it is working:

```bash
 flatpak run com.openwall.John
 flatpak run com.openwall.John --list=build-info
```

## Windows

> Delivered using Microsoft-hosted Windows 2016 Server in Azure [ supports up to AVX512BW ]

To install John the Ripper by downloading the .zip file and installing manually,
follow these steps:

- Download the ZIP file to your machine.
- Navigate to where you downloaded the file and double click the compressed file.
- Extract it to a directory such as `C:\john-the-ripper`.
- Start a command prompt.
- Navigate to the directory you extracted the .zip file, e.g., `cd C:\john-the-ripper\run`.
- Run JtR:

```powershell
C:\john-the-ripper\run>john --list=build-info
C:\john-the-ripper\run>john --test --format=SHA512crypt
```

The highlights:

- fallback for CPU[*] and OMP;
- prince mode available;
- OpenCL available (GPU driver installation is needed);
- generic crypt(3) format available;
- security feature Address Space Layout Randomisation (ASLR) enabled;
- security feature Data Execution Prevention (DEP) enabled;
- ~~the stable John 1.9.0 Jumbo 2:~~
  - ~~is available for X86_64 and i386;~~
- the stable John 1.9.0 Jumbo 1:
  - is available for X86_64 and i386;
- a development version:
  - is available for X86_64.

[*] John the Ripper runs using the best SIMD instructions available on the host
it's running on.

### Windows Deployments

The links below contain all the executables and libraries needed to run a fresh
John the Ripper installation.

- ~~the stable John 1.9.0 Jumbo 2:~~
  - ~~The [32bit version](https://github.com/claudioandre-br/packages/releases/download/1.9.0-jumbo-2/winX32_1_JtR.7z)
[(logs)](https://github.com/openwall/john-packages/blob/master/1.9.0.J2/x32_log.txt);~~
  - ~~The [64bit version](https://github.com/claudioandre-br/packages/releases/download/1.9.0-jumbo-2/winX64_1_JtR.7z)
[(logs)](https://github.com/openwall/john-packages/blob/master/1.9.0.J2/x64_log.txt);~~
- the stable John 1.9.0 Jumbo 1:
  - The [32bit version](https://github.com/claudioandre-br/packages/releases/download/1.9.0-jumbo-1/x32_win.zip)
[(logs)](https://github.com/openwall/john-packages/blob/master/1.9.0.J1/x32_log.txt);
  - The [64bit version](https://github.com/claudioandre-br/packages/releases/download/1.9.0-jumbo-1/x64_win.zip)
[(logs)](https://github.com/openwall/john-packages/blob/master/1.9.0.J1/x64_log.txt);
- a development [64bit version](https://github.com/openwall/john-packages/releases/tag/jumbo-dev).

Libs **may** be needed on some systems.

### Running a non-OpenMP build on Windows

In some situations a non-OpenMP build may be faster. You can ask to fallback to
a non-OpenMP build specifying the value of OMP_NUM_THREADS in the command line.
You avail the best SIMD instructions at one's disposal without any OpenMP stuff. E.g.:

```powershell
PS C:\john-the-ripper\run> set OMP_NUM_THREADS=1
PS C:\john-the-ripper\run> .\john --list=build-info
```

### Running OpenCL

Some adjustments may be necessary to allow John the Ripper detect your GPU
hardware. If you are facing problems, please ask for support.

- That being said, a few advices to anyone facing Windows problems:
  - replacing cygwin's OpenCL library `cygOpenCL-1.dll` in the `run` directory with `OpenCL.dll` installed
  in the `c:\Windows\System32` folder should make everything _almost_ work. Make a backup of `cygOpenCL-1.dll`, copy in the `OpenCL.dll`, and rename the copied file `cygOpenCL-1.dll`.
  - if you get errors like `Error building kernel /run/opencl/cryptsha512_kernel_GPU.cl` try running john from the subdirectory `opencl` (e.g. from `JtR\run\opencl` run `..\john.exe`).

Benchmarking:

```text
PS C:\bleeding\run> .\john --test=5 --format=sha512crypt-opencl
Device 0: Juniper [AMD Radeon HD 6700 Series]
Benchmarking: sha512crypt-opencl, crypt(3) $6$ (rounds=5000) [SHA512 OpenCL]... DONE
Speed for cost 1 (iteration count) of 5000
Raw:	11522 c/s real, 819200 c/s virtual
```

Real cracking:

```powershell
PS C:\bleeding\run> .\john --format=sha512crypt-opencl d:\hash.txt
Device 0: Juniper [AMD Radeon HD 6700 Series]
Using default input encoding: UTF-8
Loaded 2 password hashes with 2 different salts (sha512crypt-opencl, crypt(3) $6$ [SHA512 OpenCL])
Cost 1 (iteration count) is 5000 for all loaded hashes
Press 'q' or Ctrl-C to abort, almost any other key for status
                 (?)
1g 0:00:00:28  3/3 0.03540g/s 5553p/s 9178c/s 9178C/s 123456
```

```powershell
PS C:\bleeding\run> .\john --format=sha512crypt-opencl d:\hash.txt --mask=Hello?awor?l?l?a
Device 0: Juniper [AMD Radeon HD 6700 Series]
Using default input encoding: UTF-8
Loaded 2 password hashes with 2 different salts (sha512crypt-opencl, crypt(3) $6$ [SHA512 OpenCL])
Remaining 1 password hash
Cost 1 (iteration count) is 5000 for all loaded hashes
Press 'q' or Ctrl-C to abort, almost any other key for status
GPU 0 probably invalid temp reading (-1°C).
Hello world!     (?)
1g 0:00:05:06 DONE (2018-01-01 15:08) 0.003265g/s 11369p/s 11369c/s 11369C/s HelloYworik_..HelloLworurU
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```
## Docker Image

> Delivered using GitHub Actions [ supports up to AVX512BW ]

For testing and future reference, we have a Docker image of John the Ripper.
To use it:

```bash
 # CPU only formats
 docker run -it ghcr.io/openwall/john:v1.9.0J2 <binary id> <john options>

 # To run ztex formats
 docker run -it --device=/dev/ttyUSB0 ghcr.io/openwall/john:v1.9.0J1 ztex <john options>
```

Run John the Ripper and check if it is working:

```bash
 docker run -it ghcr.io/openwall/john:v1.9.0J2 # => SSE2
 docker run -it ghcr.io/openwall/john:v1.9.0J2 best # => uses the best SIMD available
 docker run -it ghcr.io/openwall/john:v1.9.0J2 ssse3-no-omp -list=build-info
 docker run -it ghcr.io/openwall/john:v1.9.0J2 avx512bw -test=0 -format=cpu
 docker run -it ghcr.io/openwall/john:v1.9.0J2 -list=format-tests | cut -f3 > ~/alltests.in
 docker run -it -v "$HOME":/host ghcr.io/openwall/john:v1.9.0J2 avx -form=SHA512crypt /host/alltests.in --max-run=300
```

Compare the performance of SIMD extensions:

```bash
 docker run -it ghcr.io/openwall/john:v1.9.0J2 sse2    --test=10 --format=SHA512crypt
 docker run -it ghcr.io/openwall/john:v1.9.0J2 sse4.1  --test=10 --format=SHA512crypt
 docker run -it ghcr.io/openwall/john:v1.9.0J2 avx     --test=10 --format=SHA512crypt
 docker run -it ghcr.io/openwall/john:v1.9.0J2 avx2    --test=10 --format=SHA512crypt
```

The highlights:

- prince mode available;
- ~~the stable John 1.9.0 Jumbo 2 (`ghcr.io/openwall/john:v1.9.0J2`):~~
  - ~~has auto-selection of the best SIMD if user specifies `best` as the `<binary id>`.~~
- the stable John 1.9.0 Jumbo 1 (`ghcr.io/openwall/john:v1.9.0J1`):
  - has ztex formats available.
- the development version (`ghcr.io/openwall/john:latest`):
  - has auto-selection of the best SIMD if user specifies `best` as the `<binary id>`.

The available binaries (their IDs are sse2, sse2-no-omp, ssse3, etc) are:

- /john/run/john-sse2 (default binary)
- /john/run/john-sse2-no-omp
- /john/run/john-ssse3
- /john/run/john-ssse3-no-omp
- /john/run/john-sse4.1
- /john/run/john-sse4.1-no-omp
- /john/run/john-sse4.2
- /john/run/john-sse4.2-no-omp
- /john/run/john-avx
- /john/run/john-avx-no-omp
- /john/run/john-xop
- /john/run/john-xop-no-omp
- /john/run/john-avx2
- /john/run/john-avx2-no-omp
- /john/run/john-avx512f
- /john/run/john-avx512f-no-omp
- /john/run/john-avx512bw
- /john/run/john-avx512bw-no-omp
- /john/run/john-ztex (SSE2)
- /john/run/john-ztex-no-omp (SSE2)

## Packages Checksums

> Released packages checksums computed by Build Servers

File verification is the process of using an algorithm for verifying the integrity
of a computer file. A popular approach is to store checksums (hashes) of files,
also known as message digests, for later comparison. All john packages checksums (hashes)
are computed by the CI servers.

Accessing the build logs, you can view the hashes of all relevant
files. For your convenience, we provide a file named checksum.txt containing the
checksums for all packages.

#### John the Ripper 1.9.0 Jumbo 2

~~The checksums are available in [this file](https://github.com/openwall/john-packages/blob/master/1.9.0.J2/checksum.txt).~~

#### John the Ripper 1.9.0 Jumbo 1

The checksums are available in [this file](https://github.com/openwall/john-packages/blob/master/1.9.0.J1/checksum.txt).

## Security

Please inspect all packages prior to running any of them to ensure safety.
We already know they're safe, but you should verify the security and contents of any
binary from the internet you are not familiar with.

We take security very seriously.

## Contribute

We love contributions in the form of issues and pull requests. [Read more here](CONTRIBUTING.md) before contributing.

## License

GNU General Public License v2.0
