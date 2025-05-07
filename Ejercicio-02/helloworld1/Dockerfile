<<<<<<< HEAD
# Node v16
FROM node:16-alpine as build-step
=======
FROM node:18 as build-step
>>>>>>> 705315b2b1f07ccc3fbb1e53998e51cf95df6296
RUN mkdir -p /training-angular
WORKDIR /training-angular
COPY package.json /training-angular
RUN npm install
COPY . /training-angular
RUN npm run build --prod

FROM nginx:1.17.1-alpine
<<<<<<< HEAD
COPY --from=build-step /training-angular/dist/helloworld1 /usr/share/nginx/html
=======
COPY --from=build-step /training-angular/dist/helloworld1 /usr/share/nginx/html
>>>>>>> 705315b2b1f07ccc3fbb1e53998e51cf95df6296
