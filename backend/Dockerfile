# Backend Dockerfile
FROM node:18-alpine as builder

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies
RUN npm install --production

# Copy application source
COPY . .

# Expose port
EXPOSE 8000

# Start the application
CMD ["npm", "start"]

# Production stage - server with Nginx

FROM nginx:alpine

# Copy the built application from the builder stage
COPY --from=builder /app /usr/share/nginx/html

# Copy custom Nginx configuration
COPY /nginx/nginx.conf /etc/nginx/conf.d/default.conf

# Expose port
EXPOSE 80

# Start Nginx
CMD ["nginx", "-g", "daemon off;"]