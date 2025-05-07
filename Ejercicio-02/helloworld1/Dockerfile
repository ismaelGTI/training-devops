# Node v18
FROM node:18-alpine AS build-step
RUN mkdir -p /training-angular
WORKDIR /training-angular
COPY package.json /training-angular
RUN npm install
COPY . /training-angular
RUN npm run build --prod
# Depuración: Mostrar contenido de la carpeta dist
RUN ls -la /training-angular/dist
RUN ls -la /training-angular/dist/helloworld1

FROM nginx:1.17.1-alpine
COPY --from=build-step /training-angular/dist/helloworld1 /usr/share/nginx/html
# Depuración: Mostrar contenido de la carpeta de Nginx
RUN ls -la /usr/share/nginx/html
