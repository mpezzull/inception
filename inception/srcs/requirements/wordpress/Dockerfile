FROM  alpine:3.14

# Update System and Install Tools
RUN apk update
RUN apk add openrc
RUN apk add php7-common php7-iconv php7-json php7-gd php7-curl php7-xml \
	php7-mysqli php7-imap php7-cgi fcgi php7-pdo php7-pdo_mysql php7-soap php7-xmlrpc \
	php7-posix php7-mcrypt php7-gettext php7-ldap php7-ctype php7-dom php7 php7-fpm php7-opcache


# Download WordPress and untar it
RUN wget https://wordpress.org/latest.tar.gz
RUN tar xvf latest.tar.gz
RUN rm latest.tar.gz

# ADD and COPY Files to container
COPY conf/wp-config.php /wordpress/wp-config.php

# start openrc
RUN openrc
RUN touch /run/openrc/softlevel

# Copy installing script and make it executable
COPY tools/run.sh /
COPY conf/www.conf /etc/php7/php-fpm.d
RUN chmod +x ./run.sh

ENTRYPOINT [ "./run.sh" ]
