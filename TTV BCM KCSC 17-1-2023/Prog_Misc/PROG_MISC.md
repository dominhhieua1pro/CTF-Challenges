# PROG/MISC

## BinggChillinggg
Down file zip về ta nhận được 1 folder có tên Bingg chứa 52*78 images có size 10x10

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



