The start of the attestation architecture. Right now, it's just a silly "Hello World!" CakeML component running alongside a linux VM. The next step is to replace the current CakeML component with a slimmed down version of the real AM. The challenge here is maintaining a single AM codebase that can drop into the CAmkES build process, or build a standalone linux executable.

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

In addition to the regular seL4/CAmkES build requirements, this assumes you have the 64-bit architecture targeting CakeML compiler in you path under the name "cake64".
