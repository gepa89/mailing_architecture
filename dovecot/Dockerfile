FROM dovecot/dovecot:latest

# Variables de entorno
ENV POSTFIX_USER=postfix
ENV POSTFIX_GROUP=postfix
ENV POSTFIX_UID=89
ENV POSTFIX_GID=89

# Crea el grupo y usuario postfix si no existen
RUN if ! getent group ${POSTFIX_GROUP}; then groupadd -r -g ${POSTFIX_GID} ${POSTFIX_GROUP}; fi && \
    if ! id -u ${POSTFIX_USER} >/dev/null 2>&1; then \
    useradd -r -u ${POSTFIX_UID} -g ${POSTFIX_GROUP} ${POSTFIX_USER}; fi

# Crea el directorio de autenticación para Postfix y asigna permisos
RUN mkdir -p /var/spool/postfix/private && \
    chown -R ${POSTFIX_USER}:${POSTFIX_GROUP} /var/spool/postfix/private && \
    chmod -R 770 /var/spool/postfix/private

# Copia los archivos de configuración
COPY ./conf.d /etc/dovecot/conf.d/
COPY ./auth-passwdfile.conf.ext /etc/dovecot/auth-passwdfile.conf.ext

# Ajusta permisos de configuración y datos
RUN chown -R vmail:mail /etc/dovecot /var/mail && \
    chmod -R 750 /etc/dovecot /var/mail

# Expone los puertos necesarios para IMAP, POP3 y LMTP
EXPOSE 143 993 110 995 24

# Ejecuta Dovecot
CMD ["dovecot", "-F"]

