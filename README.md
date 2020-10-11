# packet-manipulation
A library that enables to assemble from scratch, forge, dissect and send network packets.

### Protocols
The library supports the following protocols:
* Ethernet
* IPV4
* ARP
* ICMP
* UDP
* TCP
* DNS (query and response)

### Create Layers
Layer constructors contain only basic parameters, all other properties have defualt values and can be simply accessed manually through the instance.
```Python
from .layers import Types, Ethernet, IP, UDP, ARP, ICMP, Raw

# data samples
source_mac = 
dest_mac = 
dest_ip = 
source_ip =
port = 52334

ethernet = Ethernet(dest_mac=dest_mac, src_mac=source_mac, protocol=Types.Proto_codes.IPv4)
ip = IP(src_ip=source_ip, dest_ip=dest_ip, protocol=Types.Proto_codes.UDP)
# set protocol version
ip.protocol = 4
# time to live
ip.ttl = 255
udp = UDP(src_port=port, dest_port=port)
arp = ARP(src_ip=source_ip, src_mac=source_mac, dest_ip=dest_ip, dest_mac=dest_mac)

# print IP layer summary
print (ip.summary())
# print all IP layer information
print (ip)

```

### Handle packets
```Python
from .layers import Packet

# create a packet
packet = Packet()

payload =  Raw('sample message')
# add layers
packet.add_layers(ethernet, ip, udp, payload)
# get a specific layer
packet[Types.Layers.Ethernet]
# check if layer exists
Types.Layers.UDP in packet # equals True

# prints size in bytes and layers size
print (packet)
# prints all packet's layers information
packet.print()

# dissect income network data
packet.dissect(YOUR_RAW_BYTES)
```
### Send packet
The function send receives a packet and optional network interface and socket object. Those will be created independently if not provided.
```Python
from .layers import send
# pack layer into a bytes
packed_packet = packet.pack()
send(packed_packet)
```

### Examples
#### UDP data
#### Ping
#### Syn Attack
