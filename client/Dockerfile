# Base Stage: Install dependencies and build the app
FROM node:18 AS build
WORKDIR /app
RUN npm install -g pnpm
COPY package.json pnpm-lock.yaml ./
RUN pnpm install
COPY . .
RUN pnpm build  # Build the Next.js application

# Production Stage: Serve pre-built Next.js
FROM node:18-alpine AS production
WORKDIR /app
RUN npm install -g pnpm
COPY --from=build /app/package.json ./package.json
COPY --from=build /app/.next ./.next
COPY --from=build /app/public ./public
COPY --from=build /app/node_modules ./node_modules

# Expose the application port
EXPOSE 5005

# Start the application in production mode
CMD ["pnpm", "start"]
