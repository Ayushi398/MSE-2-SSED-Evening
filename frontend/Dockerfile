
# Stage 1: Build the frontend
FROM node:24-bookworm-slim AS build

WORKDIR /app

COPY package*.json ./
RUN npm ci


COPY . .
RUN npm run build

# Stage 2: Run using Nginx
FROM nginx:alpine

COPY nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/dist /usr/share/nginx/html

EXPOSE 80

CMD ["nginx", "-g", "daemon off;"]
