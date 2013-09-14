VERSION=1.10.2
SOURCE=http://www.wireshark.org/download/src/all-versions/wireshark-$(VERSION).tar.bz2
TEMPDIR:=$(shell mktemp -d)

.PHONY: all depends build clean

all: depends build clean

depends:
	wget --no-clobber $(SOURCE)
	apt-get install autoconf bison flex libtool libgtk2.0-dev libpcap-dev libc-ares-dev libsmi2-dev libgnutls-dev libgcrypt11-dev libkrb5-dev libcap2-bin libgeoip-dev libortp-dev libportaudio-dev libcairo2-dev libcap-dev -y
	tar xf wireshark-$(VERSION).tar.bz2

build:
	cd wireshark-$(VERSION) && ./autogen.sh && ./configure --enable-setcap-install--prefix=/usr --sysconfdir=/usr/share --datadir=/usr/share --libdir=/usr/lib --enable-warnings-as-errors=no --with-lua=/usr/ --docdir=/usr/share/doc/wireshark-doc/
	make -C wireshark-$(VERSION)
	make -C wireshark-$(VERSION) install DESTDIR=$(TEMPDIR)
	fpm -s dir -t deb -n wireshark -v $(VERSION) -C $(TEMPDIR) -p wireshark_VERSION_ARCH.deb -d "libpcap0.8" -d "libportaudio2" -d "libgtk2.0-0" -d "libcairo2" -d "libgeoip1" -d "libcap2" . 
	mv *.deb ../

clean:
	rm -rf wireshark-$(VERSION)
	rm wireshark-$(VERSION).tar.bz2
	rm -rf $(TEMPDIR)
