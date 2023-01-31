FROM debian:11.6 AS builder

WORKDIR /tmp/make
COPY *.tar.gz ./

# Installing dependencies
RUN apt-get update && apt-get install -y tar build-essential
# Compiling and installing PCRE from source file
RUN mkdir pcre2 &&\
        tar -zxf pcre2.tar.gz -C pcre2 --strip-components 1 &&\
        cd pcre2 &&\
        ./configure &&\
        make &&\
        make install
# Compiling and installing zlib from source file
RUN mkdir zlib &&\
        tar -zxf zlib.tar.gz -C zlib --strip-components 1  &&\
        cd zlib &&\
        ./configure &&\
        make &&\
        make install
# Compiling and installing OpenSSL from source file
RUN mkdir openssl &&\
        tar -zxf openssl.tar.gz -C openssl --strip-components 1 &&\
        cd openssl &&\
        ./Configure linux-x86_64 --prefix=/usr &&\
        make &&\
        make install

# Compiling and installing nginx from source file
RUN mkdir nginx &&\
        tar zxf nginx.tar.gz -C nginx --strip-components 1 &&\
        cd nginx &&\
        ./configure \ 
            --prefix=/usr/local/nginx \
            --sbin-path=sbin/nginx \
            --conf-path=nginx.conf &&\
        make &&\
        make install &&\
        echo "daemon off;" >> /usr/local/nginx/nginx.conf &&\
        echo "error_log /dev/stdout info;" >> /usr/local/nginx/nginx.conf
        #echo "access_log /dev/stdout info;" >> /usr/local/nginx/nginx.conf

ENTRYPOINT [ "/usr/local/nginx/sbin/nginx"]
