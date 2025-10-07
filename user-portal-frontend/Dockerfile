# ---- Stage 1: Build ----
FROM node:20-alpine AS build

WORKDIR /usr/src/app

# Copy only package files first (for caching)
COPY package*.json ./

# Faster, safer install (fixes ERESOLVE + skips audit/fund)
RUN npm ci --legacy-peer-deps --no-audit --no-fund

# Copy the rest of the app
COPY . .

# Build the app
RUN npm run build

# ---- Stage 2: Nginx ----
FROM nginx:alpine
COPY --from=build /usr/src/app/build /usr/share/nginx/html
EXPOSE 3000
CMD ["nginx", "-g", "daemon off;"]
