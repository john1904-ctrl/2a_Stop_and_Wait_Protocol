# 2a_Stop_and_Wait_Protocol
## AIM 
To write a python program to perform stop and wait protocol
## ALGORITHM
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
## Server
```
import socket

s = socket.socket()
s.bind(('localhost', 8000))
s.listen(1)
print("Server ready...")

c, _ = s.accept()
while True:
    msg = c.recv(1024).decode()
    if not msg:
        break
    print("Received:", msg)
    c.send(b"ACK")
    if msg == "exit":
        break

c.close()
s.close()
```
## Client
```
import socket

c = socket.socket()
c.connect(('localhost', 8000))
c.settimeout(5)

while True:
    msg = input("Message: ")
    c.send(msg.encode())

    if msg == "exit":
        break

    try:
        if c.recv(1024).decode() == "ACK":
            print("ACK received")
    except socket.timeout:
        print("No ACK, retransmitting...")

c.close()
```
## OUTPUT
## Server

<img width="725" height="138" alt="image" src="https://github.com/user-attachments/assets/c98c878e-d2d2-4942-a240-5308c6e953cf" />

## Client

<img width="700" height="137" alt="image" src="https://github.com/user-attachments/assets/b9d8e5b7-9db5-48e0-a534-111c1fe33389" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed.
