# Maintainer: Twilight0 <https://github.com/Twilight0>
pkgname=nouveau-dkms
pkgver=2.2.3
pkgrel=1
pkgdesc="Unified Nouveau out-of-tree module with Fermi core, shader, and DDR3 memory reclocking (DKMS)"
arch=('x86_64')
url="https://github.com/Twilight0/nouveau-dkms"
license=('GPL-2.0-only')
depends=('dkms')
optdepends=('nouveau-utils: dynamic clock governor daemon, CLI management tool, and interactive TUI')
provides=('nouveau-dkms')
conflicts=('nouveau-fermi-reclock-dkms' 'nouveau-fermi-reclock-cachyos-lts-v2')
replaces=('nouveau-fermi-reclock-dkms')
source=(
  "nouveau-source.tar.gz::https://github.com/Twilight0/nouveau-dkms/releases/download/v2.1.0/nouveau-source.tar.gz"
  "nouveau.patch"
  "dkms.conf"
  "nouveau.conf"
)
sha256sums=('07ed99d8a366ae0f906af52dda33857f4c27135151bc505918d4c9c908c03ce5'
            'ee4d2889064f4a9d9bad111cda5f5b6fff27ca7c6e81f6362fc19ff9dcb7e9ff'
            '7f0d3d86a1551d4f1775d6dea33568f04d59dbf38faa7e9d50c0b327cfc327a6'
            '326efac21bf858f7be0e41b21f2c585bfd1ef5b18dad9cce022685a4623bb090')

prepare() {
  msg2 "Applying Fermi reclocking and 120Hz display patches..."
  patch -Np1 -d "${srcdir}/nouveau-source" < "${srcdir}/nouveau.patch"

  # Replace @PKGVER@ in dkms.conf
  sed "s/@PKGVER@/${pkgver}/g" -i "${srcdir}/dkms.conf"
}

package() {
  local destdir="${pkgdir}/usr/src/${pkgname}-${pkgver}"
  install -d "${destdir}"
  
  # Copy pre-patched sources directly to the DKMS build directory
  cp -r "${srcdir}/nouveau-source/"* "${destdir}/"
  
  # Install dkms.conf
  install -Dm644 "${srcdir}/dkms.conf" "${destdir}/dkms.conf"

  # Install default modprobe configuration
  install -Dm644 "${srcdir}/nouveau.conf" "${pkgdir}/usr/lib/modprobe.d/nouveau.conf"
}
