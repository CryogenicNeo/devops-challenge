# Docker build 1st stage

FROM docker.io/node:15.5.1-alpine3.12@sha256:5f693a289930c5a1f690458d35259a882546007d776ae521a96e4140aebfdccd as builder

WORKDIR /src

COPY ./package.json ./package-lock.json .
COPY ./public/ public/
COPY ./src/ src/

RUN npm ci
RUN npm run build

# Docker build 2nd stage

FROM docker.io/nginx:stable-alpine@sha256:dc5069ad14f19660b141b21236140b91656bf89bbc3e2417c70ae650cd66104c

WORKDIR /app

COPY --from=builder /src/build/ .

COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

EXPOSE 80

CMD [ "/usr/sbin/nginx", "-g", "daemon off;" ]
