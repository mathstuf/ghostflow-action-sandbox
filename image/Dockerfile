FROM rustlang/rust:nightly AS builder

# Install the ghostflow-cli tool.
RUN cargo +nightly install --root /usr/local --git https://gitlab.kitware.com/ben.boeckel/rust-ghostflow.git --branch ghostflow-cli

FROM alpine:3.10 AS runner

# Install git.
RUN apk add --no-cache --update-cache git

# Install glibc so we can run ghostflow-cli.
RUN apk add --no-cache --update-cache ca-certificates wget
RUN wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub
RUN wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.30-r0/glibc-2.30-r0.apk
RUN wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.30-r0/glibc-bin-2.30-r0.apk
RUN apk add glibc-2.30-r0.apk glibc-bin-2.30-r0.apk
RUN rm glibc-2.30-r0.apk glibc-bin-2.30-r0.apk

# Install ghostflow-cli from the builder.
COPY --from=builder /usr/local/bin/ghostflow-cli /usr/local/bin/ghostflow-cli
