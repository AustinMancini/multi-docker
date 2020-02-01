# Production Dockerfile
FROM node:alpine as builder
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY . .
RUN npm run build

FROM nginx
EXPOSE 3000

# overwrite the existing default.conf file
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

# copy production assests from the builder phase
COPY --from=builder /app/build /usr/share/nginx/html