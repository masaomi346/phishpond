# Dockerfile pulled from sprintcube/docker-compose-lamp
FROM mitmproxy/mitmproxy:12.1.2
RUN apt update && apt install -y bash vim && \
    mkdir /home/mitmproxy/logs && \
    chmod -R 777 /home/mitmproxy/.mitmproxy /home/mitmproxy/logs 
COPY addons /home/mitmproxy/addons/ 
