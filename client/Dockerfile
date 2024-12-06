# Use an official Node runtime as a parent image
FROM node:18-alpine AS build

# Install pnpm globally
RUN npm install -g pnpm

# Set the working directory
WORKDIR /app

# Copy the package.json and pnpm-lock.yaml to the working directory
COPY ./package*.json ./
COPY ./pnpm-lock.yaml ./

# Install dependencies using pnpm
RUN pnpm install

# Copy the remaining application files
COPY . .

# Build the Next.js app (static export)
RUN pnpm run build

# Use NGINX to serve the built static files
FROM nginx:alpine

# Copy the Next.js static files to the NGINX server's html directory
COPY --from=build /app/.next /usr/share/nginx/html

# Expose port 80 (standard for HTTP traffic)
EXPOSE 5006

# Start NGINX
CMD ["nginx", "-g", "daemon off;"]
