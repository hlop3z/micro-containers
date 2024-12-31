# =======================================================================================
# Stage (Builder): Base Image
# =======================================================================================
FROM golang:latest AS builder

# Set the working directory for the Go application
WORKDIR /usr/src/app

# Copy Go source code into the builder image
COPY . .

# Build the Go application (in release mode, optimally)
RUN go mod tidy
RUN GOOS=linux GOARCH=amd64 CGO_ENABLED=0 go build -ldflags "-s -w" -o go_docker .

# =======================================================================================
# Stage 2: Runtime — Create a minimal image for the `Application`
# =======================================================================================
FROM scratch

# Copy the statically compiled binary from the builder stage into the runtime image
COPY --from=builder /usr/src/app/go_docker ./app

# Specify the command to execute the binary when the container runs
CMD ["/app"]
