# # Stage 1: Build the Next.js app
# FROM node:18 AS builder

# # Set working directory
# WORKDIR /app

# # Copy package files
# COPY package*.json ./ 
# COPY pnpm-lock.yaml ./

# # Install dependencies
# RUN npm install -g pnpm && pnpm install

# # Copy application files
# COPY . .

# # Build the Next.js app
# RUN pnpm run build

# # Stage 2: Run the app
# FROM node:18-alpine AS runner

# # Set working directory
# WORKDIR /app

# # Copy build artifacts and dependencies from builder stage
# COPY --from=builder /app/public ./public
# COPY --from=builder /app/.next ./.next
# COPY --from=builder /app/package.json ./package.json
# COPY --from=builder /app/node_modules ./node_modules

# # Expose the desired port
# EXPOSE 5006

# # Set environment variables
# ENV NODE_ENV production

# # Start the application
# CMD ["next", "start", "-p", "5006"]

FROM node:18 AS build

WORKDIR /app

COPY package*.json ./
COPY pnpm-lock.yaml ./

RUN npm install -g pnpm && pnpm install

COPY . .

RUN pnpm run build

EXPOSE 5006
CMD ["pnpm", "run", "start", "-p", "5006"]


