# Use Node for build stage
FROM node:20-alpine AS build

WORKDIR /usr/src/app

COPY package*.json ./
RUN npm install

COPY . .
RUN npm run build

# Use nginx for serving production build
FROM nginx:alpine

# Copy React build to nginx html folder
COPY --from=build /usr/src/app/build /usr/share/nginx/html

# Expose port 3000
EXPOSE 3000

# Start nginx
CMD ["nginx", "-g", "daemon off;"]
