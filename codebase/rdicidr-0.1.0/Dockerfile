FROM node:22 as builder

WORKDIR /app

COPY package.json ./

RUN --mount=type=cache,target=/root/.npm \
    npm install

COPY . .

RUN npm run build

FROM nginx:stable-alpine

WORKDIR /usr/share/nginx/html

COPY --from=builder /app/build .
COPY nginx.conf /etc/nginx/conf.d/default.conf

CMD ["nginx-debug", "-g", "daemon off;"]