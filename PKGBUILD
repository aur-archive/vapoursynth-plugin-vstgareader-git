# Maintainer:  Gustavo Alvarez <sl1pkn07@gmail.com>

_plug=vstgareader
pkgname=vapoursynth-plugin-${_plug}-git
pkgver=20121228
pkgrel=1
pkgdesc="Plugin for Vapoursynth: ${_plug} (GIT version)"
arch=('i686' 'x86_64')
url="https://github.com/chikuzen/${_plug}"
license=('LGPL2.1')
depends=('vapoursynth')
provides=("vapoursynth-plugin-${_plug}")
conflicts=("vapoursynth-plugin-${_plug}")
makedepends=('git')

_gitroot="git://github.com/chikuzen/${_plug}.git"
_gitname="${_plug}"

build() {
  cd "${srcdir}"

  msg "Connecting to GIT server..."

  if [ -d "${_gitname}" ] ; then
    cd "${_gitname}" && git pull --depth=1
  else
    git clone --depth=1 "${_gitroot}" "${_gitname}"
  fi

  cd "${srcdir}"

  msg "GIT checkout done or server timeout"
  msg "Starting make..."

  rm -fr "${_gitname}-build"
  cp -R "${_gitname}" "${_gitname}-build"
  cd "${_gitname}-build"

  ./configure
  make
}

package(){
    cd "${srcdir}/${_gitname}-build"
    install -Dm775 "lib${_plug}.so" "${pkgdir}/usr/lib/vapoursynth/lib${_plug}.so"
    install -Dm664 readme.rst "${pkgdir}/usr/share/doc/vapoursynth/plugins/${_plug}/README"
}

