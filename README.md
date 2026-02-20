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
client.py
```
import socket
s = socket.socket()
s.bind(('localhost', 8000))
s.listen(5)
print("Server is listening...")
c, addr = s.accept()
print("Connection from:", addr)
address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}
while True:
    ip = c.recv(1024).decode()
    if not ip:
        break  
    print("Received IP:", ip)
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
c.close()
print("Connection closed.")
```
server.py
```
import socket
s = socket.socket()
s.connect(('localhost', 8000))
while True:
    ip = input("Enter Logical Address (or 'exit' to quit): ")
    if ip.lower() == 'exit':
        break
    s.send(ip.encode())
    mac = s.recv(1024).decode()
    print("MAC Address:", mac)
    print("IP Address Sent:", ip)
s.close()
print("Connection closed.")
```
## OUPUT - ARP
<img width="1506" height="304" alt="Screenshot 2026-02-20 112400" src="https://github.com/user-attachments/assets/6063d85b-2bc3-4828-895e-3f4fbd27c931" />

## PROGRAM - RARP
server.py
```
import socket
s = socket.socket()
s.connect(('localhost', 9000))
while True:
    mac = input("Enter MAC Address (or 'exit' to quit): ")
    if mac.lower() == 'exit':
        break
    s.send(mac.encode())
    ip = s.recv(1024).decode()
    print("Logical Address:", ip)
s.close()
print("Connection closed.")

```
client.py
```
import socket
s = socket.socket()
s.bind(('localhost', 9000))
s.listen(5)
print("Server is listening on port 9000...")
c, addr = s.accept()
print("Connection from:", addr)
address = {
    "6A:08:AA:C2": "192.168.1.100",
    "8A:BC:E3:FA": "192.168.1.99"
}
while True:
    mac = c.recv(1024).decode()
    if not mac:
        break  
    print("Received MAC Address:", mac)

    try:
        c.send(address[mac].encode())
    except KeyError:
        c.send("Not Found".encode())
c.close()
print("Connection closed.")

```
## OUPUT -RARP
<img width="1501" height="279" alt="Screenshot 2026-02-20 112551" src="https://github.com/user-attachments/assets/d12d0142-7273-4d6c-bb3d-8a5c6cb3354d" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
