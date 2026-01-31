# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL

## Reg.No.: 212225040312

## AIM

## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program

## PROGRAM
server.py
~~~
import socket

client_socket = socket.socket()
client_socket.connect(('localhost', 8000))

while True:
    data = client_socket.recv(1024).decode()
    if not data:
        break
    print(data)
    client_socket.send("Acknowledgement received from the server".encode())
~~~

client.py
~~~
import socket
server_socket = socket.socket()
server_socket.bind(('localhost', 8000))
server_socket.listen(1)

print("Waiting for connection from server...")
connection, addr = server_socket.accept()
print(f"Connected to: {addr}")

total_frames = int(input("Enter number of frames to send: "))
frames = list(range(total_frames))
window_size = int(input("Enter Window Size: "))

start = 0  
while start < len(frames):
    end = start + window_size
    frame_batch = frames[start:end] 
    connection.send(str(frame_batch).encode())  
    ack = connection.recv(1024).decode()
    if ack:
        print(ack)
        start = end
~~~

## OUPUT
Server

<img width="771" height="114" alt="Screenshot 2026-01-31 134151" src="https://github.com/user-attachments/assets/a3b47a81-4f45-41c3-8f14-862c3bf1de9d" />

Client

<img width="935" height="202" alt="Screenshot 2026-01-31 134139" src="https://github.com/user-attachments/assets/84828ba3-73b4-4bab-88ce-4a6f45ea4e16" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
