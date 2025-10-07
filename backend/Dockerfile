k# Use Node 20
FROM node:20-alpine

# Set working directory
WORKDIR /usr/src/app

# Copy package.json and package-lock.json first (for caching)
COPY package*.json ./

# Install dependencies
RUN npm install --production

# Copy rest of the app
COPY . .

# Expose backend port (change if your app uses a different port)
EXPOSE 5000

# Start the backend
CMD ["node", "app.js"]
