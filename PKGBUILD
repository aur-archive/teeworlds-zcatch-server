#Maintainer: andy123 <ajs @ online.de>

pkgname=teeworlds-zcatch-server
pkgver=0.4.5
_bamver=0.4.0
pkgrel=1
pkgdesc="A multiplayer 2D shooter's server mod"
arch=('i686' 'x86_64')
url="http://www.teeworlds.com/forum/viewtopic.php?id=7958"
license=('custom')
depends=('zlib')
makedepends=('python2')
source=(https://github.com/downloads/matricks/bam/bam-${_bamver}.tar.bz2
	https://github.com/Teetime/teeworlds/tarball/zCatch
        http://pixelbanane.de/yafu/3706005946/lightcatch.map
	http://pixelbanane.de/yafu/1746469715/ctf_nephtys.map
	http://pixelbanane.de/yafu/3266172569/juglecatch.map
	http://pixelbanane.de/yafu/2333573102/grasscatch.map
	http://pixelbanane.de/yafu/3832214070/dm1_catch.map
	rc.d)
sha1sums=('5dad113e38ba89384d842655eb477834285c216b'
	  '1c2f67aed9d5dd2c99d541869c465badade2f944'
          'de63eb6a7315439f4c080d4e6a504145bdd336f3'
          '6735f6b87164d79c8a133fbc1142255911d4a4df'
          '5c0f261f5c8649e122bb60905eb80a9c3078ef0a'
          '265b1985997517a8f94604fef39dda4eccb941cb'
          '8782e162aa5f9e32669191457410067fb3a64acb'
          '0efbeaa64746d1e06a99b6a8c5b100c45242bfa4')

build() {
	# Build bam (used to build teeworlds)
	# Now it is released separately I should make a separate package...
	cd ${srcdir}/bam-${_bamver}
	./make_unix.sh

	# Build zcatch
	cd ${srcdir}/Teetime-teeworlds-206e9ad
	# Use Python 2
	sed -i 's/python /python2 /' bam.lua

	../bam-${_bamver}/bam server_release
}

package() {
        mkdir -p ${pkgdir}/usr/share/${_name}/data/maps
	cp ${srcdir}/{ctf_nephtys.map,juglecatch.map,grasscatch.map,dm1_catch.map,lightcatch.map} ${pkgdir}/usr/share/${_name}/data/maps/
        
	install -Dm755 ${srcdir}/Teetime-teeworlds-206e9ad/zcatch_srv ${pkgdir}/usr/bin/$pkgname
        install -Dm644 ${srcdir}/Teetime-teeworlds-206e9ad/license.txt ${pkgdir}/usr/share/licenses/${pkgname}/license.txt
	install -Dm755 ${srcdir}/rc.d ${pkgdir}/etc/rc.d/$pkgname
}
