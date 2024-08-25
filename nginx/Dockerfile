FROM centos:7
COPY gmcurl /usr/bin/gmcurl
COPY gmssl_openssl_1.1_b2024_x64_1.tar.gz /usr/local/gmssl_openssl_1.1_b2024_x64_1.tar.gz
COPY nginx-1.24.0.tar.gz /usr/local/nginx-1.24.0.tar.gz
RUN cd /etc/yum.repos.d/ && mkdir bak && rm *.repo && curl -o /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo && yum -y install gcc make pcre-devel zlib-devel && yum clean all && rm -rf  Centos-7.repo
RUN bash && cd /usr/local/ && tar zxvf gmssl_openssl_1.1_b2024_x64_1.tar.gz && rm -rf gmssl_openssl_1.1_b2024_x64_1.tar.gz && tar -zxvf nginx-1.24.0.tar.gz && rm -rf nginx-1.24.0.tar.gz && useradd nginx && cd nginx-1.24.0 && ./configure --prefix=/usr/local/nginx  --http-client-body-temp-path=/usr/local/nginx/client_temp --http-proxy-temp-path=/usr/local/nginx/proxy_temp --http-fastcgi-temp-path=/usr/local/nginx/fastcgi_temp --http-uwsgi-temp-path=/usr/local/nginx/uwsgi_temp --http-scgi-temp-path=/usr/local/nginx/scgi_temp --user=nginx --group=nginx --with-compat --with-file-aio --with-threads --with-http_addition_module --with-http_auth_request_module --with-http_dav_module --with-http_flv_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_mp4_module --with-http_random_index_module --with-http_realip_module --with-http_secure_link_module --with-http_slice_module --with-http_ssl_module --with-http_stub_status_module --with-http_sub_module --with-http_v2_module --with-mail --with-mail_ssl_module --with-stream --with-stream_realip_module --with-stream_ssl_module --with-stream_ssl_preread_module --with-cc-opt="-I/usr/local/gmssl/include" --with-ld-opt="-lm" --with-openssl="/usr/local/gmssl" && make && make install && cd /usr/local/nginx/ && rm -rf /usr/local/nginx-1.24.0 && mkdir -p /usr/local/nginx/ssl && chown -R nginx:nginx /usr/local/nginx
ENV NGINX_VERSION 1.24.0
ENV GMOPENSSL_VERSION 1.1_b2024_x64_1
ENV PATH /usr/local/nginx/sbin:$PATH
WORKDIR /usr/local/nginx
EXPOSE 180
CMD ["nginx", "-g", "daemon off;"]
#CMD ["nginx"]
