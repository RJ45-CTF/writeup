---
title: 'crypto/base727'
author: "nr1a"
---
![](https://i.postimg.cc/1zqpdVDP/image.png)
![](https://i.postimg.cc/pL08rYJP/chat.png)
source
727.py
```
import binascii

flag = open('flag.txt').read()

def encode_base_727(string):
    base = 727
    encoded_value = 0

    for char in string:
        encoded_value = encoded_value * 256 + ord(char)

    encoded_string = ""
    while encoded_value > 0:
        encoded_string = chr(encoded_value % base) + encoded_string
        encoded_value //= base

    return encoded_string

encoded_string = encode_base_727(flag)
print(binascii.hexlify(encoded_string.encode()))
```
out.txt
`06c3abc49dc4b443ca9d65c8b0c386c4b0c99fc798c2bdc5bccb94c68c37c296ca9ac29ac790c4af7bc585c59d`

chatgptに書かせた謎のエンコーダ？っぽいのでコードを読みながら戻すようにいい感じにコード書けば出来ました。


```py
import binascii
import re

def decode_base_727(encoded_string):
    base = 727
    decoded_value = 0

    for char in encoded_string:
        decoded_value = decoded_value * base + ord(char)

    decoded_string = ""
    while decoded_value > 0:
        decoded_string = chr(decoded_value % 256) + decoded_string
        decoded_value //= 256

    return decoded_string

with open('out.txt', 'r') as f:
    content = f.read()
    content = re.sub(r'[^0-9a-fA-F]', '', content)
    if len(content) % 2 != 0:
        content += '0'
    encoded_string = binascii.unhexlify(content).decode()

decoded_string = decode_base_727(encoded_string)
print(decoded_string)
```

`flag: osu{wysiwysiwysiywsywiwywsi}`