FROM debian:buster-slim

ENV ROOT_HOME="/root"
ADD .bashrc ${ROOT_HOME}/.bashrc

# Avoid warnings by switching to noninteractive
ENV DEBIAN_FRONTEND=noninteractive

ARG USERNAME=vscode
ARG USER_UID=1000
ARG USER_GID=$USER_UID

# Configure apt and install packages
RUN apt-get update \
    && apt-get -yq install --no-install-recommends \
    # Core
    ssh-client locales gcc lib32stdc++6 \
    iproute2 procps apt-utils dialog  \
    # Core Dev Tools
    wget curl git unzip xz-utils \
    # Docker Dependencies
    apt-transport-https apt-utils software-properties-common \
    lsb-release gnupg2 \
    # Python Dependencies
    make build-essential libssl-dev zlib1g-dev libbz2-dev \
    libreadline-dev llvm libncurses5-dev libncursesw5-dev \
    tk-dev libffi-dev liblzma-dev python-openssl \
    2>&1

#
# Create a non-root user to use if preferred - see https://aka.ms/vscode-remote/containers/non-root-user.
RUN groupadd --gid $USER_GID $USERNAME \
    && useradd -s /bin/bash --uid $USER_UID --gid $USER_GID -m $USERNAME \
    # [Optional] Add sudo support for the non-root user
    && apt-get install -y sudo \
    && echo $USERNAME ALL=\(root\) NOPASSWD:ALL > /etc/sudoers.d/$USERNAME\
    && chmod 0440 /etc/sudoers.d/$USERNAME

# Authorize SSH Host
RUN mkdir -p /root/.ssh && \
    chmod -R 0600 /root/.ssh && \
    ssh-keyscan github.com > /root/.ssh/known_hosts

#
# Install Python 2 & 3
#apt-get -yq install --no-install-recommends \
# python-pip \
#    python3-pip python3-venv \
RUN curl -k https://pyenv.run | bash \
    && export PATH="/root/.pyenv/bin:$PATH" \
    # && exec $SHELL \
    && eval "$(/root/.pyenv/bin/pyenv init -)" \
    && eval "$(/root/.pyenv/bin/pyenv virtualenv-init -)" \
    && pyenv update \
    && pyenv install 3.8.2 \
    && pyenv global 3.8.2 \
    && echo "export PATH=\"/root/.pyenv/bin:\$PATH\"" >> /home/$USERNAME/.bashrc \
    && echo "export PATH=\"/root/.pyenv/bin:\$PATH\"" >> /root/.bashrc \
    && echo "eval \"\$(pyenv init -)\"" >> /home/$USERNAME/.bashrc \
    && echo "eval \"\$(pyenv init -)\"" >> /root/.bashrc \
    2>&1


#
# Install Azure Functions, .NET Core, and Azure CLI
RUN echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $(lsb_release -cs) main" > /etc/apt/sources.list.d/azure-cli.list \
    && echo "deb [arch=amd64] https://packages.microsoft.com/repos/microsoft-debian-$(lsb_release -cs)-prod $(lsb_release -cs) main" > /etc/apt/sources.list.d/dotnetdev.list \
    && curl -sL https://packages.microsoft.com/keys/microsoft.asc | (OUT=$(apt-key add - 2>&1) || echo $OUT) \
    && apt-get update \
    && apt-get -yq install --no-install-recommends \
    azure-cli dotnet-sdk-3.1 azure-functions-core-tools-3

#
# Install Docker CE CLI (needed for publish with --build-native-deps)
RUN apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common lsb-release \
    && curl -fsSL https://download.docker.com/linux/$(lsb_release -is | tr '[:upper:]' '[:lower:]')/gpg | apt-key add - 2>/dev/null \
    && add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/$(lsb_release -is | tr '[:upper:]' '[:lower:]') $(lsb_release -cs) stable" \
    && apt-get update \
    && apt-get install -y docker-ce-cli \
    #
    # Install Docker Compose
    && curl -sSL "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose \
    && chmod +x /usr/local/bin/docker-compose

#
# Clean up
RUN apt-get autoremove -y \
    && apt-get clean -y \
    && rm -rf /var/lib/apt/lists/*


# Switch back to dialog for any ad-hoc use of apt-get
ENV DEBIAN_FRONTEND=
