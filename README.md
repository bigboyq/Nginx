# Nginx
Nginx with ngx_connect_module
1. vi /etc/apt/sources.list.d/nginx.list
```
deb-src https://nginx.org/packages/debian/ bullseye nginx
```
2. Trust Nginx repo
```
apt install gnupg
apt-key adv --keyserver keyserver.ubuntu.com --recv-keys ABF5BD827BD9BF62
apt update
```
3. Nginx Build Environement
```
apt-get build-dep nginx
```
4. Install Openssl
```
cd /usr/local/src
git clone https://github.com/openssl/openssl.git
cd openssl
git branch -a
git checkout OpenSSL_1_1_1-stable
```
5. Install ngx_connect_module
```
cd ~
git clone https://github.com/chobits/ngx_http_proxy_connect_module.git
```
6. Get Nginx Source
```
cd ~
wget http://nginx.org/download/nginx-1.21.6.tar.gz
tar xzvf nginx-1.21.6.tar.gz
```
7. Patch with Ngx_connect_module
```
cd ~/nginx-1.21.6
patch -p1 <~/ngx_http_proxy_connect_module/patch/proxy_connect_rewrite_102101.patch
```
8. Prepare for dpkg-buildpackage
```
tar xvf nginx_1.26.1-1~bullseye.debian.tar.xz -C ~/nginx-1.21.6
```
9. Build
```
cd ~/nginx-1.21.6
dpkg-buildpackage -uc -b
```

# More to know
1. nginx_1.20.2-1~bullseye.debian.tar.xz is original from Debian
2. nginx_1.26.1-1~bullseye.debian.tar.xz is modified version
3. debian/rules modified
3.1 add ngx_connect_module
3.2 add openssl src
3.3 "-Wno-missing-field-initializers" appended to DEB_CFLAGS_MAINT_APPEND for ignore warning
4. changelog modified for correct build version
5. CHANGE/CHANGE.ru updated with Nginx-1.26.1 source
6. nginx.service modified for resolve PID warning

# Thanks
1. https://nginx.org/
2. https://github.com/chobits/ngx_http_proxy_connect_module
