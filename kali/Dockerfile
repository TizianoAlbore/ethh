FROM kalilinux/kali-rolling

# Set the frontend to noninteractive to avoid prompts during build
ENV DEBIAN_FRONTEND=noninteractive

# Update and install the default Kali metapackage
RUN apt update && \
    apt full-upgrade -y && \
    apt install -y kali-linux-default

# Set default shell
CMD ["/bin/bash"]
