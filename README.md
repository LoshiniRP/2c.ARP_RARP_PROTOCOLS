# 2c.SIMULATING ARP /RARP PROTOCOLS
## Aim:
To write a python program for simulating ARP protocols using TCP.
## Algorithm:
### Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
### Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.

## Program - ARP:
### Server side:
```
import socket 
s=socket.socket()
s.connect(('localhost',8000)) 
while True:
    ip=input("Enter logical Address : ")
    s.send(ip.encode())
    print("MAC Address",s.recv(1024).decode())
```

### Client side:
```
import socket
s=socket.socket() 
s.bind(('localhost',8000)) 
s.listen(5) 
c,addr=s.accept()
address={"165.165.80.80":"6A:08:AA:C2","165.165.79.1":"8A:BC:E3:FA"};
while True: 
    ip=c.recv(1024).decode() 
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
```

## Output - ARP:
<img width="1920" height="1080" alt="Screenshot (136)" src="https://github.com/user-attachments/assets/2e53118c-3613-4855-9929-a3b901662278" />


## Program - RARP:
### Server side:
```
import socket 
s=socket.socket() 
s.connect(('localhost',8000)) 
while True:
    ip=input("Enter MAC Address : ")
    s.send(ip.encode())
    print("Logical Address", s.recv(1024).decode())
```

### Client side:
```
import socket
s=socket.socket()
s.bind(('localhost',8000)) 
s.listen(5) 
c,addr=s.accept()
address={"6A:08:AA:C2":"192.168.1.100","8A:BC:E3:FA":"192.168.1.99"};
while True: 
    ip=c.recv(1024).decode() 
    try:
        c.send(address[ip].encode())
    except KeyError:
        c.send("Not Found".encode())
```

## Output -RARP:
<img width="1920" height="1080" alt="Screenshot (138)" src="https://github.com/user-attachments/assets/41572a83-142e-4c98-9651-489a2487f73a" />


## Result:
Thus, the python program for simulating ARP protocols using TCP was successfully executed.
