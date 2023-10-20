FROM ubuntu:22.04

RUN apt update &&\
    apt upgrade -y &&\
    apt install -y curl git jq libicu70 wget apt-transport-https software-properties-common

RUN wget -q https://packages.microsoft.com/config/ubuntu/22.04/packages-microsoft-prod.deb &&\
    dpkg -i packages-microsoft-prod.deb &&\
    rm packages-microsoft-prod.deb &&\
    apt update &&\
    apt-get install -y powershell &&\
    pwsh -Command "Install-Module -Name Az -Repository PSGallery -Force"

RUN mkdir -p /etc/apt/keyrings &&\
    curl -sLS https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor | tee /etc/apt/keyrings/microsoft.gpg > /dev/null &&\
    chmod go+r /etc/apt/keyrings/microsoft.gpg &&\
    echo "deb [arch=`dpkg --print-architecture` signed-by=/etc/apt/keyrings/microsoft.gpg] https://packages.microsoft.com/repos/azure-cli/ $(lsb_release -cs) main" | tee /etc/apt/sources.list.d/azure-cli.list &&\
    apt-get update &&\
    apt-get install azure-cli

# Also can be "linux-arm", "linux-arm64".
ENV TARGETARCH="linux-x64"

WORKDIR /azp/

COPY ./start.sh ./
RUN chmod +x ./start.sh

ENTRYPOINT ./start.sh
