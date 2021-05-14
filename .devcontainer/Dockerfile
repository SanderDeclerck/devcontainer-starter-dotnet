FROM mcr.microsoft.com/vscode/devcontainers/base:0-focal

RUN rm /bin/sh && ln -s /bin/bash /bin/sh

USER vscode

# Install dotnet
WORKDIR /dotnet-install
RUN sudo wget https://download.visualstudio.microsoft.com/download/pr/cd855e4d-b02a-4327-b218-7ab500ecff83/c7649b00ee20e30244b8b84ff9139c71/dotnet-sdk-6.0.100-preview.3.21202.5-linux-x64.tar.gz

RUN mkdir -p $HOME/dotnet \
  && tar zxf dotnet-sdk-6.0.100-preview.3.21202.5-linux-x64.tar.gz -C $HOME/dotnet

RUN echo 'export DOTNET_ROOT=$HOME/dotnet' >> ~/.bashrc
RUN sudo ln -s /home/vscode/dotnet/dotnet /usr/bin/dotnet

# Install node
WORKDIR /node-install
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash \
  && source ~/.bashrc \
  && nvm install 14.17.0

# Install yarn
WORKDIR /yarn-install
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add - \
    && echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
RUN sudo apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && sudo apt-get -y install --no-install-recommends yarn