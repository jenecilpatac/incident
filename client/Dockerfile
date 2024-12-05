# Base Stage
FROM node:18 AS base
WORKDIR /app
RUN npm i -g pnpm
COPY package.json pnpm-lock.yaml ./

RUN pnpm install

COPY . .

# Build the Next.js application
RUN pnpm build

# Release Stage
FROM node:18-alpine3.19 as release
WORKDIR /app
RUN npm i -g pnpm

# Copy necessary files from the base stage
COPY --from=base /app/node_modules ./node_modules
COPY --from=base /app/package.json ./package.json
COPY --from=base /app/.next ./.next
COPY --from=base /app/src ./src

# Expose the application port
EXPOSE 5005

# Start the application in development mode
CMD ["pnpm", "dev"]
