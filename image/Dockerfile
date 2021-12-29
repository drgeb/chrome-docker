FROM ubuntu:20.04

RUN apt-get update && apt-get clean && DEBIAN_FRONTEND="noninteractive" apt-get install -y \
    x11vnc \
    xvfb \
    fluxbox \
    wmctrl \
    wget \
    ntp \
    gnupg2 \
    && wget -q -O - https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add - \
    && echo "deb http://dl.google.com/linux/chrome/deb/ stable main" >> /etc/apt/sources.list.d/google.list \
    && apt-get update && apt-get -y install google-chrome-stable

RUN useradd apps \
    && mkdir -p /home/apps \
    && chown -v -R apps:apps /home/apps

RUN mkdir -p /etc/opt/chrome/policies && \
    mkdir /etc/opt/chrome/policies/managed && \
    mkdir /etc/opt/chrome/policies/recommended && \
    chmod -w /etc/opt/chrome/policies/managed && \
    touch /etc/opt/chrome/policies/managed/test_policy.json && \
    echo $'{ \n\
            "ExtensionInstallForcelist": [";https://client2.google.com/service/update2/crx"] } > /etc/opt/chrome/policies/managed/test_policy.json \n\
          }' >> /etc/opt/chrome/policies/managed/test_policy.json

COPY bootstrap.sh /

CMD '/bootstrap.sh'
