=== Build a new version ===

To avoid an excessive spam in the git log from upstream, I have used
import-orig with the istio upstream sources. For the moment the process
of importing a new release is a bit manual:

* Download the tar.gz source release from https://github.com/RadeonOpenCompute/k8s-device-plugin/releases
  (sadly no shasum for the src package provided).
* Run something like `gbp import-orig --pristine-tar k8s-device-plugin-1.25.2.3.tar.gz`
  to import the new version.
* Push the new version and the tags to the amd-k8s-device-plugin repo (upstream and master branches).
* Change the debian configuration (changelog, patches, etc..) and send a code review.
* Build with: `BACKPORTS=yes https_proxy=http://webproxy.eqiad.wmnet:8080 GIT_PBUILDER_AUTOCONF=no ARCH=amd64 DIST=bullseye-wikimedia gbp buildpackage -j4 -sa -us -uc --git-builder=git-pbuilder --git-color=on`
