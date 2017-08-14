SOURCE=https://github.com/evanmiller/mod_zip
TEMPDIR:=$(shell mktemp -d)
VERSION:="1.1.6-git"

.PHONY: all depends build clean

all: depends build clean

depends:
	sudo apt-get install build-essential libpcre3-dev zlib1g-dev libssl-dev git ruby ruby-dev -y
	sudo gem install fpm
	apt-get source nginx
	git clone $(SOURCE)

build:
	cd nginx-* && ./configure --with-cc-opt='-g -O2 -fdebug-prefix-map=/build/nginx-2tpxfc/nginx-1.10.3=. -fstack-protector-strong -Wformat -Werror=format-security -Wdate-time -D_FORTIFY_SOURCE=2' --with-ld-opt='-Wl,-z,relro -Wl,-z,now' --prefix=/usr/share/nginx --conf-path=/etc/nginx/nginx.conf --http-log-path=/var/log/nginx/access.log --error-log-path=/var/log/nginx/error.log --lock-path=/var/lock/nginx.lock --pid-path=/run/nginx.pid --modules-path=/usr/lib/nginx/modules --http-client-body-temp-path=/var/lib/nginx/body --http-fastcgi-temp-path=/var/lib/nginx/fastcgi --http-proxy-temp-path=/var/lib/nginx/proxy --http-scgi-temp-path=/var/lib/nginx/scgi --http-uwsgi-temp-path=/var/lib/nginx/uwsgi --with-debug --with-pcre-jit --with-ipv6  --add-dynamic-module=../mod_zip
	make modules -C nginx-*
	mkdir -p $(TEMPDIR)/usr/lib/nginx/modules/
	mkdir -p $(TEMPDIR)/usr/lib/nginx/modules/
	mkdir -p $(TEMPDIR)/etc/nginx/modules-enabled/
	echo "load_module modules/ngx_http_zip_module.so;" > $(TEMPDIR)/etc/nginx/modules-enabled/50-mod-zip.conf
	cp nginx-*/objs/ngx_http_zip_module.so $(TEMPDIR)/usr/lib/nginx/modules
	fpm -s dir -t deb -n libnginx-mod-zip -v $(VERSION) -C $(TEMPDIR) -p libnginx-mod-zip_VERSION_ARCH.deb -d "nginx" .
	mv *.deb ../

clean:
	rm -rf nginx*
	rm -rf $(TEMPDIR)
	rm -rf mod_zip

