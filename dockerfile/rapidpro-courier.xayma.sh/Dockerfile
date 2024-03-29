FROM debian:buster-slim

RUN set -ex \
    && addgroup --system courier \
    && adduser --system --ingroup courier courier

# Install ca-certificates so HTTPS works in general
RUN apt-get update && \
    apt-get install -y --no-install-recommends ca-certificates wget && \
    rm -rf /var/lib/apt/lists/*

ARG COURIER_REPO=nyaruka/courier
ENV COURIER_REPO=${COURIER_REPO}
ARG COURIER_VERSION=7.0.0
ENV COURIER_VERSION=${COURIER_VERSION}

RUN set -ex \
    && wget -O courier.tar.gz "https://github.com/$COURIER_REPO/releases/download/v${COURIER_VERSION}/courier_${COURIER_VERSION}_linux_amd64.tar.gz" \
    && mkdir /usr/local/src/courier \
    && tar -xzf courier.tar.gz -C /usr/local/src/courier \
    \
    # Just grab the binary and ignore the other packaged files
    && mv /usr/local/src/courier/courier /usr/local/bin/ \
    && rm -rf /usr/local/src/courier courier.tar.gz \
    && apt-get purge -y --auto-remove 

EXPOSE 8080

USER courier

ENTRYPOINT []
CMD ["courier"]
