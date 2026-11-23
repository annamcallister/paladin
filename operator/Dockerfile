# Build the manager binary
FROM golang:1.26-bookworm@sha256:dc40a13b61304647ed7e5d581d246b86413dfc29d63c6d018310feb93cd98fc0 AS builder

WORKDIR /workspace

# We use Dockerfile.dockerignore to make this efficient
COPY . .

# Build
# TODO: Investigate if there is a need for cross-compilation, and if so we need to
#       wait to implement until the domain specific signer plugin interface 
#       is enabled, such that Zeto can remove non-cross-compilable ZKP libs
#       from the core build.
RUN cd operator; go build -a -o manager cmd/main.go

# TODO: Use distroless as minimal base image to package the manager binary
#       Depends on debugging/reconciling dependencies of operator
# FROM gcr.io/distroless/static:nonroot

FROM ubuntu:24.04@sha256:9c7f200c07e3d4a03e7249d2c16bf66a51120fb876aa2242cf31451412543289
WORKDIR /
COPY --from=builder --chown=65532:65532 /workspace/operator/manager .
USER 65532:65532

ENTRYPOINT ["/manager"]
