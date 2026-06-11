FROM registry.gitlab.steamos.cloud/steamrt/sniper/sdk:latest

WORKDIR /app

RUN apt update && apt install -y \
    build-essential \
    g++ \
    cmake \
    ninja-build \
    git \
    zlib1g \
    zlib1g-dev \
    libssl-dev \
    libprotobuf-dev \
    protobuf-compiler \
    pkg-config \
    libcurl4-openssl-dev \
    libmaxminddb-dev \
    curl \
    && curl -sSL https://dot.net/v1/dotnet-install.sh -o dotnet-install.sh \
        && chmod +x dotnet-install.sh \
        && ./dotnet-install.sh --channel 10.0 --install-dir /usr/share/dotnet \
        && rm dotnet-install.sh \
        && ln -sf /usr/share/dotnet/dotnet /usr/bin/dotnet

RUN git config --system --add safe.directory '*'

COPY docker/docker-entrypoint.sh ./docker-entrypoint.sh
RUN sed -i 's/\r$//' ./docker-entrypoint.sh && chmod +x ./docker-entrypoint.sh

WORKDIR /app/source

CMD ["/bin/bash", "../docker-entrypoint.sh"]