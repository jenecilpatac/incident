# Step 1: Use Node.js official image as the base image
FROM node:16-alpine AS build

# Step 2: Set the working directory
WORKDIR /app

# Step 3: Copy package.json and package-lock.json
COPY package*.json ./

# Step 4: Install dependencies
RUN npm install

# Step 5: Copy the rest of the application files
COPY . .

# Step 6: Build the NestJS application
RUN npm run build

# Step 7: Start the NestJS application (it listens on port 3000 by default)
CMD ["npm", "run", "start:prod"]

# Expose port 3000 for NestJS
EXPOSE 5006
