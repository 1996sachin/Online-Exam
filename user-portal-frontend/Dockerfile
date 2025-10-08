# ---- Stage 1: Build React app ----
FROM node:20-alpine AS build

WORKDIR /usr/src/app

# Copy package files
COPY package*.json ./

# Install all dependencies including devDependencies
RUN npm install --legacy-peer-deps --no-audit --no-fund

# Copy source files
COPY . .

# Build the React app
RUN npx react-scripts build

# ---- Stage 2: Serve with Nginx ----
FROM nginx:alpine

# Remove default Nginx static files
RUN rm -rf /usr/share/nginx/html/*

# Copy build output from previous stage
COPY --from=build /usr/src/app/build /usr/share/nginx/html

# Expose port
EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]