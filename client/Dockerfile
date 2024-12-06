# Build stage
FROM node:18 as build
WORKDIR /app

# Install pnpm globally
RUN npm install -g pnpm

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

# Install pnpm in the production image as well
RUN npm install -g pnpm

# Copy the build from the build stage
COPY --from=build /app /app

EXPOSE 5006

CMD ["pnpm", "start"]
