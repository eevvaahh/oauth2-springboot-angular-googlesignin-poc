# 1. ETAPA DE CONSTRUCCIÓN (BUILD STAGE)
FROM node:18-alpine AS builder

WORKDIR /app

# Instalar dependencias
COPY package.json package-lock.json ./
RUN npm install

# Copiar el código fuente y construir la aplicación
COPY . .
RUN npm run build --prod

# 2. ETAPA DE EJECUCIÓN (RUNTIME STAGE)
FROM nginx:alpine

# Copiar los archivos de construcción de Angular
COPY --from=builder /app/dist/ag-prueba-front /usr/share/nginx/html

# Copiar el archivo de configuración de NGINX para el routing de Angular
COPY nginx.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
