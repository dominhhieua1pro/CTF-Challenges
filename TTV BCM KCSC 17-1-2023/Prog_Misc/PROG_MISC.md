# PROG/MISC

## BinggChillinggg

Down file zip về ta nhận được 1 folder có tên Bingg chứa 52*78 images có size 10x10

![image](https://user-images.githubusercontent.com/80137840/212880852-947a7a83-6705-4e3e-aa1b-c9591fe1a02d.png)

Sử dụng thư viện Pillow để gộp tất cả images .png này thành 1 pic hoàn chỉnh

Code để solve chall này:
```
from PIL import Image

src = Image.new('RGB', (1000, 1000))

for j in range(52):
	for i in range(78):
		dst=Image.open('.\Bingg\Bingg\img'+str(j*10)+'_'+str(i*10)+'.png')
		row=int(j)*10
		column=int(i)*10
		src.paste(dst,(column, row))
src.save('flag.png')
```

![image](https://user-images.githubusercontent.com/80137840/212880396-7f71f6c2-f1f2-4bce-bd51-2e1b48b6195e.png)

Flag: `KCSC{Zao_shang_hao_zhong_guo!_Xian_zai_wo_you_bing_chilling!!}`


## xò
Challenge cho ta 2 bức ảnh có nhiều điểm ảnh khác nhau:

![1.jpg](https://user-images.githubusercontent.com/80137840/212881139-6f8c0f42-33ad-4b5e-b9e9-f4047b439104.png)
![2.jpg](https://user-images.githubusercontent.com/80137840/212881193-5e820174-0e18-47b5-8abd-28eec6ee4cef.png)

Thực hiện phép xor các bytes khác nhau 2 bức ảnh này để tìm flag

Code xor

```
from pwn import *

with open("1.jpg", mode='rb') as f1:
    pic1 = f1.read()

with open("2.jpg", mode='rb') as f2:
    pic2 = f2.read()

flag = ''
for i in range(max(len(pic1),len(pic2))):
	if pic1[i] != pic2[i]:
       		flag += chr(pic1[i] ^ pic2[i])
		
print(flag)
```

Flag: `KCSC{Da_bao_roi_cu_x%r_tung_byte_la_ra_ma_li}`


## Gen Max Number

Đề bài `nc 146.190.115.228 10464`

![image](https://user-images.githubusercontent.com/80137840/212886117-5d334d88-ad0a-40b6-9db7-68fcd2b888ea.png)

Thử nc đến server:

![image](https://user-images.githubusercontent.com/80137840/212886305-15817b2b-20f0-40d1-9764-a399b1dfb863.png)

Sử dụng pwn lib để remote tới server lấy giá trị `Number: `

Tách number thành array, sort giảm dần sau đó join lại và send tới server

Loop 100 lần và nhận flag

Code solve chall:

```
from pwn import *

host = "146.190.115.228"
port = 10464
r = remote(host,port)

for i in range(100):
	r.recvuntil(b"Number: ")
	number = eval(r.recvline().strip().decode())
	arr = [int(x) for x in str(number)]
	arr.sort(reverse=True)
	res = "".join([str(x) for x in arr])
	r.sendline(f"{res}")
	print(r.recvline())

print(r.recvline())
```
![image](https://user-images.githubusercontent.com/80137840/212887624-9a2b6293-e95f-4330-ba1a-30c6cde7c8ee.png)

![image](https://user-images.githubusercontent.com/80137840/212887518-fe03b4bd-bce5-4236-8052-b4ac5025d3b0.png)

Flag: `KCSC{You will maximize yourself when participating in KCSC, G00d_j0b}`


## Split String

Đề bài `nc 146.190.115.228 10463`

![image](https://user-images.githubusercontent.com/80137840/213164812-db19df40-c19e-4cc7-9d1b-b0649620980b.png)

Thử nc đến server:

![image](https://user-images.githubusercontent.com/80137840/213165020-209ae2a9-45e1-4854-a927-317dd7e52569.png)

Sử dụng pwn lib để remote tới server lấy giá trị `Split it: `

Sử dụng thư viện wordninja để hỗ trợ việc split thành mảng các từ có nghĩa, sau đó join lại và send tới server

Loop 100 lần và nhận flag

Code solve chall:

```
import wordninja
from pwn import *

host="146.190.115.228"
port=10463
r = remote(host,port)

for i in range(100):
	r.recvuntil(b"Split it: ")
	str = r.recvline().strip().decode()
	# print(str)
	res = wordninja.split(str)
	res = " ".join(res)
	# print(res)
	r.sendline(res)

	print(r.recvline())
print(r.recvline())
```

![image](https://user-images.githubusercontent.com/80137840/213168316-09518b89-a7ea-4c96-922d-f7ffee9fa50d.png)

Flag: `KCSC{Looks like you know how to use that tool, nice hecker}`


## Smaller Number

Đề bài `nc 146.190.115.228 10454`

![image](https://user-images.githubusercontent.com/80137840/213168725-dced9ccb-5b78-4221-a820-e59224fe136c.png)

Thử nc đến server:

![image](https://user-images.githubusercontent.com/80137840/213168594-974ffc2f-5270-495e-ac30-c67b857fa248.png)

Sử dụng pwn lib để remote tới server lấy giá trị `Ans: `

Kiểm tra từng phần tử xem có bao nhiêu phần tử nhỏ hơn, sau đó append vào 1 array và send tới server

Loop 100 lần và nhận flag

Code solve chall:

```
from pwn import *
host="146.190.115.228"
port=10454
r = remote(host,port)

for i in range(100):
	r.recvuntil(b"Array: ")
	arr = eval(r.recvline().strip().decode())
	res = [] 
	c = 0
	for u in arr:
		for v in arr:
			if v < u:
				c += 1
		res.append(c)
		c = 0
	# print(res)
	res = str(res)
	# print(res)
	r.sendline(res)
	print(r.recvline())
print(r.recvline())
```

![image](https://user-images.githubusercontent.com/80137840/213170602-fd0462f0-4e5a-447a-ae46-d843229f88e9.png)

Flag: `KCSC{Phew, i done, you clear, hen ra tet gap mat}`
