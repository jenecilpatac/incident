# Build stage
FROM node:18 as build
WORKDIR /app

# Copy files
COPY . .

# First, install with npm (if necessary for some compatibility)
RUN npm install

# Now, install dependencies with pnpm
RUN pnpm install

# Run the build
RUN pnpm run build

# Production stage (SSR with Next.js)
FROM node:18 as production
WORKDIR /app
COPY --from=build /app /app
EXPOSE 5006
CMD ["pnpm", "start"]
