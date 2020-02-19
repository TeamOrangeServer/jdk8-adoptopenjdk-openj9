# Maintainer: sousuke0422 <sousuke20xx@gmail.com>

# java-11-adoptopenjdk in aur
# Michael Lass <bevan@bi-co.net>

# This PKGBUILD heavily borrows from java-openjdk in [extra] maintained by:
# Levente Polyak <anthraxx[at]archlinux[dot]org>
# Guillaume ALAUX <guillaume@archlinux.org>

# This PKGBUILD is maintained on github:
# https://github.com/michaellass/AUR

#_majorver=8
#_minorver=0
#_securityver=6
#_updatever=242
#pkgrel=1
#pkgver=${_majorver}.${_minorver}.${_securityver}.u${_updatever}
#_tag_ver=${_majorver}.${_minorver}.${_securityver}+${_updatever}
_java_ver=8
_jdk_update=242
_jdk_build=08
_openj9=0.18.1
pkgrel=1
pkgver=${_java_ver}.u${_jdk_update}.b${_jdk_build}.openj9
_tag_ver=${_java_ver}u${_jdk_update}-b${_jdk_build}_openj9-${_openj9}
_tar_ver=${_java_ver}u${_jdk_update}b${_jdk_build}_openj9-${_openj9}

pkgname=jdk8-adoptopenjdk-openj9
pkgdesc="OpenJDK Java ${_java_ver} development kit (AdoptOpenJDK build)"
arch=('x86_64')
url='https://adoptopenjdk.net/'
license=('custom')

depends=('java-runtime-common>=3' 'ca-certificates-utils' 'desktop-file-utils' 'libxrender' 'libxtst' 'alsa-lib')
optdepends=('gtk2: for the Gtk+ 2 look and feel'
            'gtk3: for the Gtk+ 3 look and feel')
provides=("java-runtime-headless=${_java_ver}"
          "java-runtime-headless-openjdk=${_java_ver}"
          "jre${_java_ver}-openjdk-headless=${pkgver}"
          "jre-openjdk-headless=${pkgver}"
          "java-runtime=${_java_ver}"
          "java-runtime-openjdk=${_java_ver}"
          "jre${_java_ver}-openjdk=${pkgver}"
          "jre-openjdk=${pkgver}"
          "java-environment=${_java_ver}"
          "java-environment-openjdk=${_java_ver}"
          "jdk${_java_ver}-openjdk=${pkgver}"
          "jdk-openjdk=${pkgver}"
          "openjdk${_java_ver}-src=${pkgver}"
          "openjdk-src=${pkgver}")
backup=(etc/${pkgname}/jre/lib/net.properties
        etc/${pkgname}/jre/lib/logging.properties
        etc/${pkgname}/jre/lib/security/java.security
        etc/${pkgname}/jre/lib/security/policy/limited/exempt_local.policy
        etc/${pkgname}/jre/lib/security/policy/limited/default_US_export.policy
        etc/${pkgname}/jre/lib/security/policy/limited/default_local.policy
        etc/${pkgname}/jre/lib/security/policy/unlimited/default_US_export.policy
        etc/${pkgname}/jre/lib/security/unlimited/default_local.policy
        etc/${pkgname}/jre/lib/security/policy/README.txt
        etc/${pkgname}/jre/lib/security/java.policy
        etc/${pkgname}/jre/lib/management/management.properties
        etc/${pkgname}/jre/lib/management/jmxremote.access
        etc/${pkgname}/jre/lib/management/jmxremote.password.template
        etc/${pkgname}/jre/lib/sound.properties)
install=install_jdk8-adoptopenjdk-openj9.sh
#https://github.com/AdoptOpenJDK/openjdk8-binaries/releases/download/jdk8u242-b08_openj9-0.18.1/OpenJDK8U-jdk_x64_linux_openj9_8u242b08_openj9-0.18.1.tar.gz
source=(https://github.com/AdoptOpenJDK/openjdk${_java_ver}-binaries/releases/download/jdk${_tag_ver}/OpenJDK${_java_ver}U-jdk_x64_linux_openj9_${_tar_ver}.tar.gz
        freedesktop-java.desktop
        freedesktop-jconsole.desktop)
sha256sums=('ca785af638b24f9d4df896f5a9f557cc9f1e5fa5e2b1174d6b906e3fd5474c2e'
            '5792a4850b547d0caf0f8ecfb4b1639c1147586d65902269d0af1c1207198c6e'
            '248a8ccb26e9d6dba93258308e3122bc322a126df0413307ccdcea0d545b9a79')

_jvmdir=/usr/lib/jvm/java-${_java_ver}-adoptopenjdk-openj9
_jdkdir=jdk${_java_ver}u${_jdk_update}-b${_jdk_build}

package() {

  install -dm 755 "${pkgdir}${_jvmdir}"
  cp -a "${srcdir}/${_jdkdir}"/* "${pkgdir}${_jvmdir}"

  cd "${pkgdir}${_jvmdir}"

  # Conf
#  install -dm 755 "${pkgdir}/etc"
#  mv conf "${pkgdir}/etc/${pkgname}"
#  ln -sf /etc/${pkgname} conf

  # Legal
#  install -dm 755 "${pkgdir}/usr/share/licenses"
#  mv legal "${pkgdir}/usr/share/licenses/${pkgname}"
#  ln -sf /usr/share/licenses/${pkgname} legal

  # Man pages
  for f in man/man1/* man/ja/man1/* man/ja_JP.UTF-8/man1/*; do
    install -Dm 644 "${f}" "${pkgdir}/usr/share/${f/\.1/-adoptopenjdk-openj9${_java_ver}.1}"
  done
  rm -rf man
  ln -sf /usr/share/man man

  # Link JKS keystore from ca-certificates-utils
  rm -f jre/lib/security/cacerts
  ln -sf /etc/ssl/certs/java/cacerts jre/lib/security/cacerts

  # Desktop files
  for f in jconsole java; do
    install -Dm 644 \
      "${srcdir}/freedesktop-${f}.desktop" \
      "${pkgdir}/usr/share/applications/${f}-${pkgname}.desktop"
  done

}
