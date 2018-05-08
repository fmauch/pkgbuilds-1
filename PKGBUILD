# Previous Maintainer: Benjamin Chretien <chretien at lirmm dot fr>
# Maintainer: Gonçalo Camelo Neves Pereira <goncalo_pereira@outlook.pt>
pkgname=libdart
pkgver=6.4.0
pkgrel=2
pkgdesc="Dynamic Animation and Robotics Toolkit"
arch=('i686' 'x86_64')
url="http://dartsim.github.io"
license=('BSD')
depends=('assimp' 'boost' 'eigen>=3' 'fcl' 'flann' 'glut' 'libccd' 'libgl'
         'urdfdom')
optdepends=('bullet: Bullet support'
            'coin-or-ipopt: Ipopt support'
            'nlopt: NLopt support')
makedepends=('cmake' 'doxygen')
_name=dart
source=(https://github.com/dartsim/${_name}/archive/v${pkgver}.tar.gz)
sha256sums=('7a9e6e081d1cb910a7c9c996d76dd48ddca15b798c6d9a3cc7664534e5d28a84')

# Build type
_buildtype="Release"

# Build the project
build() {
  cd "${srcdir}/${_name}-${pkgver}"

  msg "Starting CMake (build type = ${_buildtype})"

  # Create a build directory
  mkdir -p "${srcdir}/${_name}-${pkgver}-build"
  cd "${srcdir}/${_name}-${pkgver}-build"

  # Run CMake in release
  cmake -DCMAKE_BUILD_TYPE="${_buildtype}" \
        -DCMAKE_INSTALL_PREFIX="/usr" \
        "${srcdir}/${_name}-${pkgver}"

  # Compile the library
  msg "Building the project"
  make
}

# Run unit tests
check() {
  msg "Running unit tests"
  cd "${srcdir}/${_name}-${pkgver}-build"
  make test
}

# Create the package
package() {
  # Install in /opt/roboptim
  cd "${srcdir}/${_name}-${pkgver}-build"

  msg "Installing files"
  make DESTDIR="${pkgdir}/" install
}
