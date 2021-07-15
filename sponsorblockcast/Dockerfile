ARG BUILD_FROM
FROM $BUILD_FROM

ARG TARGETOS
ARG TARGETARCH
ARG TARGETVARIANT

RUN apk --no-cache add jq bc grep curl \
  && GC_URL=`wget https://api.github.com/repos/vishen/go-chromecast/releases/latest -O - | jq -r '.assets[].browser_download_url' | grep ${TARGETOS}_${TARGETARCH}${TARGETVARIANT}` \
  && wget $GC_URL -O /root/go-chromecast.tgz \
  && tar xzf /root/go-chromecast.tgz -C /usr/bin \
  && rm -rf /root/* \
  && chmod +x /usr/bin/go-chromecast

ENV SBCPOLLINTERVAL 1
ENV SBCSCANINTERVAL 300
ENV SBCCATEGORIES sponsor
ENV SBCDIR /tmp/sponsorblockcast

ADD sponsorblockcast.sh /usr/bin/sponsorblockcast

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
