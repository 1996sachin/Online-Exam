# ---- Stage 1: Build ----
FROM node:20-alpine AS build

WORKDIR /usr/src/app

# Copy package files first
COPY package*.json ./

# Install all dependencies (including dev) for build
RUN npm install --legacy-peer-deps --no-audit --no-fund

# Copy app source
COPY . .

# Build the React app
RUN npm run build

# ---- Stage 2: Nginx ----
FROM nginx:alpine
COPY --from=build /usr/src/app/build /usr/share/nginx/html
EXPOSE 3000
CMD ["nginx", "-g", "daemon off;"]