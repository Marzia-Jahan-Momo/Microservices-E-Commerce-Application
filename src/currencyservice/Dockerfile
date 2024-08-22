FROM node:20.16.0-alpine as builder

RUN apk add --update --no-cache python3 make g++

WORKDIR /usr/src/app

COPY package*.json ./

RUN npm install --only=production


# Final stage
FROM alpine:3.20.2

RUN apk add --no-cache nodejs

WORKDIR /usr/src/app

COPY --from=builder /usr/src/app/node_modules ./node_modules

COPY . .

EXPOSE 7000

ENTRYPOINT [ "node", "server.js" ]
