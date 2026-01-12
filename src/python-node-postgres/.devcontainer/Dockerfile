FROM ubuntu:${templateOption:ubuntuVersion}

ENV DEBIAN_FRONTEND=noninteractive

ARG USERNAME=ubuntu
ARG PYTHON_VERSION=${templateOption:pythonVersion}
ARG NODE_VERSION=${templateOption:nodeVersion}
ARG PACKAGE_MANAGER=${templateOption:packageManager}

RUN apt update && apt install -y \
    git \
    curl \
    wget \
    ca-certificates \
    sudo \
    build-essential \
    gcc \
    python3-dev \
    just \
    && rm -rf /var/lib/apt/lists/*

RUN echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME \
    && chmod 0440 /etc/sudoers.d/$USERNAME

USER $USERNAME
WORKDIR /workspace

ENV PATH="$PATH:/home/ubuntu/.local/bin"

RUN curl https://mise.run/bash | sh
RUN curl -LsSf https://astral.sh/uv/install.sh | sh

RUN mise use -gy python@$PYTHON_VERSION
RUN mise use -gy node@$NODE_VERSION

RUN if [ "$PACKAGE_MANAGER" = "pnpm" ]; then \
      curl -fsSL https://get.pnpm.io/install.sh | sh -; \
    elif [ "$PACKAGE_MANAGER" = "yarn" ]; then \
      corepack enable && corepack prepare yarn@stable --activate; \
    elif [ "$PACKAGE_MANAGER" = "bun" ]; then \
      curl -fsSL https://bun.sh/install | bash; \
    fi

RUN if [ "$PACKAGE_MANAGER" = "bun" ]; then \
      echo 'export PATH="$HOME/.bun/bin:$PATH"' >> /home/ubuntu/.bashrc; \
      export PATH="$HOME/.bun/bin:$PATH"; \
    fi

RUN mise trust "/workspace"
