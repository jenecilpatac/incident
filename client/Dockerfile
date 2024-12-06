# Stage 1: Build the Next.js app
FROM node:18-alpine AS builder

WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy all app files and build the Next.js app
COPY . .
RUN npm run build

# Stage 2: Production-ready image
FROM node:18-alpine

WORKDIR /app

# Copy the built app from the builder stage
COPY --from=builder /app ./

# Set the environment variable for the production server
ENV PORT 5006

# Expose the desired port
EXPOSE 5006

# Run the Next.js app
CMD ["npm", "start"]

FROM nginx:alpine

# Copy the Nginx configuration
COPY default.conf /etc/nginx/conf.d/default.conf

# Expose the Nginx port
EXPOSE 5005

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]