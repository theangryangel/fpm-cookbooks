VERSION=6.40
SOURCE=http://nmap.org/dist/nmap-$(VERSION).tar.bz2
TEMPDIR:=$(shell mktemp -d)

.PHONY: all depends build clean

all: depends build clean

depends:
	wget --no-clobber $(SOURCE)
	apt-get install libssl-dev libdnet-dev libpcap-dev libpcre3-dev liblua5.1-0-dev -y
	tar xf nmap-$(VERSION).tar.bz2

build:
	cd nmap-$(VERSION) && ./configure --prefix=/usr
	make -C nmap-$(VERSION)
	make -C nmap-$(VERSION) install DESTDIR=$(TEMPDIR)
	fpm -s dir -t deb -n nmap -v $(VERSION) -C $(TEMPDIR) -p nmap_VERSION_ARCH.deb -d "libssl1.0.0" -d "libpcre3" -d "libdnet" -d "liblua5.1.0" .
	mv *.deb ../

clean:
	rm -rf nmap-$(VERSION)
	rm nmap-$(VERSION).tar.bz2
	rm -rf $(TEMPDIR)
