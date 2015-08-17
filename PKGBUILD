
pkgdesc="ROS - Navigation related tutorials."
url='http://www.ros.org/'

pkgname='ros-hydro-navigation-tutorials'
pkgver='0.2.0'
arch=('i686' 'x86_64')
pkgrel=1
license=('BSD')
makedepends=('cmake' 'ros-build-tools')

ros_depends=(ros-hydro-odometry-publisher-tutorial
  ros-hydro-navigation-stage
  ros-hydro-robot-setup-tf-tutorial
  ros-hydro-laser-scan-publisher-tutorial
  ros-hydro-roomba-stage
  ros-hydro-point-cloud-publisher-tutorial
  ros-hydro-simple-navigation-goals-tutorial)
depends=(${ros_depends[@]})

_tag=release/hydro/navigation_tutorials/${pkgver}-0
_dir=navigation_tutorials
source=("${_dir}"::"git+https://github.com/ros-gbp/navigation_tutorials-release.git"#tag=${_tag})
md5sums=('SKIP')

build() {
  # Use ROS environment variables
  /usr/share/ros-build-tools/clear-ros-env.sh
  [ -f /opt/ros/hydro/setup.bash ] && source /opt/ros/hydro/setup.bash

  # Create build directory
  [ -d ${srcdir}/build ] || mkdir ${srcdir}/build
  cd ${srcdir}/build

  # Fix Python3 error
  /usr/share/ros-build-tools/fix-python-scripts.sh ${srcdir}/${_dir}

  cmake ${srcdir}/${_dir} \
        -DCMAKE_BUILD_TYPE=Release \
        -DCATKIN_BUILD_BINARY_PACKAGE=ON \
        -DCMAKE_INSTALL_PREFIX=/opt/ros/hydro \
        -DPYTHON_EXECUTABLE=/usr/bin/python2 \
        -DPYTHON_INCLUDE_DIR=/usr/include/python2.7 \
        -DPYTHON_LIBRARY=/usr/lib/libpython2.7.so \
        -DSETUPTOOLS_DEB_LAYOUT=OFF
  make
}

package() {
  cd "${srcdir}/build"
  make DESTDIR="${pkgdir}/" install
}
