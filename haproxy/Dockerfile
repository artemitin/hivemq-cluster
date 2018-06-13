# Pull haproxy image. The official docker haproxy image is used here.
FROM haproxy:1.5

COPY haproxy.cfg /usr/local/etc/haproxy/haproxy.cfg 

# Define working directory
WORKDIR /etc/haproxy


# Expose ports
EXPOSE 80
EXPOSE 81
EXPOSE 1883
