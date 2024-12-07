FROM debian:bookworm-slim

# Actualizar repositorios y herramientas necesarias
RUN apt-get update && \
    apt-get install -y bind9 bind9utils dnsutils net-tools procps vim && \
    apt-get clean

# Crear directorios requeridos por Bind9
RUN mkdir -p /etc/bind/zones /var/cache/bind /var/run/named && \
    chown -R bind:bind /etc/bind /var/cache/bind /var/run/named

# Copiar configuraciones locales al contenedor
COPY named.conf /etc/bind/named.conf
COPY named.conf.options /etc/bind/named.conf.options
COPY named.conf.local /etc/bind/named.conf.local
COPY zones /etc/bind/zones

# Establecer el usuario y el comando para Bind9
USER bind
CMD ["named", "-g"]

