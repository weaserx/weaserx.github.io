# Routing the WindowsVM VPN to Host without SOCKS

**File > Tools  > Network Manager** `Ctrl + H` for shortcut.

add a new Host-only network interface.

![Screenshot1](/ss/Pasted-image-20250822143608.png)

set adapter 1 to `NAT` connection

![Screenshot2](/ss/Pasted-image-20250822143800.png)

set adapter 2 to `Host-only` connection with created interface

![Screenshot3](/ss/Pasted-image-20250822143821.png)

run `ncpa.cpl`

![Screenshot](/ss/Pasted-image-20250822142552.png)

after we connected the we VPN we can see the following `Pulse Secure` interface in here

![Screenshot4](/ss/Pasted-image-20250822142617.png)

enter properties of VPN interface and turn on this checkbox with `Host-only` (Ethernet 3) interface

![Screenshot5](/ss/Pasted-image-20250822142713.png)

then go to `Host-only` interface's properties. and set the ip with `192.168.56.2` and subnet mask `255.255.255.0`

![Screenshot6](/ss/Pasted-image-20250822142818.png)

because we have the same subnet with `192.168.56.1` on `Host-only` interface in host machine 

```rb
ifconfig vboxnet0
```

![Screenshot7](/ss/Pasted-image-20250822142844.png)

in windows the final picture is like this:

- Ethernet 2 >  VPN
- Ethernet > NAT
- Ethernet 3 > Host-Only interface

![Screenshot8](/ss/Pasted-image-20250822143010.png)

now we need to route host's routes to the VPN tunnel

adding subnets (recommended option)

```rb
sudo ip route add 172.16.0.0/12 via 192.168.56.2
sudo ip route add 10.0.0.0/8 via 192.168.56.2
sudo ip route add 192.168.0.0/16 via 192.168.56.2
```

adding only one ip:

```rb
sudo ip route add 172.19.8.18/32 via 192.168.56.2
sudo ip route add 172.19.8.19/32 via 192.168.56.2
sudo ip route add 172.19.8.34/32 via 192.168.56.2
```

to route all traffic from VPN:

(ATTENTION!) routig all the traffic will delete your default routes. maybe you can not access your internal or the internet. But dont worry restart is the solution xD.

```rb
sudo ip route add default via 192.168.56.2
```
![Screenshot9](/ss/Pasted-image-20250822143351.png)


