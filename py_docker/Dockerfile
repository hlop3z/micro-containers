# =======================================================================================
# Stage (Builder): Base Image
# =======================================================================================
FROM alpine:latest AS builder

# Python installation
RUN apk update && apk add python3

# Copy Go source code into the builder image
COPY ./main.py ./main.py

# =======================================================================================
# Stage (Clean-Up): Remove unnecessary files in the runtime image
# =======================================================================================
RUN rm -rf /usr/share/man /usr/share/doc /usr/share/info /tmp/* /var/cache/apk/* /root/.cache/* /var/log/*

# =======================================================================================
# Start App
# =======================================================================================

# Set the command to run the binary (replace with your binary name)
CMD ["python", "main.py"]
