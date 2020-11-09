# Maintainer: Evan Anderson <evananderson@thelinuxman.us>
# Former maintainer: David Manouchehri <david@davidmanouchehri.com>
# Former maintainer: BxS <bxsbxs at gmail dot com>

pkgname=microchip-mplabc18-bin
pkgver=3.47
pkgrel=2.1
pkgdesc="C compiler for PIC18 MCUs"
arch=(x86_64)
url=http://www.microchip.com/c18
license=(custom)
[[ $CARCH = x86_64 ]] && depends=(lib32-gcc-libs)
makedepends=(lib32-tclkit)

provides=('mplabc18' 'microchip-mplabc18_bin')
conflicts=('mplabc18' 'microchip-mplabc18_bin')

options=(!strip docs libtool emptydirs !zipman staticlibs)

install=$pkgname.install
instdir=opt/microchip/mplabc18/v$pkgver
installer=mplabc18-v$pkgver-linux-lite-installer.run
source=("https://github.com/Manouchehri/Microchip-C18-Lite/releases/download/v$pkgver/mplabc18-v$pkgver-linux-lite-installer.run" "bitrock-unpacker.tcl")

md5sums=('1b79f6a55215fb2b1608e97f30bdc095'
         '70dedba4c417f8c0bb07c32d19e9d197')

build() {
  msg2 "Unpacking files from Microchip's installer blob"
  ./bitrock-unpacker.tcl ./$installer ./unpacked.vfs
}

package() {
  msg2 "Creating the package"
  cd $pkgdir
  mkdir -p "$pkgdir/$instdir/etc"
  chmod 0755 $srcdir/$installer

  msg2 "Copy files to package"
  cp -r $srcdir/unpacked.vfs/default/programfileslinux/* $pkgdir/$instdir

  msg2 "Setup profile.d"
  mkdir -p "$pkgdir/etc/profile.d"
  echo "export PATH=\"\$PATH\":'/$instdir/bin'" > "$pkgdir/etc/profile.d/$pkgname.sh"
  echo "export C18_TOOLCHAIN_ROOT='/$instdir'" >> "$pkgdir/etc/profile.d/$pkgname.sh"
  cat "$pkgdir/etc/profile.d/$pkgname.sh"

  msg2 "Add symlink to license file"
  mkdir -p "$pkgdir/usr/share/licenses/$pkgname"
  ln -s "/$instdir/MPLABC18CompilerLicense.txt" "$pkgdir/usr/share/licenses/$pkgname/LICENSE"
	
  msg2 "Setup access right"
  chmod +x "$pkgdir/$instdir/bin/_mplink"
  chmod +x "$pkgdir/$instdir/bin/mp2cod"
  chmod +x "$pkgdir/$instdir/bin/mp2hex"
  chmod +x "$pkgdir/$instdir/bin/mplink"
  chmod +x "$pkgdir/$instdir/bin/mplib"
  chmod +x "$pkgdir/$instdir/bin/cpp18"
  chmod +x "$pkgdir/$instdir/bin/mcc18"
  chmod +x "$pkgdir/$instdir/bin/mcc18-traditional"
  chmod +x "$pkgdir/$instdir/bin/mcc18-extended"

}

