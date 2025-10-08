# ---- Stage 1: Build ----
FROM node:20-alpine AS build

WORKDIR /usr/src/app

# Copy package files
COPY package*.json ./

# Install all dependencies (including devDependencies)
RUN npm install --legacy-peer-deps --no-audit --no-fund

# Copy source files
COPY . .

# Build React app
RUN npx react-scripts build

# ---- Stage 2: Serve with Nginx ----
FROM nginx:alpine
COPY --from=build /usr/src/app/build /usr/share/nginx/html
EXPOSE 3000
CMD ["nginx", "-g", "daemon off;"]