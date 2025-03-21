Unfortunately docker bridge network doesn't allow ARP requests so we have to set up a macvlan network

For accessing this network (therefore the webapps) we have to set up a macvlan interface on our machine

```
# Create macvlan interface "macvlan0", change eth0 with your correct interface
sudo ip link add macvlan0 link eth0 type macvlan mode bridge

# Assign an IP that is not used, for ex 192.168.56.50
sudo ip addr add 192.168.56.50/24 dev macvlan0

# Activate the interface
sudo ip link set macvlan0 up

# Activate promiscuos mode (change eth0 with your correct interface)
sudo ip link set eth0 promisc on
```

after doing so the containers are accessible from their own ip address:
192.168.56.101:3000 (Fedora)
192.168.56.80:8080/vnc.html (Kali)
