Task 1: DNS – How Names Become IPs
What happens when you type google.com in a browser?
Your computer asks a DNS server for the IP address of google.com.
DNS resolves the domain name and returns an IP address.
The browser connects to that IP address using TCP/HTTPS.
Google's server responds and the webpage is loaded.
DNS Record Types
Record	Purpose
A	Maps a domain name to an IPv4 address
AAAA	Maps a domain name to an IPv6 address
CNAME	Creates an alias from one domain to another
MX	Specifies the mail server for a domain
NS	Specifies the authoritative DNS servers for a domain
Run
dig google.com

Look for output similar to:

google.com.    300    IN    A    142.250.193.78
A Record = 142.250.193.78
TTL = 300 seconds

(Your values may differ depending on location and time.)

Task 2: IP Addressing
What is an IPv4 Address?

An IPv4 address is a unique 32-bit identifier assigned to a device on a network. It consists of four octets separated by dots.

Example:

192.168.1.10

Each octet ranges from 0–255.

Public vs Private IP
Type	Description	Example
Public IP	Reachable over the Internet	8.8.8.8
Private IP	Used inside local networks	192.168.1.10
Private IP Ranges
10.0.0.0      - 10.255.255.255
172.16.0.0    - 172.31.255.255
192.168.0.0   - 192.168.255.255
Run
ip addr show

Example:

inet 192.168.1.15/24

This is a private IP because it belongs to the 192.168.x.x range.

Task 3: CIDR & Subnetting
What does /24 mean?

In 192.168.1.0/24, the first 24 bits are used for the network portion and the remaining 8 bits are available for hosts.

Usable Hosts
CIDR	Total IPs	Usable Hosts
/24	256	254
/16	65,536	65,534
/28	16	14
Why do we subnet?

Subnetting divides a large network into smaller networks. It improves organization, security, performance, and efficient IP address usage.

CIDR Exercise
CIDR	Subnet Mask	Total IPs	Usable Hosts
/24	255.255.255.0	256	254
/16	255.255.0.0	65,536	65,534
/28	255.255.255.240	16	14
Task 4: Ports – The Doors to Services
What is a Port?

A port is a logical communication endpoint that allows multiple services to run on the same IP address.

For example:

Web server → Port 80
Database → Port 3306
SSH → Port 22
Common Ports
Port	Service
22	SSH
80	HTTP
443	HTTPS
53	DNS
3306	MySQL
6379	Redis
27017	MongoDB
Run
ss -tulpn

Example output:

tcp LISTEN 0 128 0.0.0.0:22
tcp LISTEN 0 128 0.0.0.0:3306

Match:

Port	Service
22	SSH
3306	MySQL
Task 5: Putting It Together
You run:
curl http://myapp.com:8080

What networking concepts are involved?

DNS resolves myapp.com to an IP address. The connection is established to port 8080 on that IP. Routing, TCP communication, and HTTP protocol are then used to retrieve the response.

Your app can't reach a database at 10.0.1.50:3306. What would you check first?
Verify network connectivity using ping or telnet.
Confirm the database service is running on port 3306.
Check firewall/security group rules.
Ensure the application is using the correct IP address and port
