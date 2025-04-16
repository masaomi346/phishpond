# Dockerfile pulled from sprintcube/docker-compose-lamp
FROM mitmproxy/mitmproxy:10.4.2
RUN apt update && apt install -y bash vim
RUN mkdir /home/mitmproxy/logs
RUN chmod -R 777 /home/mitmproxy/logs 
COPY addons /home/mitmproxy/addons/ 
