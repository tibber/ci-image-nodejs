FROM cimg/node:24.13

RUN sudo apt-get update && \
    sudo apt-get -y install gettext-base && \
    sudo rm -rf /var/lib/apt/lists/*

# Install kiota
RUN curl -sSL https://github.com/microsoft/kiota/releases/latest/download/linux-x64.zip -o kiota.zip && \
    sudo unzip -o kiota.zip -d /usr/local/bin && \
    sudo chmod +x /usr/local/bin/kiota && \
    rm -f kiota.zip

# Install pnpm via corepack
RUN corepack enable --install-directory ~/bin && \
    pnpm config set store-dir .pnpm-store
