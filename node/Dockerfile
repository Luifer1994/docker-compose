# Imagen de NodeJS
FROM node:18-alpine

# Establecer directorio de trabajo
WORKDIR /var/www/html/app

# Copiar shell scripts
COPY scripts /var/www/salescontrol/node

# Eliminar caracteres incompatibles
RUN sed -i 's/\r$//' /var/www/salescontrol/node/*.sh

# Otorgar permisos de ejecución a los archivos sh
RUN chmod +x /var/www/salescontrol/node/*.sh

# Ejecutar archivo principal sh de arranque
CMD [ "/var/www/salescontrol/node/run.sh" ]