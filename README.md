# Network Packet Handling

This project demonstrates custom network packet construction and transmission between a client and server using Python sockets. The packet includes a structured header and supports various payload types (integer, float, string).

## Project Files

- `client.py`: Sends custom packets to the server.
- `server.py`: Receives packets, parses the header and payload, and echoes the information back to the client.
---

## Packet Format

Each packet has:
- **Header (5 bytes total)**:
  - `version` (1 byte)
  - `header_length` (1 byte)
  - `service_type` (1 byte): 
    - `1` = integer payload  
    - `2` = float payload  
    - `3` = string payload
  - `payload_length` (2 bytes, unsigned short)

- **Payload (variable)**:
  - Encoded based on `service_type`.

---

## How to Run

### 1. Start the Server
python server.py
 - Listens on IP: 10.128.0.2, Port: 12345 (can be modified in the script).
 - Waits for incoming connections and unpacks received packets.

### 2. Send to the Client
python client.py --version 1 --header_length 5 --service_type 3 --payload "Hello Server!" --host 10.128.0.2 --port 12345
 --version: Packet version
 --header_length: Length of the header
 --service_type: Type of data (1 = int, 2 = float, 3 = string)
 --payload: Data to send
 --host: Server IP (default: localhost)
 --port: Server port (default: 12345)

### Notes
- struct module is used to encode/decode header and payload using format !BBBH.
- The server automatically detects the payload length and type using the header fields.
- The server echoes the interpreted packet back to the client as a UTF-8 string.

## Author
- Lexi Ouellette 
- Project: Computer Networks Programming Assignment – Packet Handling
