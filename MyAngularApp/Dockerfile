# Stage 1: Build the Angular application
FROM node:18-alpine as build
WORKDIR /app
COPY MyAngularApp/package.json MyAngularApp/package-lock.json ./
RUN npm install
COPY MyAngularApp/ .
RUN npm run build

# Stage 2: Serve the app with nginx
FROM nginx:alpine

# Remove the default nginx.conf
RUN rm /etc/nginx/conf.d/default.conf

# Copy the custom nginx.conf from your project
COPY MyAngularApp/nginx.conf /etc/nginx/conf.d/default.conf

# Copy the built app to the Nginx serve directory
COPY --from=build /app/dist/my-angular-app /usr/share/nginx/html

EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
