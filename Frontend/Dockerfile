# Use official Apache (httpd) image
FROM httpd:2.4

# Set working directory
WORKDIR /usr/local/apache2/htdocs/

# Copy frontend files into Apache's web root
COPY ./Frontend-code/ .

# Expose HTTP port
EXPOSE 80

# Apache will start automatically
CMD ["httpd-foreground"]

#######   when created one time frontend service after that update servcice url in summery.html and then again one time create docker image and then again apply frontend.yaml deploment file for update the service.
