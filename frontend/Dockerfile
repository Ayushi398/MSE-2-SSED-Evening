# ──────────────────────────────────────────────
# TaskFlow Frontend – Multi-stage Dockerfile
# ──────────────────────────────────────────────

# Stage 1: Build the React/Vite application
FROM node:20-alpine AS build

WORKDIR /app

# Copy package files for layer caching
COPY package.json ./

# Install all dependencies (including dev, needed for build)
RUN npm install

# Copy source files
COPY . .

# Build the production static assets
RUN npm run build

# Stage 2: Serve with Nginx (lightweight production runtime)
FROM nginx:alpine

# Copy custom nginx configuration
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copy only the production build artifacts from the build stage
COPY --from=build /app/dist /usr/share/nginx/html

# Expose the application port
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]
