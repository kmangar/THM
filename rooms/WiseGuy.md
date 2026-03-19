# [W1seGuy](https://tryhackme.com/room/w1seguy)


## Task1: Source code  

download the python source code:  
  

```python
import random
import socketserver 
import socket, os
import string

flag = open('flag.txt','r').read().strip()

def send_message(server, message):
    enc = message.encode()
    server.send(enc)

def setup(server, key):
    flag = 'THM{thisisafakeflag}' 
    xored = ""

    for i in range(0,len(flag)):
        xored += chr(ord(flag[i]) ^ ord(key[i%len(key)]))

    hex_encoded = xored.encode().hex()
    return hex_encoded

def start(server):
    res = ''.join(random.choices(string.ascii_letters + string.digits, k=5))
    key = str(res)
    hex_encoded = setup(server, key)
    send_message(server, "This XOR encoded text has flag 1: " + hex_encoded + "\n")
    
    send_message(server,"What is the encryption key? ")
    key_answer = server.recv(4096).decode().strip()

    try:
        if key_answer == key:
            send_message(server, "Congrats! That is the correct key! Here is flag 2: " + flag + "\n")
            server.close()
        else:
            send_message(server, 'Close but no cigar' + "\n")
            server.close()
    except:
        send_message(server, "Something went wrong. Please try again. :)\n")
        server.close()

class RequestHandler(socketserver.BaseRequestHandler):
    def handle(self):
        start(self.request)

if __name__ == '__main__':
    socketserver.ThreadingTCPServer.allow_reuse_address = True
    server = socketserver.ThreadingTCPServer(('0.0.0.0', 1337), RequestHandler)
    server.serve_forever()
```


## Task2: Geting Those Flags!

The server is listening on port 1337 via TCP. You can connect to it using Netcat or any other tool you prefer.  

1. Start the Target Machine and connect to the AttackBox  


```python
# Take hex input from user
hex_string = input("Enter hex string: ")   

hex_encoded = hex_string

xored_original = bytes.fromhex(hex_encoded).decode('utf-8')

def xor_encrypt(text):
    if len(text) < 5:
        raise ValueError("Input string must be at least 5 characters long.")
    # 4 keys for first 4 characters
    keys = ['T', 'H', 'M', '{','}']  

    output = []

    # XOR first 4 characters
    for i in range(4):
        output.append(chr(ord(text[i]) ^ ord(keys[i])))

    # XOR last character with }
    last_char = text[-1]
    output.append(chr(ord(last_char) ^ ord(keys[4])))

    return "".join(output)

# Key
print(xor_encrypt(xored_original))

key=xor_encrypt(xored_original)

flag=xored_original
xored=""
for i in range(0,len(flag)):
    xored += chr(ord(flag[i]) ^ ord(key[i%len(key)]))

print(xored)
```

2. run `nc [Target IP] 1337 `  


3. 


<b>
What is the first flag?


What is the second and final flag?

<b>

