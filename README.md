# dns_cache


The Source code Folder is called DNS_attack, and it is a simple implementation of a DNS cache Poisoning in Python. The folder contains mainly seven files:- 


arp.py
attack.py
dns.py
net.py
netdiscover.py
subnet.py
colors.py


arp.py :- 

Here's a documentation of 'arp.py':

‘arp.py’ is a Python script that performs ARP (Address Resolution Protocol) poisoning on a local network. ARP poisoning is an attack that involves sending fake ARP messages to the victim's machine, causing it to associate the attacker's MAC address with the IP address of another host on the network. This can allow the attacker to intercept network traffic or perform other malicious activities.

The script uses the 'scapy' module to generate and send ARP packets with a spoofed source MAC address. The 'arp.py' script defines a class called 'ArpPoisoning' that contains methods for configuring the attack and executing it against a target.

The 'ArpPoisoning' class has the following methods:

1. '__init__(self, target_ip, gateway_ip, interface)': This is the constructor method for the 'ArpPoisoning' class. It takes three parameters: 'target_ip', which is the IP address of the victim's machine that will be attacked; 'gateway_ip', which is the IP address of the default gateway on the local network; and 'interface', which is the name of the network interface that will be used to send the ARP packets.

2. 'get_mac_address(self, ip_address)': This method uses the 'scapy' module to send an ARP request to the specified IP address and wait for a response. If a response is received, the method returns the MAC address of the host that responded. If no response is received, the method returns 'None'.

3. 'poison_target(self, target_mac, gateway_mac)': This method sends a series of ARP packets to the victim's machine and the default gateway with the attacker's MAC address and the IP address of the other host. This causes both hosts to associate the attacker's MAC address with the IP address of the other host.

4. 'restore_target(self, target_mac, gateway_mac)': This method sends a series of ARP packets to the victim's machine and the default gateway with the correct MAC addresses and IP addresses. This restores the correct ARP tables on both hosts.

5. 'run(self)': This method executes the ARP poisoning attack. It starts by getting the MAC addresses of the victim's machine and the default gateway using the 'get_mac_address()' method. It then sends ARP packets to both hosts using the 'poison_target()' method. The method also sets up a signal handler to catch keyboard interrupts and restore the ARP tables using the 'restore_target()' method when the attack is complete.

The 'arp.py' script also contains a 'main()' function that creates an instance of the 'ArpPoisoning' class and executes the 'run()' method to perform the attack.

attack.py

Here's a documentation of 'attack.py':

'attack.py' is a Python script that performs a DNS cache poisoning attack against a vulnerable DNS server. The script uses the 'scapy' module to generate DNS queries with spoofed source IP addresses and port numbers in order to trick the DNS server into accepting fake DNS responses.

The script defines a 'DNSCachePoisoning' class that provides methods for configuring the attack and executing it against a target DNS server. The class has the following methods:

1. '__init__(self, domain, nameserver, target_ip, target_port)': This is the constructor method for the 'DNSCachePoisoning' class. The method takes four parameters: 'domain', which is the domain name of the target DNS server; 'nameserver', which is the IP address of the authoritative nameserver for the target domain; 'target_ip', which is the IP address of the target DNS server; and 'target_port', which is the port number of the target DNS server.

2. 'get_response(self, query)': This method generates a DNS query packet with a spoofed source IP address and port number, and sends it to the target DNS server. The method then listens for a DNS response packet from the server and returns it to the caller.

3. 'get_poisoned_response(self, query, fake_ip)': This method generates a fake DNS response packet with a spoofed source IP address and port number, and sends it to the target DNS server. The method then listens for a DNS response packet from the server and returns it to the caller.

4. 'poison_cache(self)': This method performs the DNS cache poisoning attack against the target DNS server. The method sends a series of DNS queries to the server with spoofed source IP addresses and port numbers, and then sends fake DNS response packets to the server in an attempt to poison its cache.

The 'attack.py' script also contains a 'main()' function that creates an instance of the 'DNSCachePoisoning' class and executes the 'poison_cache()' method to perform the attack. 

dns.py

Here's a documentation of 'dns.py':

'dns.py' is a Python script that implements a basic DNS (Domain Name System) server. DNS is a protocol used to translate human-readable domain names (such as google.com) into IP addresses that computers can understand. The script uses the 'socket' module to listen for DNS requests on port 53 and respond with the appropriate IP address.

The 'dns.py' script defines a class called 'DNSServer' that contains methods for configuring and running the server. The class has the following methods:

1. '__init__(self, cache_file)': This is the constructor method for the 'DNSServer' class. It takes one parameter, 'cache_file', which is the name of a file that will be used to store the DNS cache. The cache file is a simple text file that stores DNS queries and their corresponding IP addresses.

2. 'start(self)': This method starts the DNS server by creating a socket and listening for incoming DNS requests on port 53. When a request is received, the method parses the request and looks up the corresponding IP address in the cache file. If the IP address is found, the method sends a response back to the client with the IP address. If the IP address is not found, the method sends a response back to the client indicating that the domain name could not be resolved.

3. 'stop(self)': This method stops the DNS server by closing the socket.

4. 'add_to_cache(self, domain_name, ip_address)': This method adds a DNS query and its corresponding IP address to the cache file.

5. 'load_cache(self)': This method loads the DNS cache from the cache file into memory.

6. 'save_cache(self)': This method saves the DNS cache from memory to the cache file.

The 'dns.py' script also contains a 'main()' function that creates an instance of the 'DNSServer' class and starts the server. 

netdiscover.py

Here's a documentation of 'netdiscover.py':

'netdiscover.py' is a Python script that uses ARP protocol to discover hosts on a local network. The script sends ARP requests to all hosts on the network and then listens for their ARP replies. It then prints out a list of all discovered hosts along with their MAC and IP addresses.

Here are the functions defined in 'netdiscover.py':

1. 'get_mac_address(ip_address)': This function takes an IP address as input and returns the MAC address of the corresponding host. It does this by sending an ARP request to the specified IP address and waiting for an ARP reply.

2. 'discover_hosts(interface)': This function takes the name of a network interface as input and returns a list of all hosts discovered on the network. It does this by sending ARP requests to all hosts on the network and waiting for their ARP replies. The function uses the 'get_mac_address' function to obtain the MAC addresses of discovered hosts.

3. 'print_hosts(hosts)': This function takes a list of hosts as input and prints out their MAC and IP addresses in a user-friendly format.

The 'main' function of 'netdiscover.py' uses these functions to discover hosts on the network and print out their MAC and IP addresses. It takes the name of a network interface as a command line argument and calls the 'discover_hosts' and 'print_hosts' functions to display the results.

It's important to note that the script requires root privileges to send ARP requests and receive ARP replies. The script uses the 'scapy' library to send and receive ARP packets, so this library must be installed before running the script.

Overall, 'netdiscover.py' is a useful script for discovering hosts on a local network and can be used for network troubleshooting or security purposes.

net.py

Here's a documentation of 'net.py':

'net.py' is a Python script that contains helper functions for working with network sockets. The script defines several classes and functions for creating, sending, and receiving data over network sockets.

Here are the classes and functions defined in 'net.py':

1. 'UDPSocket': This is a class that represents a UDP socket. It has methods for creating, binding, sending, and receiving data over a UDP socket. The methods include:

- '__init__(self)': Constructor method that creates a new UDP socket.
- 'bind(self, address, port)': Method for binding the socket to a specific address and port.
- 'sendto(self, data, address, port)': Method for sending data to a specific address and port.
- 'recvfrom(self, buffer_size)': Method for receiving data from the socket.

2. 'TCPSocket': This is a class that represents a TCP socket. It has methods for creating, binding, connecting, sending, and receiving data over a TCP socket. The methods include:

- '__init__(self)': Constructor method that creates a new TCP socket.
- 'bind(self, address, port)': Method for binding the socket to a specific address and port.
- 'connect(self, address, port)': Method for connecting the socket to a remote address and port.
- 'send(self, data)': Method for sending data over the socket.
- 'recv(self, buffer_size)': Method for receiving data from the socket.

3. 'create_udp_socket()': This is a helper function that creates a new UDP socket.

4. 'create_tcp_socket()': This is a helper function that creates a new TCP socket.

5. 'send_udp_packet(data, address, port)': This is a helper function that creates a new UDP socket, sends the specified data to the specified address and port, and then closes the socket.

6. 'send_tcp_packet(data, address, port)': This is a helper function that creates a new TCP socket, connects to the specified address and port, sends the specified data, receives the response, and then closes the socket.

7. 'recv_all(sock, buffer_size)': This is a helper function that receives data from a socket until no more data is available. It returns the received data as a string.

8. 'recv_until(sock, delimiter)': This is a helper function that receives data from a socket until a specified delimiter is reached. It returns the received data as a string.

The 'net.py' script can be used as a standalone library for working with network sockets or as a helper library for other network-related scripts. It's important to note that the script does not handle errors or exceptions, so proper error handling should be implemented when using the functions and classes defined in this script.

subnet.py

Here's a documentation of 'subnet.py':

'subnet.py' is a Python script that takes an IP address and subnet mask as input and calculates various properties of the corresponding subnet. It performs subnet calculations by converting the IP address and subnet mask to binary, performing logical operations, and converting the result back to decimal.

Here are the functions defined in 'subnet.py':

1. 'calculate_subnet(ip_address, subnet_mask)': This function takes an IP address and subnet mask as input and returns a dictionary containing the following information about the corresponding subnet: network address, broadcast address, subnet mask, number of hosts, and host addresses.

2. 'print_subnet(subnet)': This function takes a subnet dictionary as input and prints out the subnet information in a user-friendly format.

The 'main' function of 'subnet.py' uses these functions to calculate and display the properties of the specified subnet. It takes the IP address and subnet mask as command line arguments and calls the 'calculate_subnet' and 'print_subnet' functions to display the results.

Overall, 'subnet.py' is a useful script for performing subnet calculations and can be used for network troubleshooting or security purposes.

Colors.py

Here is the documentation for `color.py`:

`color.py` is a Python script that defines a function called `print_color()` which is used to print text in different colors in the terminal. It does this by using ANSI escape codes to modify the color and style of the text.

The `print_color()` function takes two arguments: `text` and `color`. `text` is the text to be printed in the specified color, and `color` is a string specifying the color and style of the text. 

To use the `print_color()` function in your code, simply import the `color.py` module and call the function with the desired text and color.

Overall, `color.py` is a simple yet useful script for adding color and style to text in the terminal, making it easier to read and differentiate between different types of output.

