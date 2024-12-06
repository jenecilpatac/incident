# Use a Node.js base image for building the app
FROM node:18 AS builder

# Set working directory
WORKDIR /app

# Copy package files
COPY package*.json ./
COPY pnpm-lock.yaml ./

# Install dependencies
RUN npm install -g pnpm && pnpm install

# Copy all files into the container
COPY . .

# Build the Next.js app (this will generate the .next folder)
RUN pnpm run build

# Use a minimal base image for the production stage
FROM node:18-alpine AS runner

# Set working directory
WORKDIR /app

# Copy build artifacts from the builder stage
COPY --from=builder /app/public ./public
COPY --from=builder /app/.next ./.next
COPY --from=builder /app/package.json ./package.json
COPY --from=builder /app/node_modules ./node_modules

# Expose port 3000 for the Next.js app
EXPOSE 5006

# Start the Next.js application
CMD ["npm", "run", "start"]
