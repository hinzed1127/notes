# build stage
# FROM node:12-stretch
FROM node:12-stretch AS builder
WORKDIR /app
COPY . .
RUN npm ci && npm run build

# nginx serve stage
FROM nginx:1.17
# COPY --from=0 /app/build /usr/share/nginx/html
COPY --from=builder /app/build /usr/share/nginx/html

# docker run --init --rm -p 8080:80 my-cra
