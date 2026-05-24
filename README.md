# 4.Execution_of_NetworkCommands
## AIM :Use of Network commands in Real Time environment
## Software : Command Prompt And Network Protocol Analyzer
## PROCEDURE:
Open Visual Studio Code.

Create two Python files:

server.py
client.py
Import the socket module in both programs.

In the server program:

Create a socket
Bind host and port number
Listen for client connection
Accept the connection request
Receive the website name from client
Perform ping operation
Send the result to client
In the client program:

Create a socket
Connect to server using host and port
Enter the website name to ping
Send the website name to server
Receive the ping result from server
Display the result
Open two terminals in VS Code.

Run the server program first using: python server.py

Run the client program using: python client.py

Enter the website name such as: google.com

Observe the ping response received from the server.

Stop the program by typing: exit

Close both client and server connections.

google.com youtube.com facebook.com amazon.com wikipedia.org openai.com github.com yahoo.com microsoft.com instagram.com
## program
```
import socket
import threading
from pythonping import ping

def handle_client(c, addr):
    print(f"Connected with {addr}")

    while True:
        try:
            hostname = c.recv(1024).decode()

            if not hostname:
                break

            if hostname.lower() == "exit":
                print(f"Client {addr} disconnected")
                break

            print(f"Client requested ping for: {hostname}")

            try:
                result = ping(hostname, count=2, timeout=2)

                response = f"\nPing Result for {hostname}:\n{result}"

            except Exception:
                response = "Website/Host Not Found"

            c.send(response.encode())

        except:
            break

    c.close()

# Create socket
s = socket.socket()

# Bind server
s.bind(('localhost', 8000))

# Listen for clients
s.listen(5)

print("Server waiting for connections...")

while True:
    c, addr = s.accept()

    client_thread = threading.Thread(target=handle_client, args=(c, addr))
    client_thread.start()
```
```
import socket

s = socket.socket()

s.connect(('localhost', 8000))

print("Connected to server")

while True:

    website = input("Enter website to ping: ")

    s.send(website.encode())

    if website.lower() == "exit":
        print("Connection closed")
        break

    response = s.recv(4096).decode()

    print("\nServer Response:")
    print(response)

s.close()
```

## Output
<img width="1365" height="767" alt="image" src="https://github.com/user-attachments/assets/84c5f108-1fba-40ea-a517-32711b548b40" />
<img width="1365" height="767" alt="image" src="https://github.com/user-attachments/assets/1ff654a5-2028-43b7-9764-45c7f9937f30" />


## Result
Thus Execution of Network commands Performed 
