FROM golang:1.27-bookworm@sha256:4fa7c968ba93f1635670522dbb01a2c78150443e1385746924566079f36570ea

WORKDIR /usr/src/app

COPY go.mod go.sum /usr/src/app/
COPY pkg /usr/src/app/pkg
COPY besu_bootstrap/ /usr/src/app/besu_bootstrap
RUN go build -o /usr/local/bin/besu_bootstrap ./besu_bootstrap

ENTRYPOINT [ "/usr/local/bin/besu_bootstrap" ]
