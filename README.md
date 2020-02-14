The start of the attestation architecture. Builds a slimmed down version of the CakeML AM test suite in a CAmkES component, alongside a VM instance. 

This version of the AM does not have sockets, nor a proper RNG seed source. It also seems to struggle with cryptographic signatures. It's possible the library is trying to perform file IO, which CAmkES will respond to with a runtime error. 

Next on the agenda: re-implement the above functionality, and look at 'CakeML component <-> VM' communication.

## How to build

```sh
mkdir attarch
cd attarch
repo init -u https://github.com/gaj7/attarch-manifest.git
repo sync
mkdir build
cd build
../init-build.sh -DCAMKES_VM_APP=attarch -DPLATFORM=exynos5422
ninja
```

In addition to the regular seL4/CAmkES build requirements, this assumes you have the 32-bit architecture targeting CakeML compiler in you path under the name "cake32".
