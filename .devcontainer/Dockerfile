FROM mcr.microsoft.com/devcontainers/base:ubuntu

# Install pixi, uv, and opencode system-wide (/usr/local/bin) so the vscode user can run them
ENV PIXI_HOME=/usr/local
ENV UV_INSTALL_DIR=/usr/local/bin
RUN curl -fsSL https://pixi.sh/install.sh | bash \
    && curl -LsSf https://astral.sh/uv/install.sh | sh \
    && curl -fsSL https://opencode.ai/install | bash -s -- --no-modify-path \
    && mv /root/.opencode/bin/opencode /usr/local/bin/opencode \
    && rm -rf /root/.opencode \
    && echo 'eval "$(pixi completion --shell bash)"' >> /etc/bash.bashrc \
    && echo 'eval "$(pixi completion --shell zsh)"'  >> /etc/zsh/zshrc \
    && echo 'eval "$(uv generate-shell-completion bash)"' >> /etc/bash.bashrc \
    && echo 'eval "$(uv generate-shell-completion zsh)"'  >> /etc/zsh/zshrc \
    && chsh -s /usr/bin/zsh vscode

# Point opencode at the class LiteLLM gateway. The key comes from the
# LITELLM_API_KEY env var (set it as a Codespaces secret).
COPY opencode.json /etc/opencode/opencode.json
ENV OPENCODE_CONFIG=/etc/opencode/opencode.json
