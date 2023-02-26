# Openssl 1.1.1 static compiled Implementation
## Sources
QSC/Openssl: https://github.com/open-quantum-safe/openssl  

## Install the Openssl 1.1.1 via script.
Build `Openssl 1.1.1 w/OQS Algorithms` via `build_static_openssl111.sh`. Which includes everything in a single openssl-1.1.1 binary.
```
[root@alma9 ~]# ./vagrant/demo/openssl-1.1.1/build_static_openssl111.sh
```
When the `ninja install` command finishes it should install Openssl 1.1.1 to `/opt/openssl-1.1.1/apps/openssl`  
### How to see where Engines/Openssl are installed.
Run:>`apps/openssl version -a`   
``` 
OpenSSL 1.1.1s  1 Nov 2022, Open Quantum Safe 2022-11
built on: Thu Jan 26 20:59:44 2023 UTC
platform: linux-x86_64
options:  bn(64,64) rc4(16x,int) des(int) idea(int) blowfish(ptr) 
compiler: gcc -fPIC -pthread -m64 -Ioqs/include -Wa,--noexecstack -Wall -O3 -DOPENSSL_USE_NODELETE -DL_ENDIAN -DOPENSSL_PIC -DOPENSSL_CPUID_OBJ -DOPENSSL_IA32_SSE2 -DOPENSSL_BN_ASM_MONT -DOPENSSL_BN_ASM_MONT5 -DOPENSSL_BN_ASM_GF2m -DSHA1_ASM -DSHA256_ASM -DSHA512_ASM -DKECCAK1600_ASM -DRC4_ASM -DMD5_ASM -DAESNI_ASM -DVPAES_ASM -DGHASH_ASM -DECP_NISTZ256_ASM -DX25519_ASM -DPOLY1305_ASM -DNDEBUG
OPENSSLDIR: "/usr/local/ssl"
ENGINESDIR: "/usr/local/lib64/engines-1.1"
Seeding source: os-specific
```
The Engine folder: `/usr/local/lib64/engines-1.1`  
`ll /usr/local/lib64/engines-1.1`  
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
Command to view all algorithms available: `# apps/openssl list -public-key-algorithms `
```
Name: OpenSSL RSA method
        Type: Builtin Algorithm
        OID: rsaEncryption
        PEM string: RSA
Name: rsa
        Alias for: rsaEncryption
Name: OpenSSL PKCS#3 DH method
        Type: Builtin Algorithm
        OID: dhKeyAgreement
        PEM string: DH
Name: dsaWithSHA
        Alias for: dsaEncryption
Name: dsaEncryption-old
        Alias for: dsaEncryption
Name: dsaWithSHA1-old
        Alias for: dsaEncryption
Name: dsaWithSHA1
        Alias for: dsaEncryption
Name: OpenSSL DSA method
        Type: Builtin Algorithm
        OID: dsaEncryption
        PEM string: DSA
Name: OpenSSL EC algorithm
        Type: Builtin Algorithm
        OID: id-ecPublicKey
        PEM string: EC
Name: OpenSSL HMAC method
        Type: Builtin Algorithm
        OID: hmac
        PEM string: HMAC
Name: OpenSSL CMAC method
        Type: Builtin Algorithm
        OID: cmac
        PEM string: CMAC
Name: OpenSSL RSA-PSS method
        Type: Builtin Algorithm
        OID: rsassaPss
        PEM string: RSA-PSS
Name: OpenSSL X9.42 DH method
        Type: Builtin Algorithm
        OID: X9.42 DH
        PEM string: X9.42 DH
Name: OpenSSL X25519 algorithm
        Type: Builtin Algorithm
        OID: X25519
        PEM string: X25519
Name: OpenSSL X448 algorithm
        Type: Builtin Algorithm
        OID: X448
        PEM string: X448
Name: OpenSSL POLY1305 method
        Type: Builtin Algorithm
        OID: poly1305
        PEM string: POLY1305
Name: OpenSSL SIPHASH method
        Type: Builtin Algorithm
        OID: siphash
        PEM string: SIPHASH
Name: OpenSSL ED25519 algorithm
        Type: Builtin Algorithm
        OID: ED25519
        PEM string: ED25519
Name: OpenSSL ED448 algorithm
        Type: Builtin Algorithm
        OID: ED448
        PEM string: ED448
Name: sm2
        Alias for: id-ecPublicKey
Name: OpenSSL Dilithium2 algorithm
        Type: Builtin Algorithm
        OID: dilithium2
        PEM string: dilithium2
Name: OpenSSL ECDSA p256 Dilithium2 algorithm
        Type: Builtin Algorithm
        OID: p256_dilithium2
        PEM string: p256_dilithium2
Name: OpenSSL RSA3072 Dilithium2 algorithm
        Type: Builtin Algorithm
        OID: rsa3072_dilithium2
        PEM string: rsa3072_dilithium2
Name: OpenSSL Dilithium3 algorithm
        Type: Builtin Algorithm
        OID: dilithium3
        PEM string: dilithium3
Name: OpenSSL ECDSA p384 Dilithium3 algorithm
        Type: Builtin Algorithm
        OID: p384_dilithium3
        PEM string: p384_dilithium3
Name: OpenSSL Dilithium5 algorithm
        Type: Builtin Algorithm
        OID: dilithium5
        PEM string: dilithium5
Name: OpenSSL ECDSA p521 Dilithium5 algorithm
        Type: Builtin Algorithm
        OID: p521_dilithium5
        PEM string: p521_dilithium5
Name: OpenSSL Dilithium2_AES algorithm
        Type: Builtin Algorithm
        OID: dilithium2_aes
        PEM string: dilithium2_aes
Name: OpenSSL ECDSA p256 Dilithium2_AES algorithm
        Type: Builtin Algorithm
        OID: p256_dilithium2_aes
        PEM string: p256_dilithium2_aes
Name: OpenSSL RSA3072 Dilithium2_AES algorithm
        Type: Builtin Algorithm
        OID: rsa3072_dilithium2_aes
        PEM string: rsa3072_dilithium2_aes
Name: OpenSSL Dilithium3_AES algorithm
        Type: Builtin Algorithm
        OID: dilithium3_aes
        PEM string: dilithium3_aes
Name: OpenSSL ECDSA p384 Dilithium3_AES algorithm
        Type: Builtin Algorithm
        OID: p384_dilithium3_aes
        PEM string: p384_dilithium3_aes
Name: OpenSSL Dilithium5_AES algorithm
        Type: Builtin Algorithm
        OID: dilithium5_aes
        PEM string: dilithium5_aes
Name: OpenSSL ECDSA p521 Dilithium5_AES algorithm
        Type: Builtin Algorithm
        OID: p521_dilithium5_aes
        PEM string: p521_dilithium5_aes
Name: OpenSSL Falcon-512 algorithm
        Type: Builtin Algorithm
        OID: falcon512
        PEM string: falcon512
Name: OpenSSL ECDSA p256 Falcon-512 algorithm
        Type: Builtin Algorithm
        OID: p256_falcon512
        PEM string: p256_falcon512
Name: OpenSSL RSA3072 Falcon-512 algorithm
        Type: Builtin Algorithm
        OID: rsa3072_falcon512
        PEM string: rsa3072_falcon512
Name: OpenSSL Falcon-1024 algorithm
        Type: Builtin Algorithm
        OID: falcon1024
        PEM string: falcon1024
Name: OpenSSL ECDSA p521 Falcon-1024 algorithm
        Type: Builtin Algorithm
        OID: p521_falcon1024
        PEM string: p521_falcon1024
Name: OpenSSL SPHINCS+-Haraka-128f-robust algorithm
        Type: Builtin Algorithm
        OID: sphincsharaka128frobust
        PEM string: sphincsharaka128frobust
Name: OpenSSL ECDSA p256 SPHINCS+-Haraka-128f-robust algorithm
        Type: Builtin Algorithm
        OID: p256_sphincsharaka128frobust
        PEM string: p256_sphincsharaka128frobust
Name: OpenSSL RSA3072 SPHINCS+-Haraka-128f-robust algorithm
        Type: Builtin Algorithm
        OID: rsa3072_sphincsharaka128frobust
        PEM string: rsa3072_sphincsharaka128frobust
Name: OpenSSL SPHINCS+-Haraka-128f-simple algorithm
        Type: Builtin Algorithm
        OID: sphincsharaka128fsimple
        PEM string: sphincsharaka128fsimple
Name: OpenSSL ECDSA p256 SPHINCS+-Haraka-128f-simple algorithm
        Type: Builtin Algorithm
        OID: p256_sphincsharaka128fsimple
        PEM string: p256_sphincsharaka128fsimple
Name: OpenSSL RSA3072 SPHINCS+-Haraka-128f-simple algorithm
        Type: Builtin Algorithm
        OID: rsa3072_sphincsharaka128fsimple
        PEM string: rsa3072_sphincsharaka128fsimple
Name: OpenSSL SPHINCS+-SHA256-128f-robust algorithm
        Type: Builtin Algorithm
        OID: sphincssha256128frobust
        PEM string: sphincssha256128frobust
Name: OpenSSL ECDSA p256 SPHINCS+-SHA256-128f-robust algorithm
        Type: Builtin Algorithm
        OID: p256_sphincssha256128frobust
        PEM string: p256_sphincssha256128frobust
Name: OpenSSL RSA3072 SPHINCS+-SHA256-128f-robust algorithm
        Type: Builtin Algorithm
        OID: rsa3072_sphincssha256128frobust
        PEM string: rsa3072_sphincssha256128frobust
Name: OpenSSL SPHINCS+-SHA256-128s-simple algorithm
        Type: Builtin Algorithm
        OID: sphincssha256128ssimple
        PEM string: sphincssha256128ssimple
Name: OpenSSL ECDSA p256 SPHINCS+-SHA256-128s-simple algorithm
        Type: Builtin Algorithm
        OID: p256_sphincssha256128ssimple
        PEM string: p256_sphincssha256128ssimple
Name: OpenSSL RSA3072 SPHINCS+-SHA256-128s-simple algorithm
        Type: Builtin Algorithm
        OID: rsa3072_sphincssha256128ssimple
        PEM string: rsa3072_sphincssha256128ssimple
Name: OpenSSL SPHINCS+-SHAKE256-128f-simple algorithm
        Type: Builtin Algorithm
        OID: sphincsshake256128fsimple
        PEM string: sphincsshake256128fsimple
Name: OpenSSL ECDSA p256 SPHINCS+-SHAKE256-128f-simple algorithm
        Type: Builtin Algorithm
        OID: p256_sphincsshake256128fsimple
        PEM string: p256_sphincsshake256128fsimple
Name: OpenSSL RSA3072 SPHINCS+-SHAKE256-128f-simple algorithm
        Type: Builtin Algorithm
        OID: rsa3072_sphincsshake256128fsimple
        PEM string: rsa3072_sphincsshake256128fsimple
```
### How to sign a new x509 test certificate
#### falcon1024
```
apps/openssl req -verbose -x509 -new -newkey falcon1024 -keyout falcon1024.key -out falcon1024.crt -nodes -subj '/CN=GoDaddy PQC Root Generation 1' -days 365 -config /vagrant/etc/root-openssl-1.1.1.cnf 
```
#### p521_falcon1024
```
apps/openssl req -verbose -x509 -new -newkey p521_falcon1024 -keyout p521_falcon1024.key -out p521_falcon1024.crt -nodes -subj '/CN=GoDaddy PQC Root Generation 1' -days 365 -config /vagrant/etc/root-openssl-1.1.1.cnf
```
#### sphincsshake256256fsimple
```
apps/openssl req -verbose -x509 -new -newkey sphincsshake256256fsimple -keyout sphincsshake256256fsimple.key -out sphincsshake256256fsimple.crt -nodes -subj '/CN=GoDaddy PQC Root Generation 1' -days 365 -config /vagrant/etc/root-openssl-1.1.1.cnf 
```
#### p521_dilithium5_aes
```
apps/openssl req -verbose -x509 -new -newkey p521_dilithium5_aes -keyout p521_dilithium5_aes.key -out p521_dilithium5_aes.crt -nodes -subj '/CN=GoDaddy PQC Root Generation 1' -days 365 -config /vagrant/etc/root-openssl-1.1.1.cnf 
```
#### dilithium5_aes
```
apps/openssl req -verbose -x509 -new -newkey dilithium5_aes -keyout dilithium5_aes.key -out dilithium5_aes.crt -nodes -subj '/CN=GoDaddy PQC Root Generation 1' -days 365 -config /vagrant/etc/root-openssl-1.1.1.cnf 
```
#### dilithium5
```
apps/openssl req -verbose -x509 -new -newkey dilithium5 -keyout dilithium5.key -out dilithium5.crt -nodes -subj '/CN=GoDaddy PQC Root Generation 1' -days 365 -config /vagrant/etc/root-openssl-1.1.1.cnf 
```
### How to view a certificate
```
apps/openssl x509 -in qsc.crt -text -noout 