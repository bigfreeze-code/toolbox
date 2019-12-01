FROM ubuntu:19.10

RUN apt-get update \
    && apt-get upgrade -y \
    && apt-get install -y vim \
                          git \
                          curl \
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
WORKDIR /home/user
ENV DOCKER_CLI_EXPERIMENTAL=enabled
ENV PATH="/home/user/bin:$PATH"
RUN mkdir -p /home/user/.docker/cli-plugins \
    && curl -Lo /home/user/.docker/cli-plugins/docker-buildx https://github.com/docker/buildx/releases/download/v0.3.1/buildx-v0.3.1.linux-amd64 \
    && chmod a+x /home/user/.docker/cli-plugins/docker-buildx \
    && mkdir -p /home/user/bin \
    && curl -sL https://taskfile.dev/install.sh | sh

ENTRYPOINT ["/pause"]
