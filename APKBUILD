# Reference: <https://postmarketos.org/vendorkernel>
# Kernel config based on: arch/arm64/configs/(CHANGEME!)

maintainer="LwkRenCup <dortappo@gmail.com>"
pkgname=linux-samsung-gts4lv
pkgver=4.9.337
pkgrel=0
pkgdesc="Samsung Galaxy Tab s5e LTE kernel fork"
arch="aarch64"
_carch="arm64"
_flavor="samsung-gts4lv"
url="https://kernel.org"
license="GPL-2.0-only"
options="!strip !check !tracedeps pmb:cross-native"
makedepends="
    bash
    bc
    bison
    devicepkg-dev
    findutils
    flex
    openssl-dev
    perl
    gcc-armv7
"

# Source
_repository="android_kernel_samsung_sdm670"
_commit="a30605a54f3b92627d868f169c72ef9c6ef82123"
_config="config-$_flavor.$arch"
source="
    $pkgname-$_commit.tar.gz::https://github.com/LineageOS/$_repository/archive/$_commit.tar.gz
    $_config
"
builddir="$srcdir/$_repository-$_commit"
_outdir="out"

prepare() {
    default_prepare
    . downstreamkernel_prepare
}

build() {
    unset LDFLAGS

    # 32-bit compat/vDSO toolchain for Samsung/Qualcomm 4.9
    export CROSS_COMPILE_ARM32=armv7-alpine-linux-musleabihf-

    make O="$_outdir" ARCH="$_carch" CC="${CC:-gcc}" \
        KBUILD_BUILD_VERSION="$((pkgrel + 1 ))-postmarketOS"
}

package() {
    downstreamkernel_package "$builddir" "$pkgdir" "$_carch" \
        "$_flavor" "$_outdir"

    install -Dm644 "$srcdir"/sdm670-gts4lv.dtb \
        "$pkgdir"/boot/dtbs/qcom/sdm670-gts4lv.dtb
}

sha512sums="
a545843310cd91d0b646c551a6c61391f2b29525734c0b7c82c761e700abd2fbe562499a985721f78bc85cdaac5e0f1655e2be53ad110737ae3bb22235216827  linux-samsung-gts4lv-a30605a54f3b92627d868f169c72ef9c6ef82123.tar.gz
3b19c95c645739968c6b05def41bbcf0cf339f6023c436f1425cd2ca852d253214b36626fa7954e0b50f2d3fab50d23eea279dcc6ee794c06bb149d8f985a8e0  config-samsung-gts4lv.aarch64
"
