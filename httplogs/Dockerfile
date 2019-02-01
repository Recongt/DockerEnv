FROM httpd:2.4

RUN htpasswd -b -c /usr/local/apache2/.htpasswd userlogs labsy
COPY httpd.conf /usr/local/apache2/conf/
COPY .htaccess /usr/local/apache2/htdocs/

VOLUME ["/usr/local/apache2/htdocs/"]
