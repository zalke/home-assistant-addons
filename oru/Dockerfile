FROM debian:buster

USER root
RUN apt-get update && apt-get upgrade -yq
RUN apt-get install python3 python3-pip jq nano -y

# Install chrome and dependencies
RUN "apt-get update && apt-get install -y \
    apt-transport-https \
    ca-certificates \
    curl \
    gnupg \
    chromium-browser \
    --no-install-recommends"

# Chrome won't run from the root user.
RUN groupadd chrome && useradd -g chrome -s /bin/bash -G audio,video chrome \
    && mkdir -p /home/chrome && chown -R chrome:chrome /home/chrome

COPY requirements.txt .
RUN pip3 install -r requirements.txt

COPY run.py .
COPY run.sh .

CMD cd / && chmod +x /run.sh && /run.sh
