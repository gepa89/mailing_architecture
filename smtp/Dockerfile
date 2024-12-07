# Usa una imagen base mínima
FROM debian:latest

# Actualiza el sistema e instala Postfix y SASL
RUN apt-get update && apt-get install -y \
    postfix \
    libsasl2-modules \
    sasl2-bin \
    && apt-get clean

# Crea los directorios necesarios para Postfix y TLS
RUN mkdir -p /etc/postfix /var/spool/postfix /etc/ssl/private /etc/ssl/certs /var/lib/postfix

# Copia los archivos de configuración de Postfix
COPY main.cf /etc/postfix/main.cf
COPY master.cf /etc/postfix/master.cf

# Copia los certificados de TLS
COPY certs/your-cert.pem /etc/ssl/certs/your-cert.pem
COPY certs/your-key.pem /etc/ssl/private/your-key.pem

# Ajusta los permisos de los certificados
RUN chmod 600 /etc/ssl/private/your-key.pem && \
    chmod 644 /etc/ssl/certs/your-cert.pem

# Comando para iniciar Postfix en primer plano
CMD ["postfix", "start-fg"]

