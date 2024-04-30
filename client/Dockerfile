FROM node:alpine as builder
WORKDIR '/app'
COPY ./package.json ./
RUN npm install
COPY . .
RUN npm run build


FROM nginx
EXPOSE 3000

# Copy our Nginx config file to the container and overwrite the existing file
COPY ./nginx/default.conf /etc/nginx/conf.d/default.conf

# Copy previously created build folder that contains our application to Nginx default website file path
COPY --from=builder /app/build /usr/share/nginx/html
