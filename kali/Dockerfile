FROM kalilinux/kali-rolling

# Aggiorna e installa il metapacchetto standard
RUN apt-get update && \
    apt-get install -y kali-linux-standard && \
    apt-get clean

# Imposta una shell di default
CMD ["/bin/bash"]
