# Maintainer: Alexey Ugnichev <alexey.ugnichev@gmail.com>
_pkgname=mass-effect-modder
pkgname=${_pkgname}-git 
pkgver=418.r1.0e80648
pkgrel=1
pkgdesc="MassEffectModder (MEM), a cross-platform utility to mod Mass Effect family of games."
arch=('x86_64')
url="https://github.com/MassEffectModder/MassEffectModder"
license=('GPL')
groups=()
depends=(
  'qt5-base'
)
makedepends=(
  'git'
)
provides=("${_pkgname}")
conflicts=("${_pkgname}")
replaces=()
backup=()
options=()
install=
source=(
  "${_pkgname}"::'git+https://github.com/MassEffectModder/MassEffectModder.git'
  'mass-effect-modder.desktop'  
)
noextract=()
md5sums=('SKIP'
         '132a540d3f2a5e0fdc37ab1b3720d481')

pkgver() {
  cd "${srcdir}/${_pkgname}"

  # Git, unannotated tags available
  printf "%s" "$(git describe --long --tags | sed 's/\([^-]*-\)g/r\1/;s/-/./g')"
}

build() {
  cd "${srcdir}/${_pkgname}"

  cd MassEffectModder

  qmake

  make
}

# TODO: check the check()
#check() {
# cd "${srcdir}/${_pkgname}"
  
#  cd MassEffectModder

# make -k check
#}

package() {
  cd "${srcdir}/${_pkgname}"
  
  install -d "${pkgdir}/usr/share/applications"
  install -m644 "${srcdir}/mass-effect-modder.desktop" \
    "${pkgdir}/usr/share/applications/mass-effect-modder.desktop"

  cd MassEffectModder

  # NB: not working as install targets are empty upstream (at least for now)
  #make DESTDIR="${pkgdir}/" install

  install -d "${pkgdir}/usr/bin"
  install ./MassEffectModder/MassEffectModder "${pkgdir}/usr/bin"

  install -d "${pkgdir}/usr/share/icons"
  install -m644 ./MassEffectModder/Resources/MEM.png "${pkgdir}/usr/share/icons/MassEffectModder.png"
}

