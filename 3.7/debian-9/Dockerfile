FROM bitnami/minideb-extras:stretch-r321
LABEL maintainer "Bitnami <containers@bitnami.com>"

ENV BITNAMI_PKG_CHMOD="-R g+rwX" \
    BITNAMI_PKG_EXTRA_DIRS="/opt/bitnami/rabbitmq /opt/bitnami/rabbitmq/.rabbitmq" \
    HOME="/opt/bitnami/rabbitmq/.rabbitmq" \
    NAMI_PREFIX="/.nami"

# Install required system packages and dependencies
RUN install_packages libc6 libssl1.1 libtinfo5 zlib1g
RUN bitnami-pkg install erlang-21.3.0-0 --checksum 0d86bd202d7d208fc32032716b7e954af3104ee3a4040ef2befba3b59a89d652
RUN bitnami-pkg unpack rabbitmq-3.7.13-0 --checksum 57fb0ae7359eea199a1f5ba4206e671bc357db0c7e80944ce5ecf9ef44fca045
RUN mkdir -p /opt/bitnami/rabbitmq/.rabbitmq && mkdir -p /opt/bitnami/rabbitmq/var/log/rabbitmq && chmod g+rwX -R /opt/bitnami/rabbitmq/.rabbitmq /opt/bitnami/rabbitmq/var

COPY rootfs /
ENV BITNAMI_APP_NAME="rabbitmq" \
    BITNAMI_IMAGE_VERSION="3.7.13-debian-9-r16" \
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
ENTRYPOINT [ "/app-entrypoint.sh" ]
CMD [ "nami", "start", "--foreground", "rabbitmq" ]
