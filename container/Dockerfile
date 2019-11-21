FROM debian:stretch

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y vim \
                          git \
                          netcat-openbsd

#RUN adduser --uid 1000 user
RUN adduser --disabled-login --system --shell /bin/false --uid 1000 user

COPY --from=gcr.io/google_containers/pause-amd64:3.1 /pause /

ADD ssh_config /home/user/.ssh/config

USER user

ENTRYPOINT ["/pause"]
