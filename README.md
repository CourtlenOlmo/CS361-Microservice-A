# Book Search Microservice - README

## Communication Contract

This microservice allows clients to search for books by title. The server performs a Google search and responds with the first Amazon link found, or an error message if no link is found.

### Overview:
Communication is done via ***ZeroMQ*** using the ***REQ/REP*** messaging pattern.
- **Request**: Client sends a book title **(string)** to the server.
- **Google Search**: Server searches for Amazon links.
- **Response**: Server sends back an Amazon link or error message **(both strings)**.

### Port and Server Address:
- **Port**: `5555`
- **Server Address**: `tcp://<Server IP>:5555`

## Programmatically REQUEST data (3a)

To request data, send the book title **(string)** to the server using a REQ socket. The server processes it and sends a response.

### Example Code to Request Data:

```python
import zmq

# Create ZeroMQ context and request socket
context = zmq.Context()
socket = context.socket(zmq.REQ)

# Connect to server (replace with actual IP)
server_ip = "192.168.123.132"  
socket.connect(f"tcp://{server_ip}:5555")

# Send book title
book_title = "The Catcher in the Rye"
socket.send_string(book_title)
```
## Programmatically RECEIVE data (3b)

The client receives the server's response (Amazon link or error) via the same **REQ** socket using `recv_string()`.

### Example Code to Receive Data:

```python
# Receive and print server response
response = socket.recv_string()
print(f"Server response: {response}")
```
## UML Sequence Diagram (3c)
![UML Sequence Diagram](https://www.plantuml.com/plantuml/png/ZT6nJiD030RW_PxY7zkXF003Akh0n58U83fI9x5wiOFjCF3qv48P8eJKAT79dt_BFdfaYtaiQLg-tFAK9N0gJ1ARfrTkJPtiarjAgQXEEAa4owopuqmVCtaSpkIJYbC2SEk2mzC6un5l91UygruH78MmomuFO-dtgSfj_Ly_aNLgOzEhzeKQfspjiDklL3G8nlqGq6u3Qsuj9CVB2h4qGGoqZl9mLtB7ScdocBzKci9olIFqJ36RU0rQk7dWUVMe7ch80Z9J-sU2snP_6stqJkt7OYJttDC-rTNMwwHqN7wNmtu3)



