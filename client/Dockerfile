# Stage 1: Build the Next.js app
FROM node:18-alpine AS builder

WORKDIR /app

# Copy package files and install dependencies
COPY package*.json ./
RUN npm install

# Copy all app files and build the Next.js app
COPY . . 
RUN npm run build

# Stage 2: Production-ready Next.js app (Running Next.js)
FROM node:18-alpine AS nextjs

WORKDIR /app

# Copy the built app from the builder stage
COPY --from=builder /app /app

# Set environment variable for production server
ENV PORT 5006

# Expose the port the app runs on
EXPOSE 5006

# Start the Next.js app
CMD ["npm", "start"]

# Stage 3: Nginx to serve the app
FROM nginx:alpine AS nginx

# Copy the Nginx configuration file
COPY default.conf /etc/nginx/conf.d/default.conf

# Expose Nginx port
EXPOSE 5005

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
