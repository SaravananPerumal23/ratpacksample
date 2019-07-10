FROM jenkins/jenkins:lts

# Set user root to allow us to install the rest of what's needed
USER root

RUN wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub \
    | apt-key add - \
    && apt-get -qy update \
    && apt-get install -y libappindicator3-1 libasound2 libnspr4 libnss3 libxss1 lsb-release xdg-utils fonts-liberation \
    && wget -q https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb \
    && dpkg -i ./google-chrome*.deb

# Go back to non-sudo user
USER jenkins