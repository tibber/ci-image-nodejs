FROM cimg/node:24.13@sha256:5d77ee6db8cb46bc53f329d94d84cc7afa8c522e34729abf79026085971c26b9

RUN sudo apt-get update && \
    sudo apt-get -y install gettext-base && \
    sudo rm -rf /var/lib/apt/lists/*

# Install kiota (default version; consumers can override by installing a different version in their CI step)
# renovate: datasource=github-releases depName=microsoft/kiota
ENV KIOTA_VERSION=v1.30.0
RUN curl -sSL https://github.com/microsoft/kiota/releases/download/${KIOTA_VERSION}/linux-x64.zip -o kiota.zip && \
    sudo unzip -o kiota.zip -d /usr/local/bin && \
    sudo chmod +x /usr/local/bin/kiota && \
    rm -f kiota.zip

# Install pnpm via corepack
RUN corepack enable --install-directory ~/bin && \
    pnpm config set store-dir .pnpm-store
