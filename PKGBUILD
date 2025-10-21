pkgname=spirv-llvm-translator
pkgver=21.1.1
pkgrel=2
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
    'git'
    'llvm'
    'ninja'
    'spirv-headers'
)
source=(git+ssh://git@github.com/KhronosGroup/SPIRV-LLVM-Translator#tag=v${pkgver})
sha256sums=(2fb81ad0fb976874fa7437834d5e2aba49b58208e0724b950e8e3415e43e92d8)

build() {
    cd SPIRV-LLVM-Translator

    local cmake_args=(
        -B flarebird-build
        -G Ninja
        -D CMAKE_BUILD_TYPE=Release
        -D CMAKE_INSTALL_PREFIX=/usr
        -D CMAKE_INSTALL_LIBDIR=lib64
        -D CMAKE_INSTALL_SYSCONFDIR=/etc
        -D CMAKE_POSITION_INDEPENDENT_CODE=ON
        -D CMAKE_SKIP_RPATH=ON
        -D LLVM_CONFIG=llvm-config
        -D LLVM_EXTERNAL_LIT=/usr/bin/lit
        -D LLVM_EXTERNAL_SPIRV_HEADERS_SOURCE_DIR=/usr/include/spirv
        -D LLVM_LIBDIR_SUFFIX=64
        -D LLVM_SPIRV_ENABLE_LIBSPIRV_DIS=ON
        -D LLVM_SPIRV_INCLUDE_TESTS=ON
        -D BUILD_SHARED_LIBS=ON
        -W no-dev
    )

    cmake "${cmake_args[@]}"

    cmake --build flarebird-build
}

package() {
    cd SPIRV-LLVM-Translator

    DESTDIR=${pkgdir} cmake --install flarebird-build
}
