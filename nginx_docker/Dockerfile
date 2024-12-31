# =======================================================================================
# Single-Stage: Install and Configure NGINX
# =======================================================================================
FROM nginx:alpine

# Optional: Copy custom NGINX configuration
# COPY server.conf /etc/nginx/nginx.conf

# Optional: Add HTML content
COPY site/index.html /usr/share/nginx/html/

# Expose HTTP port
EXPOSE 80

# Set the default command to start NGINX in the foreground
CMD ["nginx", "-g", "daemon off;"]


