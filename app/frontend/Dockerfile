FROM node:18-alpine AS build

# make the 'app' folder the current working directory
WORKDIR /app

COPY . .
RUN pwd
RUN ls -l
RUN echo "------------------"

# install project dependencies
RUN npm install
RUN npm run build

FROM nginx:alpine

RUN echo "------------------"
RUN pwd
RUN ls -l

WORKDIR /usr/share/nginx/html
COPY --from=build /app/build .
COPY --from=build /app/nginx/nginx.conf.template /etc/nginx/conf.d

RUN echo "------------------"
RUN ls -l
RUN pwd

EXPOSE 80

CMD ["/bin/sh", "-c", "envsubst < /etc/nginx/conf.d/nginx.conf.template > /etc/nginx/conf.d/default.conf && nginx -g \"daemon off;\""]
