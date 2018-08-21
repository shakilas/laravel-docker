FROM php:7-fpm-alpine

RUN apk --update upgrade --no-cache add php7-xdebug; \
    php -r "copy('http://getcomposer.org/installer', 'composer-setup.php');" && \
    php composer-setup.php --install-dir=/usr/bin --filename=composer && \
    php -r "unlink('composer-setup.php');"

# XDEBUG
ENV XDEBUGINI_PATH=/usr/local/etc/php/conf.d/xdebug.ini

RUN echo "zend_extension=$(find /usr/local/lib/php/extensions/ -name xdebug.so)" >> $XDEBUGINI_PATH
RUN echo "xdebug.remote_host="`/sbin/ip route|awk '/default/ { print $3 }'` >> $XDEBUGINI_PATH
RUN echo "xdebug.remote_enable=on" >> $XDEBUGINI_PATH
RUN echo "xdebug.remote_autostart=off" >> $XDEBUGINI_PATH
COPY xdebug.ini /tmp/xdebug.ini
RUN cat /tmp/xdebug.ini >> $XDEBUGINI_PATH