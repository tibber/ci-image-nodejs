FROM cimg/node:24.14@sha256:4d24911ec4872588300d27382c1765dbfd7a942ffd6c0d35d731002f948821bb

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

# Bun — run TypeScript in CI without a separate compile step (optional for consumers).
# renovate: datasource=github-releases depName=oven-sh/bun
ENV BUN_VERSION=1.3.10
ENV BUN_INSTALL=/usr/local/bun
ENV PATH="${BUN_INSTALL}/bin:${PATH}"
RUN sudo mkdir -p "${BUN_INSTALL}" && sudo chown circleci:circleci "${BUN_INSTALL}" && \
    curl -fsSL https://bun.sh/install | bash -s "bun-v${BUN_VERSION}" && \
    bun --version
