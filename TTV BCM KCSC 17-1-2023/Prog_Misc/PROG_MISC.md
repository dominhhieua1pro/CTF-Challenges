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
src.save('final.png')
```

![image](https://user-images.githubusercontent.com/80137840/212880396-7f71f6c2-f1f2-4bce-bd51-2e1b48b6195e.png)

Flag: `KCSC{Zao_shang_hao_zhong_guo!_Xian_zai_wo_you_bing_chilling!!}`


## xò
Challenge cho ta 2 bức ảnh có nhiều điểm ảnh khác nhau:

![1.jpg](https://user-images.githubusercontent.com/80137840/212881139-6f8c0f42-33ad-4b5e-b9e9-f4047b439104.png)
![2.jpg](https://user-images.githubusercontent.com/80137840/212881193-5e820174-0e18-47b5-8abd-28eec6ee4cef.png)

Ta sẽ thực hiện phép xor nội dung 2 bức ảnh này để tìm nội dung flag

Code xor

```
from pwn import *

with open("1.jpg", mode='rb') as f1:
    a = f1.read()

with open("2.jpg", mode='rb') as f2:
    b = f2.read()

_xor = xor(a,b)
print(_xor)
```
Ouput trả về rất nhiều bytes \x00 nhưng quan sát kỹ ta thấy có các bytes khác biệt

![image](https://user-images.githubusercontent.com/80137840/212883187-284517b0-fe05-418a-a74d-750f075cb5ae.png)

Lấy ra các bytes này bytes \x00_ này và join lại

```
arr = []

for i in _xor:
    if i != 0x00:
        arr.append(chr(i))

print("".join(arr))
```

Ta nhận được flag

![image](https://user-images.githubusercontent.com/80137840/212883858-49817c8a-7cf4-49cd-b58c-855fa079a87f.png)

Code hoàn chỉnh solve chall:

```
from pwn import *

with open("1.jpg", mode='rb') as f1:
    a = f1.read()

with open("2.jpg", mode='rb') as f2:
    b = f2.read()

_xor = xor(a,b)
arr = []

for i in _xor:
    if i != 0x00:
        arr.append(chr(i))

print("".join(arr))
```

Flag: `KCSC{Da_bao_roi_cu_x%r_tung_byte_la_ra_ma_li}`


## Gen Max Number

Đề bài `nc 146.190.115.228 10464`

![image](https://user-images.githubusercontent.com/80137840/212886117-5d334d88-ad0a-40b6-9db7-68fcd2b888ea.png)

Thử nc đến server:

![image](https://user-images.githubusercontent.com/80137840/212886305-15817b2b-20f0-40d1-9764-a399b1dfb863.png)

Sử dụng pwn lib để remote tới server lấy giá trị number

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

