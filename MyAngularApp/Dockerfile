# Stage 1: Build the Angular application
FROM node:16-alpine as build
WORKDIR /app
COPY MyAngularApp/package.json MyAngularApp/package-lock.json ./
RUN npm install
COPY MyAngularApp/ .
RUN npm run build

# Stage 2: Serve the app with nginx
FROM nginx:alpine
COPY --from=build /app/dist/my-angular-app /usr/share/nginx/html
EXPOSE 8080

CMD ["nginx", "-g", "daemon off;"]
