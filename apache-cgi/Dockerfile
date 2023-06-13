# podman build --tag apache-cgi:latest .
# podman run --rm -p 8080:80 --name apache-cgi apache-cgi:latest
# http://localhost:8080/cgi-bin/hello.py
#
# podman exec -it apache-cgi -- /bin/bash
# podman cp apache-cgi:/usr/local/apache2/conf/httpd.conf httpd.conf
# podman cp apache-cgi:/usr/local/apache2/cgi-bin/test-cgi test-cgi
FROM httpd

RUN apt update && apt install -y \
    python \
    nano \
    && rm -rf /var/lib/apt/lists/*

COPY httpd.conf /usr/local/apache2/conf/httpd.conf
COPY test-cgi /usr/local/apache2/cgi-bin/test-cgi
COPY hello.py /usr/local/apache2/cgi-bin/hello.py

RUN chmod -R 755 /usr/local/apache2/cgi-bin