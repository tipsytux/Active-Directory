# HTTP Badge

### HTTP - 3

```bash
curl http://ptl-92bc89a1-f6ce6e67.libcurl.so/pentesterlab --cookie 'key=please'
```

### HTTP - 4

```
curl http://ptl-ca7d5493-849b2623.libcurl.so/pentesterlab -H 'Content-Type: key/please'
```

### HTTP - 5

```
curl http://ptl-30f64f91-b9b83bb4.libcurl.so/pentesterlab -H 'Accept-Language: key-please'
```

### HTTP - 6

```
curl http://ptl-c78bd6e9-d61e08d7.libcurl.so/pentesterlab -X POST --data 'key=please'
```

### HTTP - 7

```
curl http://ptl-1f9753d6-647037ad.libcurl.so/pentesterlab -X POST --data ""
```

### HTTP - 8

```
curl http://ptl-db281a31-4adea1fb.libcurl.so/pentesterlab -X GET --data 'key=please'
```

### HTTP - 9

```
http://ptl-11eeee71-648dc083.libcurl.so/pentesterlab?key=please&key=please
```

### HTTP - 10

```
curl http://ptl-c5240bda-f9775ba2.libcurl.so/pentesterlab -X POST --data 'key=please&key=please'
```

### HTTP - 11

```
curl http://ptl-7d5c32fa-7cf5ece1.libcurl.so/pentesterlab?key=please -X POST --data 'key=please'
```

### HTTP - 12

```
curl http://ptl-08dd9cc9-28934e1c.libcurl.so/pentesterlab?key='=please'
```

### HTTP - 13

```
curl http://ptl-06c0c7a6-9414ba9b.libcurl.so/pentesterlab?key='please%26'
```

### HTTP - 14

```
curl http://ptl-4314a80e-b30b36be.libcurl.so/pentesterlab?%3Fkey=please
```

### HTTP - 15

```
curl http://ptl-22d0c026-11596cfc.libcurl.so/pentesterlab?key="pretty%20please"
```

### HTTP - 16

```
curl http://ptl-267c3ae1-9659e53b.libcurl.so/pentesterlab?key='please%23'
```

### HTTP - 17

```
curl http://ptl-c5191412-58325f5c.libcurl.so/pentesterlab?key=please%00
```

### HTTP - 18

```
curl http://ptl-36e0bc98-c237846f.libcurl.so/pentesterlab?key=please%25%30%30
```

### HTTP - 19

To send a parameter as an array, you can use the following syntax: name\[0]=value1\&name\[1]=value2.

```
curl 'http://ptl-b1c035f0-59c8d31f.libcurl.so/pentesterlab?key\[0\]=key&key\[1\]=please'
```

### HTTP - 20

```
curl "http://ptl-4cf1ee14-35e3cc78.libcurl.so/pentesterlab?key\[please\]=1"
```

### HTTP - 21

```
curl -X HACK http://ptl-3209a7a3-9f1e5c4f.libcurl.so/pentesterlab
```

### HTTP - 22

```
curl http://ptl-e4c6c605-df9cae03.libcurl.so/pentesterlab -H "X-HTTP-Method-Override: HACK"
```

### HTTP - 23

X-Forwarded-For:

```
curl http://ptl-0ae08ee8-2359e3b4.libcurl.so/pentesterlab -H "X-Forwarded-For: 1.2.3.4"
```

### HTTP - 24

X-Forwarded-Host:&#x20;

```
curl http://ptl-9f1bc886-2fc3c070.libcurl.so/pentesterlab -H "X-Forwarded-Host: pentesterlab.com"
```

### HTTP - 25

```
curl http://ptl-7e67e49f-d2617ab2.libcurl.so/pentesterlab/%2e%2e/pentesterlab
```

### HTTP - 26

```
curl http://ptl-915c2202-cda35d98.libcurl.so/pentesterlab%3bpentesterlab
```

### HTTP - 27

```
curl http://ptl-332a9717-1a334036.libcurl.so/pentesterlab%23pentesterlab
```

### HTTP - 28

```
curl http://ptl-3f26e7de-69e77f0d.libcurl.so/pentesterlab -H 'Content-Type: multipart/form-data'
```

### HTTP - 29

```
curl -H 'Content-Type: multipart/form-data' -F 'filename=@/home/kali/request.txt' http://ptl-111eab6f-f709b4d7.libcurl.so/pentesterlab
```

### HTTP - 30

```
curl -H 'Content-Type: multipart/form-data' -F 'filename=@/home/kali/request.txt' http://ptl-4c8e4d1a-244b4726.libcurl.so/pentesterlab --proxy http://127.0.0.1:8080
```

Then I sent this to burp and brum bram. Another simple way would have been to use the following

```
curl -H 'Content-Type: multipart/form-data' -F 'filename=@/home/kali/request.txt;filename=../request.txt' http://ptl-4c8e4d1a-244b4726.libcurl.so/pentesterlab
```

### HTTP - 31

```
curl http://ptl-2ff4ada9-968f422b.libcurl.so/pentesterlab -X POST --data "<key><value>please</value></key>"
```

### HTTP - 32

```
curl http://ptl-c2e155b9-70981e77.libcurl.so/pentesterlab -X POST --data "<key><value>please</value></key>" -H "Content-Type: application/xml"
```

### HTTP - 33

```
curl http://ptl-7835ea8e-c84dcc0c.libcurl.so/pentesterlab -X POST --data "<key><value>>please</value></key>" -H "Content-Type: application/xml"
```

### HTTP - 34

```
curl http://ptl-83dde52e-68dc1a39.libcurl.so/pentesterlab -X POST --data "<key><value>&lt;please&gt;</value></key>" -H "Content-Type: application/xml"
```

### HTTP - 35

```
curl http://ptl-1360f01d-8c280ce6.libcurl.so/pentesterlab -X POST --data "<key><value>&amp;please</value></key>" -H "Content-Type: application/xml"
```

### HTTP - 36

```
curl http://ptl-fb366f62-8dd32db2.libcurl.so/pentesterlab -X POST --data '<key value="please"></key>' -H "Content-Type: application/xml"
```

### HTTP - 37

```
curl http://ptl-0552eed3-c8a73731.libcurl.so/pentesterlab -X POST --data '<key value="&#x22;please"></key>' -H "Content-Type: application/xml"
```

### HTTP - 38

```
curl http://ptl-86ca4e6c-9a16aad5.libcurl.so/pentesterlab -X POST --data '{"key": "please"}' -H "Content-Type: application/json"
```

### HTTP - 39

```
curl http://ptl-a317cc40-1af11951.libcurl.so/pentesterlab -X POST --data '{"key": "please\""}' -H "Content-Type: application/json"
```

### HTTP - 40

```
curl http://ptl-ca1efa13-b9868619.libcurl.so/pentesterlab -X POST --data 'key: please' -H "Content-Type: application/yaml"
```

### HTTP - 41

```
curl http://ptl-12739d84-3775c11d.libcurl.so/pentesterlab -X POST --data 'key: ["please","please2"]' -H "Content-Type: application/yaml"
```

### HTTP - 42

```
curl -H 'Authorization: Basic a2V5OnBsZWFzZQ==' http://ptl-6e1b6d52-0b06346e.libcurl.so/pentesterlab
curl -u 'key:please'  http://ptl-6e1b6d52-0b06346e.libcurl.so/pentesterlab
```

### HTTP - 43

```python
import websocket

def on_message(ws,message):
    print(message)

def on_error(ws,error):
    print(error)

def on_close(ws):
    print("Closed")

def on_open(ws):
    ws.send("key")

ws = websocket.WebSocketApp("ws://ptl-a59f8e31-1f18023f.libcurl.so/pentesterlab",on_message=on_message)
ws.on_open = on_open
ws.run_forever()
```
