### STAGE 1: Build ###
FROM node:latest AS build-step
WORKDIR /app
COPY . .
RUN npm install
RUN npm run build --prod

### STAGE 2: Run ###
FROM nginx:latest
COPY --from=build-step /app/dist/OnlineBookShopFrontEnd /usr/share/nginx/html
COPY ./nginx-custom.conf /etc/nginx/conf.d/default.conf
# When the container starts, replace the env.js with values from environment variables
ENTRYPOINT ["/bin/sh",  "-c",  "envsubst < /usr/share/nginx/html/assets/env.template.js > /usr/share/nginx/html/assets/env.js && exec nginx -g 'daemon off;'"]
