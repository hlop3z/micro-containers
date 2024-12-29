# =======================================================================================
# Stage (Builder): Base Image
# =======================================================================================
FROM alpine:latest AS builder

# Install prerequisites for building Rust
RUN apk add --no-cache wget curl bash gcc libc-dev

# Install Rust using Rustup
RUN wget https://sh.rustup.rs -O rustup-init.sh && \
    chmod +x rustup-init.sh && \
    ./rustup-init.sh -y && \
    rm rustup-init.sh

# Add Rust to PATH
ENV PATH="/root/.cargo/bin:$PATH"

# Copy your Rust source code into the builder image
WORKDIR /usr/src/app
COPY . .

# Build your Rust project (release mode for optimized binary)
RUN cargo build --release 

# =======================================================================================
# Stage (Runtime): Apps Image
# =======================================================================================
FROM alpine:latest

# Install dependencies needed for running Rust applications
RUN apk add --no-cache libc6-compat

# Copy the built Rust binary from the builder stage
COPY --from=builder /usr/src/app/target/release/rust_docker .

# =======================================================================================
# Stage (Clean-Up): Remove unnecessary files in the runtime image
# =======================================================================================
RUN rm -rf /usr/share/man /usr/share/doc /usr/share/info /tmp/* /var/cache/apk/* /root/.cache/* /var/log/*

# =======================================================================================
# Start App
# =======================================================================================

# Set the command to run the binary (replace with your binary name)
CMD ["./rust_docker"]
