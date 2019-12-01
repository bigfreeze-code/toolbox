FROM ubuntu:19.10

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y vim \
                          git \
                          docker.io \
                          docker-compose \
                          netcat-openbsd

#RUN adduser --uid 1000 user
RUN addgroup --gid 970 docker-ext
RUN adduser --disabled-login --system --shell /bin/false --uid 1000  user \
    && usermod -G docker user \
    && usermod -G docker-ext user

COPY --from=gcr.io/google_containers/pause-amd64:3.1 /pause /

ADD ssh_config /home/user/.ssh/config
ADD gitconfig /home/user/.gitconfig

USER user

ENTRYPOINT ["/pause"]
