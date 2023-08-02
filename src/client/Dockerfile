# Stage 1: Build the Angular application
FROM node:18.10 as build
WORKDIR /app
COPY package.json package-lock.json ./
RUN npm ci
COPY . .
RUN npm run build --prod

# Stage 2: Set up Nginx
FROM nginx:1.21
COPY --from=build /app/dist/client/ /usr/share/nginx/html
COPY nginx.conf /etc/nginx/conf.d/default.conf
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
