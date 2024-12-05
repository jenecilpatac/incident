# Build stage
FROM node:18-alpine AS build

# Set the working directory
WORKDIR /app

# Install pnpm globally
RUN npm install -g pnpm

# Copy the package.json and package-lock.json to the working directory
COPY ./package*.json ./

# Install the dependencies using pnpm
RUN pnpm install

# Copy the remaining application files to the working directory
COPY . .

# Build the application using pnpm
RUN pnpm run build

# Nginx stage
FROM nginx:alpine

# Copy the built Next.js application files and static assets from the build stage
COPY --from=build /app/.next /app/.next
COPY --from=build /app/public /app/public

# Copy the NGINX configuration file
COPY default.conf /etc/nginx/conf.d/default.conf

# Expose port 5005
EXPOSE 5005

# Start NGINX
CMD ["nginx", "-g", "daemon off;"]
