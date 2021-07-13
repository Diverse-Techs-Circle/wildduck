FROM node:lts-alpine3.14 as builder

RUN apk add --no-cache python3 make g++ git

WORKDIR /app

RUN git clone https://github.com/haraka/Haraka.git ./

RUN yarn add haraka-plugin-wildduck
RUN yarn install --production --network-timeout 100000 && yarn cache clean


FROM node:lts-alpine3.14 as app

ENV NODE_ENV production

RUN apk --no-cache add --no-cache openssl

WORKDIR /app
COPY --from=builder /app /app

ENTRYPOINT ["node", "haraka.js"]
