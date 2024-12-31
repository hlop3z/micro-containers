# =======================================================================================
# Stage (Builder): Base Image
# =======================================================================================
FROM golang:latest AS builder

# Set the working directory for the Go application
WORKDIR /usr/src/app

# Copy Go source code into the builder image
COPY . .

# Build the Go application (in release mode, optimally)
RUN go mod tidy && CGO_ENABLED=0 go build -a --installsuffix cgo -o go_docker .

# =======================================================================================
# Stage (Runtime): Apps Image
# =======================================================================================
FROM busybox:latest

# Copy the built Go binary from the builder stage
COPY --from=builder /usr/src/app/go_docker .

# =======================================================================================
# Stage (Clean-Up): Remove unnecessary files in the runtime image
# =======================================================================================
RUN rm -rf /usr/share/man /usr/share/doc /usr/share/info /tmp/* /var/cache/apk/* /root/.cache/* /var/log/*

# =======================================================================================
# Start App
# =======================================================================================

# Set the command to run the binary (replace with your binary name)
CMD ["./go_docker"]

