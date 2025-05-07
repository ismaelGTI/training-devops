FROM node:16-alpine as build-step
RUN mkdir -p /training-angular
WORKDIR /training-angular
COPY package.json /training-angular
RUN npm install
COPY . /training-angular
RUN npm run build --prod

FROM nginx:1.17.1-alpine
COPY --from=build-step /training-angular/dist/helloworld1 /usr/share/nginx/html
