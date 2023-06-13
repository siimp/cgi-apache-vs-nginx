# podman build --tag nginx-cgi:latest .
# podman run --rm -p 8080:80 --name nginx-cgi nginx-cgi:latest
# http://localhost:8080/cgi-bin/hello.py
#
# podman exec -it nginx-cgi /bin/bash
# from debian /usr/share/doc/fcgiwrap/examples/nginx.conf
# podman cp nginx-cgi:/etc/nginx/conf.d/default.conf default.conf
FROM nginx

RUN apt update && apt install -y \
    python \
    nano \
    fcgiwrap \
    && rm -rf /var/lib/apt/lists/*

RUN sed -i 's/www-data/nginx/g' /etc/init.d/fcgiwrap

COPY fcgiwrap.conf /etc/nginx/fcgiwrap.conf
COPY default.conf /etc/nginx/conf.d/default.conf
COPY hello.py /usr/lib/cgi-bin/hello.py
COPY test-cgi /usr/lib/cgi-bin/test-cgi

RUN chmod -R 755 /usr/lib/cgi-bin

COPY fcgiwrap-entrypoint.sh /docker-entrypoint.d/fcgiwrap-entrypoint.sh
RUN chmod +x /docker-entrypoint.d/fcgiwrap-entrypoint.sh