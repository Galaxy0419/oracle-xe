# Maintainer: Maxim Kurnosenko <asusx2@mail.ru>
# Co-Maintainer: William Tang <ttan0037@student.monash.edu>
# Contributor: RonaldMcDaddy <wannes.demeyer@protonmail.com>
# Contributor: Tinh Truong <xuantinh at gmail dot com>
# Contributor: Cedric Sougne <cedric@sougne.name>
# Contributor: untseac
# Contributor: siasia
# Contributor: Lukas Jirkovsky <l.jirkovsky@gmail.com>
# Contributor: JuliusTZM <julius dot tzm at gmail dot com>

pkgname=oracle-xe
pkgver=21.3.0.0.0
pkgrel=1
pkgdesc='Oracle Database Express Edition'
url='https://www.oracle.com/database/'
license=('custom')
arch=('x86_64')
depends=('bzip2' 'expat' 'libaio')

source=('https://download.oracle.com/otn-pub/otn_software/db-express/oracle-database-xe-21c-1.0-1.ol8.x86_64.rpm'
        'oracle-xe.csh'
        'oracle-xe.sh'
        'oracle-xe.install'
        'oracle-xe.service')
sha256sums=('f8357b432de33478549a76557e8c5220ec243710ed86115c65b0c2bc00a848db'
            'a13051ee50375ad256251457883821f12f6070aaaa913c5bd7cbee6057b108d8'
            'e007cc29fd3f3b2607042042634ac7a08c1b757c768dce3469a8f1d369e9bbed'
            '09b40cbd94564c18151731c30334725340196f309b1b2305b1c5b5b2a32aece4'
            'a8bc0edef1a7404de1b20e14ae1aa5385fa811d6e90fddda2a6ed3d15aa96e53')

options=('!strip')
install='oracle-xe.install'

prepare() {
    # Fix permissions
    chown root:root opt/oracle/product/21c/dbhomeXE/bin/oradism
    chmod 4755 opt/oracle/product/21c/dbhomeXE/bin/oradism
}

package() {
    mv opt usr $pkgdir/

    # Install environment files
    install -D -m 744 oracle-xe.csh $pkgdir/etc/profile.d/oracle-xe.csh
    install -D -m 744 oracle-xe.sh $pkgdir/etc/profile.d/oracle-xe.sh

    # Install systemd service file
    install -D -m 644 oracle-xe.service $pkgdir/usr/lib/systemd/system/oracle-xe.service

    # Create oratab file
    touch $pkgdir/etc/oratab

    # Create oracle home directory
    mkdir -p $pkgdir/var/lib/oracle
}
