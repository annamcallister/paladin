# Build the manager binary
FROM golang:1.27-bookworm@sha256:4fa7c968ba93f1635670522dbb01a2c78150443e1385746924566079f36570ea AS builder

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

FROM ubuntu:26.04@sha256:d66b366dac61b575bee2aef07e9c26e8070096fbe84a3d4d3eb0da069b5d76db
WORKDIR /
COPY --from=builder --chown=65532:65532 /workspace/operator/manager .
USER 65532:65532

ENTRYPOINT ["/manager"]
