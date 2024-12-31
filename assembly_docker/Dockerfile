# =======================================================================================
# Stage (Builder) — 1
# =======================================================================================
FROM debian:stable-slim AS build
WORKDIR /opt
RUN apt update -y && apt install make yasm binutils -y
COPY . .

# Build binary
RUN make release

# =======================================================================================
# Stage (Runtime) — 2
# =======================================================================================
FROM scratch

# Copy binary
COPY --from=build /opt/asmttpd /
COPY --from=build /opt/web_root /web_root

# Expects web_root to be mounted at runtime
ENTRYPOINT ["/asmttpd"]
CMD ["/web_root", "80"]