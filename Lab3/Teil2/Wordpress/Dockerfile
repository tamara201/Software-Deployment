FROM debian:jessie

RUN apt update
RUN apt upgrade

RUN apt install -y apache2
RUN apt install -y php5 libapache2-mod-php5 php5-mcrypt php5-mysql

RUN cd /var/www/html/ && \
    apt install -y wget && \
    wget https://wordpress.org/latest.zip && \
    apt install -y unzip && \
    unzip -q latest.zip && \
    chown -R www-data:www-data /var/www/html/wordpress && \
    chmod -R 755 /var/www/html/wordpress && \
    mkdir -p /var/www/html/wordpress/wp-content/uploads && \
    chown -R www-data:www-data /var/www/html/wordpress/wp-content/uploads

EXPOSE 80/tcp

VOLUME /var/www/html/wordpress

CMD apachectl -D FOREGROUND