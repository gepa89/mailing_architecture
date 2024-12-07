FROM debian:latest

# Actualiza el sistema e instala Postfix
RUN apt-get update && apt-get install -y \
    postfix \
    libsasl2-modules \
    sasl2-bin \
    && apt-get clean

# Crea directorios necesarios para Postfix
RUN mkdir -p /etc/postfix /var/spool/postfix /etc/ssl/private /etc/ssl/certs

# Copia certificados y configuraciones
COPY main.cf /etc/postfix/main.cf
COPY master.cf /etc/postfix/master.cf
COPY certs/your-cert.pem /etc/ssl/certs/your-cert.pem
COPY certs/your-key.pem /etc/ssl/private/your-key.pem

# Ajusta permisos de los certificados
RUN chmod 600 /etc/ssl/private/your-key.pem && \
    chmod 644 /etc/ssl/certs/your-cert.pem

# Configura el servicio de Postfix
CMD ["postfix", "start-fg"]

