## Overview

Due to limitations with the Docker bridge network not allowing ARP requests, we must set up a macvlan network. This configuration allows direct access to the web applications running in the containers via their own IP addresses.

## Prerequisites

- **Docker** must be installed.
- **Docker Compose** must be installed.

## First Time Setup

1. **Build and Start the Containers:**

   Run the following command to build the containers and start them in detached mode:

   ```bash
   docker-compose build && docker-compose up -d
   ```

2. **Set Up the Macvlan Network:**

    To access the network (and thus the web apps), you need to create a macvlan interface on your machine. Replace eth0 with the appropriate interface for your system if necessary.

    ```bash
    # Create the macvlan interface "macvlan0"
    sudo ip link add macvlan0 link eth0 type macvlan mode bridge

    # Assign an unused IP address (e.g., 192.168.56.50)
    sudo ip addr add 192.168.56.50/24 dev macvlan0

    # Activate the macvlan interface
    sudo ip link set macvlan0 up

    # Enable promiscuous mode on your main interface (replace eth0 with your correct interface)
    sudo ip link set eth0 promisc on
    ```

## Accessing the Containers

After configuring the macvlan network, the containers will be accessible via their dedicated IP addresses:

    Fedora: http://192.168.56.101:3000
    Kali: http://192.168.56.80:8080/vnc.html

## Shutting Down the Containers
To stop the containers, run:
```bash
docker-compose down
```

## Kali Password Configuration

The default password for Kali is set to kalilinux. If you encounter issues with the second login (the OS login) via terminal while the container is running, you can change the password as follows:

1. **Open a bash session in the Kali container:**
```bash
docker exec -it eth-kali-1 /bin/bash
```
2. **Change the Kali user password:**
```bash
sudo passwd kali
```
- Wait for the prompt to enter a new password.
- Wait for the prompt to confirm the new password.
