FROM alpine
RUN apk update && \
    apk add util-linux && \
    rm -rf /var/cache/apk/*
ENTRYPOINT ["nsenter", "--target", "1", "--mount", "--uts", "--ipc", "--net", "--pid"]