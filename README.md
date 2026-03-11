# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm
1. Start the program.

2. Create a socket using socket library.

3. Bind the server to localhost and port 8080.

4. Put the server in listening mode.

5. Accept the client connection request.

6. Receive HTTP request from the client.

7. Check whether the request is GET or POST.

8. If GET, read the webpage file and send it to the client.

9. If POST, receive uploaded data and store it in a file.

10. Send HTTP response message to the client.

11. Close the client connection.

12. Stop the program.



## PROGRAMM
Index.html
```
<title>
    <head>
        <title>index-html-server</title>

    </head>
    <body>
        <h1>hello from-python-socket-server</h1>
    </body>
</title>
```
Server.py
```
Httpserver

import socket

s = socket.socket()
s.bind(("localhost",8080))
s.listen(1)

print("Server running...")

while True:
    c,addr = s.accept()
    
    request = c.recv(1024).decode()
    print("Request received")

    if "GET" in request:
        f = open("index.html","r")
        data = f.read()
        f.close()

        response = "HTTP/1.1 200 OK\n\n" + data
        c.send(response.encode())

    elif "POST" in request:
        data = request.split("\n\n")[1]

        f = open("upload.txt","w")
        f.write(data)
        f.close()

        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())

    c.close()
```
Client.py
```

httpclient
import socket

s = socket.socket()
s.connect(("localhost",8080))

ch = input("1.Download 2.Upload : ")

# Download webpage
if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())

    data = s.recv(4096)
    print(data.decode())

# Upload file
else:
    msg = input("Enter data to upload: ")

    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())

    data = s.recv(1024)
    print(data.decode())

s.close()
```
## UPLOAD.TXT
<img width="782" height="76" alt="Screenshot 2026-03-11 114351" src="https://github.com/user-attachments/assets/aca5f6a4-0f51-4dc5-857f-a19e7af78757" />

## OUTPUT
<img width="1103" height="545" alt="Screenshot 2026-03-11 114331" src="https://github.com/user-attachments/assets/7716cccc-8173-46e4-8ffa-dad903e61dfb" />
## Result
Thus the socket for HTTP for web page upload and download created and Executed
