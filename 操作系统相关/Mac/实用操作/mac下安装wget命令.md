> brew install wget   

或者



```shell
curl -O http://ftp.gnu.org/gnu/wget/wget-1.13.4.tar.gz

tar xzvf wget-1.13.4.tar.gz

cd wget-1.13.4

./configure --with-ssl=openssl

sudo make

sudo make install

which wget #Should output: /usr/local/bin/wget

```

