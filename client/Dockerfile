# Use an official Node runtime as a parent image
FROM node:18-alpine AS build

# Set the working directory
WORKDIR /app

# Install pnpm globally
RUN npm install -g pnpm

# Copy the package.json and package-lock.json to the working directory
COPY ./package*.json ./

# Install the dependencies
RUN pnpm install

# Copy the remaining application files to the working directory
COPY . .

# Build the application
RUN npm run build

# Use a lightweight server to serve the static files
FROM nginx:alpine

# Assuming the build output is in .next directory
COPY ./.next /app/.next

# Copy the NGINX configuration file
COPY default.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 5005

# Start NGINX
CMD ["nginx", "-g", "daemon off;"]
