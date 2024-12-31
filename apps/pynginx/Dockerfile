# =======================================================================================
# Single-Stage: Install and Configure NGINX
# =======================================================================================
# <alpine:latest> OR <nginx:alpine>
FROM alpine:latest 

# Python installation
RUN apk update && apk add --no-cache python3 nginx

# @ Settings
COPY production/default.conf /etc/nginx/http.d/default.conf

# Copy source code into the builder image
COPY ./main.py ./main.py

# =======================================================================================
# Stage (Clean-Up): Remove unnecessary files in the runtime image
# =======================================================================================
# RUN rm -rf /usr/share/man /usr/share/doc /usr/share/info /tmp/* /var/cache/apk/* /root/.cache/* 

# Add HTML content
COPY site/ /web

# Expose HTTP port
EXPOSE 80

# Set the default command to start NGINX in the foreground
CMD ["nginx", "-g", "daemon off;"]
