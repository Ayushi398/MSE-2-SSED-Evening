# ──────────────────────────────────────────────
# TaskFlow Backend – Production Dockerfile
# ──────────────────────────────────────────────
FROM node:20-alpine

# Set working directory
WORKDIR /app

# Set NODE_ENV to production
ENV NODE_ENV=production

# Copy package files first for better layer caching
COPY package.json ./

# Install production dependencies only
RUN npm install --omit=dev

# Copy application source (avoid copying unnecessary files via .dockerignore)
COPY src/ ./src/

# Run as non-root user for security
USER node

# Expose the backend application port
EXPOSE 3000

# Start the backend server
CMD ["node", "src/server.js"]
