# Maintainer: zer0def <zer0def@github>
# Contributor: krevedko <krevedko@aur>
pkgname=docker-registry2
pkgver=2.7.1
pkgrel=1
pkgdesc='Docker Registry 2.0 implementation to pack, ship, store, and deliver docker images'
arch=('i686' 'x86_64' 'aarch64' 'armv7h' 'armv6h' 'arm')
url='https://github.com/docker/distribution'
license=('Apache:2.0')
makedepends=('git' 'go')
install=docker-registry.install
provides=('docker-registry')
conflicts=('docker-registry')
source=(
  "git+https://github.com/docker/distribution#tag=v${pkgver}"
  'docker-registry.conf'
  'docker-registry.service'
  'docker-registry.sysusers'
)
sha512sums=(
  'SKIP'
  '2018ba2c9c4f53bdcfef1cb766e99135a0484881c2666e0ddcd5e6ef87f8fb202403c86778544a45c764c9296c7a0aaf6bbbb2b15c931a1784a004dc4621ae93'
  'a88aa4f461a712b14a8c02774e341f27dd179ccd9f1f9d32ca06fc16048c1a8bc044022a77da13c682580ee265f3f6a2207211cbaec7800989af1fd243664d29'
  '087a1e67565ddd120bb2ca5648b941f3f5a096c4dbb6d826ac64439ed6e7940b132a8e79a33506ac1a0a226eb6b30f0d26f1587b45f4881cafb65b0121f4511b'
)
b2sums=(
  'SKIP'
  '81ddd2405c000c5d7a074a405dda5b31a6c3bb6beb2bc9d2e267b9f94472eb925467638a2d59dd23a53a4e78d2782c7f51f7dbb0fff6becf34127cf9138a470c'
  '4d73e86466ef8d0e1faf49861c0b8deda0c85530a97b187067dee45112f9833929015db1c05c9ae3ec356f33a3710d0583a3aa75c25abaa74f3e2d2468aabb07'
  '75a1eecf2aa511885450a93ff78b1b73897d88c46123a4ca35de18f5350c33b59afad74a055c4089f2c6f9bcb72ad59956482a0cba3afa2ed088242870c756f2'
)

build() {
  export GOPATH="${srcdir}"
  cd "${srcdir}/distribution"
  go get -v -d
  make
}

package() {
  install -dm755 "${pkgdir}/etc/docker-registry"
  sed -e 's@/var/lib/registry@/var/lib/docker-registry@g' \
      -e 's@/etc/registry@/etc/docker-registry/.htpasswd@' \
      "${srcdir}/distribution/cmd/registry/config-example.yml" > "${pkgdir}/etc/docker-registry/config.yml"

  install -Dm755 "${srcdir}/distribution/bin/registry" "${pkgdir}/usr/bin/docker-registry"
  install -Dm644 "${srcdir}/docker-registry.conf" "${pkgdir}/etc/conf.d/docker-registry"
  install -Dm644 "${srcdir}/docker-registry.service" "${pkgdir}/usr/lib/systemd/system/docker-registry.service"
  install -Dm644 "${srcdir}/docker-registry.sysusers" "${pkgdir}/usr/lib/sysusers.d/docker-registry.conf"
}
