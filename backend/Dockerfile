# Use LTS Node.js version
FROM node:20-alpine

# Set working directory
WORKDIR /usr/src/app

# Copy package files first (for caching)
COPY package*.json ./

# Install dependencies
RUN npm install --production

# Copy rest of the app
COPY . .

# Expose backend port
EXPOSE 5000

# Start backend
CMD ["node", "app.js"]
