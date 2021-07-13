FROM node:lts-alpine3.14 as builder

RUN apk add --no-cache python3 make g++ git

WORKDIR /app

RUN git clone https://github.com/zone-eu/zone-mta-template ./

RUN yarn add zone-mta zonemta-wildduck
RUN yarn install --production --network-timeout 100000 && yarn cache clean


FROM node:lts-alpine3.14 as app

ENV NODE_ENV production

WORKDIR /app
COPY --from=builder /app /app

ENTRYPOINT ["node", "index.js"]
CMD ["--config=config/zonemta.toml"]
