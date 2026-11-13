# gdcm for Haiku

The [Haiku](https://www.haiku-os.org/) package of [gdcm](https://github.com/malaterre/GDCM) 3.2.7, which
[XarQ](https://xarq.org) uses to open DICOM medical images (.dcm). HaikuPorts doesn't have it, so we build it
and publish it in XarQ's own package repository.

## Install

Add the XarQ repository once, then install it like any other package:

```
pkgman add-repo https://xarq.org/haiku/x86_64/current
pkgman install gdcm
```

For development, install `gdcm_devel` too. The packages are built on Haiku R1/beta6
(x86_64) and also work on newer nightlies.

## What's here

`sci-libs/gdcm/` is a HaikuPorts recipe and its patches, in the same layout as the
[haikuports](https://github.com/haikuports/haikuports) tree. The patch makes GDCM build on Haiku: byte swapping uses GCC's built-ins, file offsets use Haiku's 64-bit off_t, and the bundled socket++ skips the socket constants Haiku doesn't have (the few calls that need them report "not supported").

To build it yourself, copy that folder into your haikuports tree and run:

```
haikuporter -S --get-dependencies gdcm
```

Set `VENDOR="XarQ"` in `haikuports.conf` first if the package is going into the XarQ
repository: Haiku's repository tool only accepts packages whose vendor matches the
repository's.

## Releases

Each release has the built `.hpkg` files. The XarQ repository at
https://xarq.org/haiku picks them up automatically, through the workflow in
[XarQ-design/xarq](https://github.com/XarQ-design/xarq/blob/main/.github/workflows/haiku-repo.yml).

## Licence

gdcm is under the BSD 3-clause licence; see the upstream project. The recipe is under the MIT
licence, like the HaikuPorts tree, and any patch is under gdcm's own licence.
