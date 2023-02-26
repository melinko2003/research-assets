# Openssl 3.0 via Providers Implementation

## Understanding Providers & Engines
[Engine](https://www.openssl.org/docs/man1.1.1/man1/engine.html)s & [Provider](https://www.openssl.org/docs/man3.0/man7/provider.html)s have been openssls method for interacting with external modules ( PKCS#11 HSMs, Libraries for Post Quantum Encryptions, and properitary algorithms )

## Install the Openssl 3.X Provider via script.
We next want to build the `Openssl 3.X Provider` via `build_latest_oqs_provider.sh` aka OSSL_module formerly `Openssl Engine` Support.
```
[root@alma9 ~]# ./vagrant/demo/build_latest_oqs_provider.sh
```
When the `ninja install` command finishes it should install/copy/move the `oqsprovider.so` to `/opt/liboqs/lib64`. After that either link/copy `oqsprovider.so` into `/usr/lib64/ossl-modules/`. You should be able to move to the next section and start testing.

  
### How to see where Providers/Engines are installed.
Run:>` openssl version -a`   
``` 
OpenSSL 3.0.1 14 Dec 2021 (Library: OpenSSL 3.0.1 14 Dec 2021)
built on: Wed Oct 26 00:00:00 2022 UTC
platform: linux-x86_64
options:  bn(64,64)
compiler: gcc -fPIC -pthread -m64 -Wa,--noexecstack -Wall -O3 -O2 -flto=auto -ffat-lto-objects -fexceptions -g -grecord-gcc-switches -pipe -Wall -Werror=format-security -Wp,-D_FORTIFY_SOURCE=2 -Wp,-D_GLIBCXX_ASSERTIONS -specs=/usr/lib/rpm/redhat/redhat-hardened-cc1 -fstack-protector-strong -specs=/usr/lib/rpm/redhat/redhat-annobin-cc1 -m64 -march=x86-64-v2 -mtune=generic -fasynchronous-unwind-tables -fstack-clash-protection -fcf-protection -Wa,--noexecstack -Wa,--generate-missing-build-notes=yes -specs=/usr/lib/rpm/redhat/redhat-hardened-ld -specs=/usr/lib/rpm/redhat/redhat-annobin-cc1 -DOPENSSL_USE_NODELETE -DL_ENDIAN -DOPENSSL_PIC -DOPENSSL_BUILDING_OPENSSL -DZLIB -DNDEBUG -DPURIFY -DDEVRANDOM="\"/dev/urandom\"" -DREDHAT_FIPS_VERSION="\"3.0.1-ff3fa868c239d690\"" -DSYSTEM_CIPHERS_FILE="/etc/crypto-policies/back-ends/openssl.config"
OPENSSLDIR: "/etc/pki/tls"
ENGINESDIR: "/usr/lib64/engines-3"
MODULESDIR: "/usr/lib64/ossl-modules"
Seeding source: os-specific
CPUINFO: OPENSSL_ia32cap=0xdefa220b478bffff:0x842529 
```
  
The Providers folder: `/usr/lib64/ossl-modules`  
`ll /usr/lib64/ossl-modules/`  
```
total 1420
-rwxr-xr-x. 1 root root 1330072 Nov  1 18:42 fips.so
-rwxr-xr-x. 1 root root  120344 Nov  1 18:42 legacy.so
[root@alma9 oqs-provider]# ll /usr/lib64/engines-3/ 
```
  
The Engine folder: `/usr/lib64/engines-3`
`ll /usr/lib64/engines-3/`  
```
total 204
-rwxr-xr-x. 1 root root 24560 Nov  1 18:42 afalg.so
-rwxr-xr-x. 1 root root 15520 Nov  1 18:42 capi.so
lrwxrwxrwx. 1 root root     9 Mar 25  2022 libpkcs11.so -> pkcs11.so
-rwxr-xr-x. 1 root root 53952 Nov  1 18:42 loader_attic.so
-rwxr-xr-x. 1 root root 24560 Nov  1 18:42 padlock.so
-rwxr-xr-x. 1 root root 84816 Mar 25  2022 pkcs11.so
```
### How to see what Algorithms are installed.
Command to view all algorithms available: `openssl list -signature-algorithms -provider oqsprovider`
```
  { 1.2.840.113549.1.1.1, 2.5.8.1.1, RSA, rsaEncryption } @ default
  { 1.2.840.10040.4.1, 1.2.840.10040.4.3, 1.3.14.3.2.12, 1.3.14.3.2.13, 1.3.14.3.2.27, DSA, DSA-old, DSA-SHA, DSA-SHA1, DSA-SHA1-old, dsaEncryption, dsaEncryption-old, dsaWithSHA, dsaWithSHA1, dsaWithSHA1-old } @ default
  { 1.3.101.112, ED25519 } @ default
  { 1.3.101.113, ED448 } @ default
  ECDSA @ default
  HMAC @ default
  SIPHASH @ default
  POLY1305 @ default
  CMAC @ default
  dilithium2 @ oqsprovider
  p256_dilithium2 @ oqsprovider
  rsa3072_dilithium2 @ oqsprovider
  dilithium3 @ oqsprovider
  p384_dilithium3 @ oqsprovider
  dilithium5 @ oqsprovider
  p521_dilithium5 @ oqsprovider
  dilithium2_aes @ oqsprovider
  p256_dilithium2_aes @ oqsprovider
  rsa3072_dilithium2_aes @ oqsprovider
  dilithium3_aes @ oqsprovider
  p384_dilithium3_aes @ oqsprovider
  dilithium5_aes @ oqsprovider
  p521_dilithium5_aes @ oqsprovider
  falcon512 @ oqsprovider
  p256_falcon512 @ oqsprovider
  rsa3072_falcon512 @ oqsprovider
  falcon1024 @ oqsprovider
  p521_falcon1024 @ oqsprovider
  sphincsharaka128frobust @ oqsprovider
  p256_sphincsharaka128frobust @ oqsprovider
  rsa3072_sphincsharaka128frobust @ oqsprovider
  sphincssha256128frobust @ oqsprovider
  p256_sphincssha256128frobust @ oqsprovider
  rsa3072_sphincssha256128frobust @ oqsprovider
  sphincsshake256128frobust @ oqsprovider
  p256_sphincsshake256128frobust @ oqsprovider
  rsa3072_sphincsshake256128frobust @ oqsprovider
  sphincsshake256192fsimple @ oqsprovider
  p384_sphincsshake256192fsimple @ oqsprovider
  sphincsshake256256fsimple @ oqsprovider
  p521_sphincsshake256256fsimple @ oqsprovider
```
### How to sign a new x509 test certificate
#### falcon1024
```
openssl req -verbose -x509 -new -newkey falcon1024 -keyout falcon1024.key -out falcon1024.crt -nodes -subj '/CN=GoDaddy PQC Root Generation 1' -days 365 -config /vagrant/etc/openssl-oqs.cnf -provider oqsprovider -provider default 
```
#### p521_falcon1024
```
openssl req -verbose -x509 -new -newkey p521_falcon1024 -keyout p521_falcon1024.key -out p521_falcon1024.crt -nodes -subj '/CN=GoDaddy PQC Root Generation 1' -days 365 -config /vagrant/etc/openssl-oqs.cnf -provider oqsprovider -provider default 
```
#### sphincsshake256256fsimple
```
openssl req -verbose -x509 -new -newkey sphincsshake256256fsimple -keyout sphincsshake256256fsimple.key -out sphincsshake256256fsimple.crt -nodes -subj '/CN=GoDaddy PQC Root Generation 1' -days 365 -config /vagrant/etc/openssl-oqs.cnf -provider oqsprovider -provider default
```
#### p521_dilithium5_aes
```
openssl req -verbose -x509 -new -newkey p521_dilithium5_aes -keyout p521_dilithium5_aes.key -out p521_dilithium5_aes.crt -nodes -subj '/CN=GoDaddy PQC Root Generation 1' -days 365 -config /vagrant/etc/openssl-oqs.cnf -provider oqsprovider -provider default
```
#### dilithium5_aes
```
openssl req -verbose -x509 -new -newkey dilithium5_aes -keyout dilithium5_aes.key -out dilithium5_aes.crt -nodes -subj '/CN=GoDaddy PQC Root Generation 1' -days 365 -config /vagrant/etc/openssl-oqs.cnf -provider oqsprovider -provider default
```
#### dilithium5
```
openssl req -verbose -x509 -new -newkey dilithium5 -keyout dilithium5.key -out dilithium5.crt -nodes -subj '/CN=GoDaddy PQC Root Generation 1' -days 365 -config /vagrant/etc/openssl-oqs.cnf -provider oqsprovider -provider default
```
### How to view a certificate
```
openssl x509 -in qsc.crt -text -noout -provider oqsprovider -provider default