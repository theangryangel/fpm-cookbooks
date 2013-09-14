VERSION=2.3
SOURCE=http://www.thc.org/releases/thc-ipv6-$(VERSION).tar.gz
TEMPDIR:=$(shell mktemp -d)

.PHONY: all depends build clean

all: depends build clean

depends:
	wget --no-clobber $(SOURCE)
	apt-get install libpcap-dev libssl-dev  -y
	tar xf thc-ipv6-$(VERSION).tar.gz

build:
	make -C thc-ipv6-$(VERSION)
	make -C thc-ipv6-$(VERSION) install DESTDIR=$(TEMPDIR)
	fpm -s dir -t deb -n thc-ipv6 -v $(VERSION) -C $(TEMPDIR) -p thc-ipv6_VERSION_ARCH.deb -d "libssl1.0.0" -d "libpcap0.8" .
	mv *.deb ../

clean:
	rm -rf thc-ipv6-$(VERSION)
	rm thc-ipv6-$(VERSION).tar.gz
	rm -rf $(TEMPDIR)
