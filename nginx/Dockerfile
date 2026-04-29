FROM nginxinc/nginx-unprivileged:1-alpine-slim

ENV NGINX_ENTRYPOINT_WORKER_PROCESSES_AUTOTUNE=true
COPY nginx.conf /etc/nginx/nginx.conf
