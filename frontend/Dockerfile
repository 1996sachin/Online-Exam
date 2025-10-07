# Use a lightweight Node image for build
FROM node:20-alpine AS build

WORKDIR /usr/src/app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy all source files and build
COPY . .
RUN npm run build

# Use a small web server image to serve static files
FROM nginx:alpine

# Copy build output to nginx html folder
COPY --from=build /usr/src/app/build /usr/share/nginx/html

# Expose port 80
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
