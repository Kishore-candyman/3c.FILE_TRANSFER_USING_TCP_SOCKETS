# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM

CLIENT:
```
import socket

s = socket.socket()
host = socket.gethostname()
port = 60000

s.connect((host, port))
s.send("Hello server!".encode())

with open('received_file', 'wb') as f:  # Binary write mode
    while True:
        print('Receiving data...')
        data = s.recv(1024)
        if not data:
            break
        f.write(data)

print('File received successfully')
s.close()
print('Connection closed')

```

CLIENT:
```
import socket

port = 60000
s = socket.socket()
host = socket.gethostname()
s.bind((host, port))
s.listen(5)
print("Server listening...")

while True:
    conn, addr = s.accept()
    print(f"Got connection from {addr}")
    
    data = conn.recv(1024)
    print('Server received:', repr(data.decode()))

    filename = 'mytext.txt'
    with open(filename, 'rb') as f:  # Open file in binary read mode
        l = f.read(1024)
        while l:
            conn.send(l)  # Send bytes
            print('Sent:', repr(l))
            l = f.read(1024)

    print('Done sending file')
    conn.send("Thank you for connecting".encode())  # Final message
    conn.close()
    

```
## OUPUT

CLIENT:

![image](https://github.com/user-attachments/assets/74aa5f56-2d3b-4a81-96bf-ff4e138ce4ba)

SERVER:

![image](https://github.com/user-attachments/assets/7afa6601-9efc-4a5e-8584-023a0728ccf3)

## RESULT
Thus, the python program for creating File Transfer using TCP Sockets Links was 
successfully created and executed.
