ARG CADDY_VERSION
ARG CF_API_TOKEN

ENV CF_API_TOKEN

FROM caddy:${CADDY_VERSION}-builder AS builder

RUN --mount=type=cache,target=/go/pkg/mod \
    --mount=type=cache,target=/root/.cache/go-build \
    xcaddy build \
    --with github.com/greenpau/caddy-security \
    --with github.com/caddy-dns/cloudflare \
    --with github.com/mholt/caddy-l4 \
    --with github.com/WeidiDeng/caddy-cloudflare-ip \
    --with go.akpain.net/caddy-tailscale-auth

FROM caddy:${CADDY_VERSION}

COPY --from=builder /usr/bin/caddy /usr/bin/caddy