# Use official Ubuntu image
FROM ubuntu:22.04

# Avoid interactive prompts
ENV DEBIAN_FRONTEND=noninteractive

# Install Apache and OpenSSL
RUN apt-get update && apt-get install -y apache2 openssl && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Enable SSL module and default SSL site
RUN a2enmod ssl && a2ensite default-ssl

# Generate self-signed certificate
RUN openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
    -keyout /etc/ssl/private/apache-selfsigned.key \
    -out /etc/ssl/certs/apache-selfsigned.crt \
    -subj "/C=NO/ST=Oslo/L=Oslo/O=StudentOrg/OU=IT/CN=localhost"

# Update default SSL site to use the generated certs
RUN sed -i 's|ssl-cert-snakeoil.pem|apache-selfsigned.crt|' /etc/apache2/sites-available/default-ssl.conf && \
    sed -i 's|ssl-cert-snakeoil.key|apache-selfsigned.key|' /etc/apache2/sites-available/default-ssl.conf

# Add custom index.html for HTTPS
RUN echo "hei fra dockerfile 443" > /var/www/html/index.html

# Expose HTTP and HTTPS ports
EXPOSE 443

# Run Apache in the foreground
CMD ["apachectl", "-D", "FOREGROUND"]
