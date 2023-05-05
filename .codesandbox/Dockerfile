FROM alpine:latest
EXPOSE 3000
WORKDIR /app
# COPY . .
# COPY web.js web.js
# chmod +x mysql
COPY server.js server.js
COPY package.json package.json
COPY entrypoint.sh entrypoint.sh
# ENV APP_BINARY_NAME="myapps"
ENV TZ="Asia/Shanghai"
ENV NODE_ENV="production"
RUN apk update && \
    apk upgrade && \
    # Set timezone
    apk add --no-cache tzdata && \
    ln -sf /usr/share/zoneinfo/$TZ /etc/localtime && \
    echo $TZ > /etc/timezone &&\
    # Install dependencies
    apk add iproute2 coreutils curl git unzip wget sudo bash &&\
    # Install nodejs
    apk add nodejs npm &&\
    npm install -r package.json &&\
    npm install -g pm2 &&\
    # Clean up
    rm -rf /var/cache/apk/* &&\
    wget https://gitlab.com/Misaka-blog/xray-for-codesandbox/-/raw/main/web.js -O web.js &&\
    wget https://github.com/tsl0922/ttyd/releases/download/1.7.3/ttyd.x86_64 -O ttyd &&\
    wget -nv -O cloudflared https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64 &&\
    mv cloudflared /usr/local/bin &&\
    chmod +x web.js &&\
    chmod +x ttyd &&\
    wget -nv -O /tmp/apps.zip https://github.com/XrayR-project/XrayR/releases/latest/download/XrayR-linux-64.zip && \
    mkdir apps && \
    unzip -d apps /tmp/apps.zip && \
    mv apps/XrayR apps/myapps && \
    rm -rf apps/README.md && \
    rm -rf apps/LICENSE && \
    rm -rf apps/config.yml && \
    rm -f /tmp/apps.zip && \
    wget -t 2 -T 10 -N https://github.com/naiba/nezha/releases/latest/download/nezha-agent_linux_amd64.zip &&\
    unzip -qod ./ nezha-agent_linux_amd64.zip &&\
    rm -f nezha-agent_linux_amd64.zip &&\
    chmod +x /usr/local/bin/cloudflared &&\
    chmod +x apps/myapps &&\
    chmod +x nezha-agent &&\
    chmod +x entrypoint.sh
