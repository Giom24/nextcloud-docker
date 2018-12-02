FROM nextcloud:apache

ARG CONTRY_CODE
ARG STATE
ARG LOCATION
ARG ORGANISATION
ARG ORGANIZATIONAL_UNIT
ARG COMMON_NAME

##Install SSL
RUN a2enmod ssl
RUN mkdir /etc/apache2/ssl
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/apache.key -out /etc/apache2/ssl/apache.crt \ 
    -subj "/C=${CONTRY_CODE}/ST=${STATE}/L=${LOCATION}/O=${ORGANISATION}/OU=${ORGANIZATIONAL_UNIT}/CN=${COMMON_NAME}"

RUN echo \
"<VirtualHost *:443>\n\
    SSLEngine on\n\
    SSLCertificateFile /etc/apache2/ssl/apache.crt\n\
    SSLCertificateKeyFile /etc/apache2/ssl/apache.key\n\
    \n\
    DocumentRoot /var/www/html/\n\
</VirtualHost>" >> /etc/apache2/sites-available/ssl.conf

EXPOSE 443

RUN a2ensite ssl.conf