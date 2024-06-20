# FROM debian:stable-slim
# 
# ARG USER_UID
# ARG USER_GID
# 
# RUN groupadd -g ${USER_GID} gabo && useradd -u ${USER_UID} -g gabo -m gabo && usermod -p "*" gabo
# 
# RUN apt update && apt install -y curl git
# RUN curl -sL https://deb.nodesource.com/setup_18.x | bash
# RUN apt-get update && apt-get install -y nodejs && apt-get install -y nano cron && apt-get clean
# 
# RUN npm install --global yarn
# 
# RUN npm install -g eslint
# 
# RUN rm -rf /var/www/html
# 
# WORKDIR /var/www
FROM node:18.16-slim

RUN apt update && apt install -y wget ncat git git-flow chromium

USER node

WORKDIR /var/www

EXPOSE 8080 8081