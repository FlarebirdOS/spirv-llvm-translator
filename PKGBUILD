pkgname=spirv-llvm-translator
pkgver=21.1.0
pkgrel=1
pkgdesc="Tool and a library for bi-directional translation between SPIR-V and LLVM IR"
arch=('x86_64')
url="https://github.com/KhronosGroup/SPIRV-LLVM-Translator"
license=('LicenseRef-custom')
depends=(
    'gcc-libs'
    'glibc'
    'llvm-libs'
    'spirv-tools'
)
makedepends=(
    'cmake'
    'llvm'
    'ninja'
    'spirv-headers'
)
source=(https://github.com/KhronosGroup/SPIRV-LLVM-Translator/archive/v${pkgver}/SPIRV-LLVM-Translator-${pkgver}.tar.gz)
sha256sums=(4f7019a06c731daebbc18080db338964002493ead4cfb440fef95d120c50a170)

build() {
    cd SPIRV-LLVM-Translator-${pkgver}

    local cmake_args=(
        -B flarebird-build
        -G Ninja
        -D CMAKE_BUILD_TYPE=Release
        -D CMAKE_INSTALL_PREFIX=/usr
        -D CMAKE_INSTALL_LIBDIR=lib64
        -D BUILD_SHARED_LIBS=ON
        -D CMAKE_SKIP_INSTALL_RPATH=ON
        -D LLVM_EXTERNAL_SPIRV_HEADERS_SOURCE_DIR=/usr
        -D CMAKE_POSITION_INDEPENDENT_CODE=ON
        -D CMAKE_SKIP_RPATH=ON
        -D LLVM_INCLUDE_TESTS=ON
        -D LLVM_EXTERNAL_LIT=/usr/bin/lit
        -W no-dev
    )

    cmake "${cmake_args[@]}"

    cmake --build flarebird-build
}

package() {
    cd SPIRV-LLVM-Translator-${pkgver}

    DESTDIR=${pkgdir} cmake --install flarebird-build
}
