FROM debian:jessie
MAINTAINER Randy Nel Gupta <gupta@scaratec.com>

# Change this when a newer version is released:
ENV TYPO3_VERSION 7.0.2

RUN apt-get update && apt-get upgrade -q -y && \
    apt-get install -y apache2 libapache2-mod-php5 imagemagick php5-cgi php5-curl php5-gd php5-mysql wget && \
    apt-get clean && rm -rf /tmp/* /var/tmp/* && \
    mkdir -p /var/www/ && \
    cd /var/www/ && \
    wget -O - http://prdownloads.sourceforge.net/typo3/typo3_src-${TYPO3_VERSION}.tar.gz | tar zxf - && \
    ln -s typo3_src-${TYPO3_VERSION} typo3_src && \
    cd html && \
    rm -R * && \
    ln -s ../typo3_src typo3_src && \
    ln -s typo3_src/index.php index.php && \
    ln -s typo3_src/typo3 typo3 && \
    touch FIRST_INSTALL && \
    cp typo3_src/_.htaccess ./ && \
    chown -R www-data:www-data /var/www && \
    mv _.htaccess .htaccess
COPY etc/php5/apache2/php.ini /etc/php5/apache2/
CMD /usr/sbin/apache2ctl -D FOREGROUND
