# IKEv2 VPN Server on Docker

The original readme please see:
 - https://github.com/gaomd/docker-ikev2-vpn-server

New feature:
 - Support windows, android with certificate file

## Setup server

```
git clone https://github.com/tiennan/docker-ikev2-vpn-server.git

cd docker-ikev2-vpn-server

sudo docker build -t tsl0922/docker-ikev2-vpn-server:v1 .

sudo docker run --privileged -d --name ikev2-vpn-server --restart=always -p 500:500/udp -p 4500:4500/udp -e "CERT_CN=vpn1.example.com" -e "VPN_USER=your_username" -e "VPN_PASSWORD=your_password" tsl0922/docker-ikev2-vpn-server:v1

sudo docker run --privileged -i -t --rm --volumes-from ikev2-vpn-server -e "HOST=vpn1.example.com" tsl0922/docker-ikev2-vpn-server:v1 generate-mobileconfig > ikev2-vpn.mobileconfig

```
 - `vpn1.example.com` // your server domain or ip
 - `your_username` // username for windows clinet
 - `your_password` // password for windows client
 
## Setup clients

#### iOS/Mac
 - please see https://github.com/gaomd/docker-ikev2-vpn-server
 
#### windows/Android
1. copy certificate from container to server
```
sudo docker cp {ContainerID}:/etc/ipsec.d/certs/clientCert.p12 .
```
2. copy certificate from server to local
```
scp {USER}@{IP}:/path/to/clientCert.p12 .
```
3. double click to install certificate into your computer

 - please see https://shenyuqi.com/archives/541 for more useful tips
 
