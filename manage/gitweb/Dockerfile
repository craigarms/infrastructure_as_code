FROM alpine:3.5

ENV GITLIST_URL=https://github.com/klaussilveira/gitlist/releases/download/1.0.0/gitlist-1.0.0.tar.gz

RUN apk add --no-cache git \
                        apache2 \
                        php5-apache2 \
                        curl \
                        php5-json \
                        php5-phar \
                        php5-openssl \
                        php5-mysql \
                        php5-curl \
                        php5-mcrypt \
                        php5-pdo_mysql \
                        php5-ctype \
                        php5-gd \
                        php5-xml \
                        php5-dom \
                        php5-iconv

RUN mkdir /repos /run/apache2 /web

RUN cd /repos && git --bare init foo

RUN curl -o /tmp/gitlist.tgz -SL $GITLIST_URL;\
        tar -xzf /tmp/gitlist.tgz -C /tmp/;\
        mv /tmp/gitlist /web/html;\
        rm -rf /tmp/gitlist /tmp/gitlist.tar.gz;\
        mkdir /web/html/cache;\
        chmod 777 /web/html/cache;\
        cp /web/html/config.ini-example /web/html/config.ini

RUN sed -i 's@/home/git/repositories/@/repos/@' /web/html/config.ini

RUN sed -i 's@^#LoadModule rewrite_module modules/mod_rewrite.so@LoadModule rewrite_module modules/mod_rewrite.so@' /etc/apache2/httpd.conf

RUN echo '<Virtualhost _default_:*>' > /etc/apache2/conf.d/000-default.conf;\
        echo 'DocumentRoot /web/html' >> /etc/apache2/conf.d/000-default.conf;\
        echo '<Directory />' >> /etc/apache2/conf.d/000-default.conf;\
        echo 'Options FollowSymLinks' >> /etc/apache2/conf.d/000-default.conf;\
        echo 'AllowOverride All' >> /etc/apache2/conf.d/000-default.conf;\
        echo '</Directory>' >> /etc/apache2/conf.d/000-default.conf;\
        echo '<Directory /web/html/>' >> /etc/apache2/conf.d/000-default.conf;\
        echo 'Options Indexes FollowSymLinks MultiViews' >> /etc/apache2/conf.d/000-default.conf;\
        echo 'AllowOverride All' >> /etc/apache2/conf.d/000-default.conf;\
        echo 'Require all granted' >> /etc/apache2/conf.d/000-default.conf;\
        echo '</Directory>' >> /etc/apache2/conf.d/000-default.conf;\
        echo '</Virtualhost>' >> /etc/apache2/conf.d/000-default.conf;

EXPOSE 80/tcp

CMD [ "/usr/sbin/httpd", "-D", "FOREGROUND" ]
