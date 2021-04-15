ARG BUILD_FROM=ghcr.io/hassio-addons/base/amd64:9.1.7
# hadolint ignore=DL3006
FROM ${BUILD_FROM}
ARG GC_BUILD=linux_armv7
ADD sponsorblockcast.sh /usr/bin/sponsorblockcast
RUN apk -U add jq bc grep curl \
  && GC_URL=`wget https://api.github.com/repos/vishen/go-chromecast/releases/latest -O - | jq -r '.assets[].browser_download_url' | grep $GC_BUILD` \
  && wget $GC_URL -O /root/go-chromecast.tgz \
  && tar xzf /root/go-chromecast.tgz -C /usr/bin \
  && chmod +x /usr/bin/sponsorblockcast \
  && chmod +x /usr/bin/go-chromecast \
  && rm -rf /var/cache/apk/* /lib/apk/db/* /root/*
ENV SBCPOLLINTERVAL 1
ENV SBCSCANINTERVAL 300
ENV SBCCATEGORIES sponsor
ENV SBCDIR /tmp/sponsorblockcast
# Build arguments
ARG BUILD_ARCH
ARG BUILD_DATE
ARG BUILD_DESCRIPTION
ARG BUILD_NAME
ARG BUILD_REF
ARG BUILD_REPOSITORY
ARG BUILD_VERSION
# Labels
LABEL \
    io.hass.name="${BUILD_NAME}" \
    io.hass.description="${BUILD_DESCRIPTION}" \
    io.hass.arch="${BUILD_ARCH}" \
    io.hass.type="addon" \
    io.hass.version=${BUILD_VERSION} \
    maintainer="Yaroslav Yadryshnikov <me@yay.qa>" \
    org.opencontainers.image.title="${BUILD_NAME}" \
    org.opencontainers.image.description="${BUILD_DESCRIPTION}" \
    org.opencontainers.image.vendor="Home Assistant Community Add-ons" \
    org.opencontainers.image.authors="Yaroslav Yadryshnikov <me@yay.qa>" \
    org.opencontainers.image.licenses="GNU" \
    org.opencontainers.image.url="https://addons.community" \
    org.opencontainers.image.source="https://github.com/${BUILD_REPOSITORY}" \
    org.opencontainers.image.documentation="https://github.com/${BUILD_REPOSITORY}/blob/main/README.md" \
    org.opencontainers.image.created=${BUILD_DATE} \
    org.opencontainers.image.revision=${BUILD_REF} \
    org.opencontainers.image.version=${BUILD_VERSION}
CMD /usr/bin/sponsorblockcast
