# Frontend Dockerfile
FROM node:18-alpine AS builder

WORKDIR /app

# Copy package files
COPY /frontend/package*.json ./

# Install dependencies
RUN npm install

# Copy source and build
COPY /frontend/. ./
RUN npm run build

FROM nginx:alpine

# Copy the built application from the builder stage
# npm build outputs to /app/dist
COPY --from=builder /app/dist /usr/share/nginx/html   

# Copy custom Nginx configuration
COPY /nginx/nginx.conf /etc/nginx/conf.d/default.conf

# Expose port
EXPOSE 3000

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]