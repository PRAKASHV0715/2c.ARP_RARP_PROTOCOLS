# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.
P
## PROGRAM - ARP
##Server (ARP Server)

import socket

arp_table = { "192.168.1.1": "AA:BB:CC:DD:EE:01", "192.168.1.2": "AA:BB:CC:DD:EE:02", "192.168.1.3": "AA:BB:CC:DD:EE:03" }

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM) server.bind(("localhost", 5000)) server.listen(5)

print("ARP Server is running...")

while True: client, addr = server.accept() print("Connected with", addr)
~~~
ip = client.recv(1024).decode()
print("Requested IP:", ip)

mac = arp_table.get(ip, "MAC Address not found")
client.send(mac.encode())

client.close()
~~~
##Client (ARP Client)

import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

client.connect(("localhost", 5000))

ip = input("Enter IP Address: ")

client.send(ip.encode())

mac = client.recv(1024).decode()

print("MAC Address:", mac)

client.close() 

## OUPUT - ARP

<img width="1036" height="146" alt="Screenshot 2026-03-26 140229" src="https://github.com/user-attachments/assets/379b174d-7b00-4bdd-9b02-8da36fd8eefb" />


<img width="1047" height="272" alt="Screenshot 2026-03-26 140240" src="https://github.com/user-attachments/assets/c552fea3-8984-408e-a0bc-04232e867ee8" />


## PROGRAM - RARP
##Server (RARP Server)

import socket

rarp_table = { "AA:BB:CC:DD:EE:01": "192.168.1.1", "AA:BB:CC:DD:EE:02": "192.168.1.2", "AA:BB:CC:DD:EE:03": "192.168.1.3" }

server = socket.socket(socket.AF_INET, socket.SOCK_STREAM) server.bind(("localhost", 6000)) server.listen(5)

print("RARP Server is running...")

while True: client, addr = server.accept() print("Connected with", addr)
~~~
mac = client.recv(1024).decode()
print("Requested MAC:", mac)

ip = rarp_table.get(mac, "IP Address not found")
client.send(ip.encode())

client.close()
~~~
##Client (RARP Client)

import socket

client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

client.connect(("localhost", 6000))

mac = input("Enter MAC Address: ")

client.send(mac.encode())

ip = client.recv(1024).decode()

print("IP Address:", ip)

client.close()


## OUPUT -RARP

<img width="1050" height="201" alt="Screenshot 2026-03-26 140402" src="https://github.com/user-attachments/assets/3a83a3a9-9b08-4196-a141-a3bbe4f6734c" />

<img width="1041" height="173" alt="Screenshot 2026-03-26 140438" src="https://github.com/user-attachments/assets/1d6b531a-54dc-4b57-8ace-89268ac7b1c8" />


## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
