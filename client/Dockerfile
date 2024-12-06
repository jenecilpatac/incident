# Use an official Node runtime as a parent image
FROM node:18-alpine AS build

# Install pnpm globally
RUN npm install -g pnpm

# Set the working directory
WORKDIR /app

# Copy the package.json and pnpm-lock.yaml to the working directory
COPY ./package*.json ./
COPY ./pnpm-lock.yaml ./

# Install the dependencies using pnpm
RUN pnpm install

# Copy the remaining application files to the working directory
COPY . .

# Build the application using pnpm
RUN pnpm run build

# Use a lightweight server to serve the static files
FROM nginx:alpine

# Copy the build files from the first stage to the NGINX server
COPY --from=build /app/.next /usr/share/nginx/html

# Copy the NGINX configuration file
COPY default.conf /etc/nginx/conf.d/default.conf

# Expose port 80
EXPOSE 5006

# Start NGINX
CMD ["nginx", "-g", "daemon off;"]