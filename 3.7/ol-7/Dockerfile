FROM bitnami/oraclelinux-extras:7-r68
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV BITNAMI_PKG_CHMOD="-R g+rwX" \
    BITNAMI_PKG_EXTRA_DIRS="/opt/bitnami/rabbitmq /opt/bitnami/rabbitmq/.rabbitmq" \
    HOME="/opt/bitnami/rabbitmq/.rabbitmq" \
    NAMI_PREFIX="/.nami"

# Install required system packages and dependencies
RUN install_packages glibc ncurses-libs openssl-libs zlib
RUN bitnami-pkg install erlang-21.0.0-1 --checksum 9ad6d6426c031237e0f27d8462e37ed4295dce73056d056b6aa287fbc83335c4
RUN bitnami-pkg unpack rabbitmq-3.7.7-4 --checksum 9c3c613d86ad7f69c1092fc59b8306356e7f53fe9375611ae422f10188769d81
RUN mkdir -p /opt/bitnami/rabbitmq/.rabbitmq && mkdir -p /opt/bitnami/rabbitmq/var/log/rabbitmq && chmod g+rwX -R /opt/bitnami/rabbitmq/.rabbitmq /opt/bitnami/rabbitmq/var

COPY rootfs /
ENV BITNAMI_APP_NAME="rabbitmq" \
    BITNAMI_IMAGE_VERSION="3.7.7-ol-7-r34" \
    PATH="/opt/bitnami/erlang/bin:/opt/bitnami/rabbitmq/bin:/opt/bitnami/rabbitmq/sbin:$PATH" \
    RABBITMQ_CLUSTER_NODE_NAME="" \
    RABBITMQ_CLUSTER_PARTITION_HANDLING="ignore" \
    RABBITMQ_DISK_FREE_LIMIT="{mem_relative, 1.0}" \
    RABBITMQ_ERL_COOKIE="" \
    RABBITMQ_HASHED_PASSWORD="" \
    RABBITMQ_MANAGER_PORT_NUMBER="15672" \
    RABBITMQ_NODE_NAME="rabbit@localhost" \
    RABBITMQ_NODE_PORT_NUMBER="5672" \
    RABBITMQ_NODE_TYPE="stats" \
    RABBITMQ_PASSWORD="bitnami" \
    RABBITMQ_USERNAME="user" \
    RABBITMQ_VHOST="/"

EXPOSE 4369 5672 25672 15672

USER 1001
ENTRYPOINT ["/app-entrypoint.sh"]
CMD ["nami","start","--foreground","rabbitmq"]
