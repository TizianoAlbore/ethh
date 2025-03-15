FROM ubuntu:latest

RUN apt-get update && \
    apt-get install -y bind9 && \
    apt-get clean

# Copia i file di configurazione in /etc/bind
COPY named.conf /etc/bind/named.conf
COPY db.lab.local /etc/bind/db.lab.local

# Avvio di Bind in foreground (perché Docker vuole un processo in primo piano)
CMD ["named", "-c", "/etc/bind/named.conf", "-g"]
