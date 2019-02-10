## How to prepare oracle/*
download Oracle instantclient from Oracle site to oracle directory  

## How to prepare *.so file

download php source code

```
$ curl -L -O http://jp2.php.net/get/php-7.1.16.tar.gz/from/this/mirror
$ tar xzvf mirror
```

compile oci8

```
cd php-7.1.16/ext/oci8/
phpize
./configure --with-oci8=shared,instantclient,/usr/local/instantclient
make
make install
```

compile pdo\_oci

```
cd php-7.1.16/ext/pdo_oci/
phpize
./configure --with-pdo_oci=shared,instantclient,/usr/local/instantclient
make
make install
```

And copy *.so to local








