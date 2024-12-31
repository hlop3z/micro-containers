# =======================================================================================
# Stage 1: Builder — Build the `Application`
# =======================================================================================
FROM rust:latest AS builder

# Set the working directory for the build process
WORKDIR /usr/src/app

# Copy the entire project into the container
COPY . .

# Add the MUSL target for static linking
RUN rustup target add x86_64-unknown-linux-musl

# Install necessary tools for MUSL cross-compilation
RUN apt-get update && apt-get install -y musl-tools

# Compile the Rust project in release mode for optimized performance
RUN cargo build --release --target x86_64-unknown-linux-musl

# =======================================================================================
# Stage 2: Runtime — Create a minimal image for the `Application`
# =======================================================================================
FROM scratch

# Copy the statically compiled binary from the builder stage into the runtime image
COPY --from=builder /usr/src/app/target/x86_64-unknown-linux-musl/release/rust_docker /app

# Specify the command to execute the binary when the container runs
CMD ["/app"]
