# Crypto

## Tet_is_ya_best
Nội dung ciphertext đề bài cho:
```
lyl, rwns dmsfm rn wkmrx myf iyrx pynljorw, jn luy ejvvynl lxrqjljsmrw pynljorw jm ojyl mrh.
lyl jn knkrwwi pxsh luy ymq sp trmkrxi ls yrxwi pyexkrxi. 
eypsxy lyl, ojylmrhyny cxycrxy hrmi lujmvn psx luy luxyy hrjm qrin. 
luyi gwyrm luyjx uskny rmq qygsxrly fjlu pwsfyxn nkgu rn dkhbkrl lxyy sx cyrgu ewsnnsh. 
r ukvy rhskml sp pssq fjww ey eskvul eypsxy lyl psx hrdjmv lxrqjljsmrw qjnuyn. ermu gukmv, ermu lyl, vjs gur, asj rmq hkl, …rmq grmqjyn rxy luy pssqn lurl hknl uroy sm lyl uswjqrin.
qkxjmv lyl, cyscwy ojnjl luyjx xywrljoyn’ ushyn rmq vjoy fjnuyn. 
usfyoyx, luy ojylmrhyny eywjyoy lurl luy pjxnl ojnjlsx r prhjwi xygyjoyn jm luy iyrx qylyxhjmyn luyjx psxlkmy psx luy ymljxy iyrx, cyscwy myoyx ymlyx rmi uskny sm luy pjxnl qri fjluskl eyjmv jmojlyq pjxnl. 
rmsluyx gknlsh jn vjojmv wkgdi hsmyi, fujgu jn ckl jmls r xyq ymoywscy rn r nihesw sp wkgd rmq fjnu psx r myf rvy. 
lxrqjljsmrwwi, ywqyxn fjww vjoy wkgdi hsmyi ls gujwqxym rmq luy swqynl cyscwy jm luy prhjwi. usfyoyx, msfrqrin, cyscwy grm vjoy jl ls rmismy jmgwkqjmv pxjymqn, crxymln, myjvuesxn,… 
eynjqyn, ojylmrhyny knkrwwi vs ls crvsqrn sx lyhcwyn ls cxri psx uyrwlu, fyrwlu, nkggynn,… 
ls ojylmrhyny, lyl jn luy urccjynl ljhy sp rww iyrx rxskmq, hyheyxn jm r prhjwi grm vrluyx lsvyluyx, fujgu jn r hyrmjmvpkw hynnrvyn sp wkmrx myf iyrx pynljorw. 
rww jm rww, lyl jn rww reskl ergd ls sxjvjmn, ey vssq ls sluyxn, ymtsi luy cxygjskn hshyml, rmq fjnu psx luy eynl ls gshy.
luy pwrv jn: dgng{lyl_lyl_lyl_lyl_qym_xsj__gukg_grg_erm_mrh_hsj_lurl_mujyk_nkg_dusy__wko_pxsh_wkwkkkkkkkkkkkk}
```
Dự đoán đây có thể là mã thay thế (substitution cipher)

Copy cipher vào trang `https://math.dartmouth.edu/~awilson/tools/frequency_analysis.html`

Đầu tiên nhận thấy ngay dgng khả năng cao là kcsc bằng cách thay d thành k, g thành c và n thành s

Tiếp tục làm tương tự để tìm ra các ký tự làm cho các words có nghĩa và ta được flag là
`kcsc{tet_tet_tet_tet_den_roi__chuc_cac_ban_nam_moi_that_nhieu_suc_khoe__luv_from_luluuuuuuuuuuuu}`

![image](https://user-images.githubusercontent.com/80137840/212813845-6c6840e5-ac9e-426d-9e4f-ea0702c7a1d2.png)
Tuy nhiên format của BTC là KCSC{} nên ta cần sửa flag lại thành
`KCSC{tet_tet_tet_tet_den_roi__chuc_cac_ban_nam_moi_that_nhieu_suc_khoe__luv_from_luluuuuuuuuuuuu}`



# Chuyến tàu vô tận
Nội dung ciphertext đề bài cho:

`01010011 00110001 01000010 01010100 01010110 01101011 00110101 01010110 01010011 01101011 01001010 01010011 01010101 00110000 01000110 01001111 01010001 00110000 01001110 01001101 01010001 01010101 01010110 01000010 01010010 01010101 01010110 01001000 01010011 00110000 01110100 01010000 01010110 01010101 00111001 01000110 01010100 00110000 01010110 01000010 01010110 01000110 01010010 01010101 01010100 00110001 01001110 01000110 01010101 00110001 01001010 01010000 01010111 01010110 01001010 01000111 01010100 01000110 01001110 01001010`

Thử convert về dạng ASCII ta được chuỗi:
`S1BTVk5VSkJSU0FOQ0NMQUVBRUVHS0tPVU9FT0VBVFRUT1NFU1JPWVJGTFNJ`

Đưa chuỗi này vào trang https://www.dcode.fr/cipher-identifier ta được kết quả suggest cao là base64 encoding

![image](https://user-images.githubusercontent.com/80137840/212826570-20e131c5-3b74-4b1a-8737-2fffd35fd0c3.png)

Thực hiện decode base64 chuỗi ASCII này ta được: 
`KPSVNUJBRSANCCLAEAEEGKKOUOEOEATTTOSESROYRFLSI`

Đến đây, quay lại đọc Description 1 chút, ta thấy mô tả có nhắc đến keyword **đường ray**

![image](https://user-images.githubusercontent.com/80137840/212829562-a19ea18a-7470-4c6c-8245-269edb710e0f.png)

=> Đoạn text vừa decode base64 có thể đã được encrypted bởi loại mã **Rail Fence Cipher**

Tiến hành decrypt đoạn text này ta nhận được một đoạn text bắt đầu bởi KCSC và được viết liền các ký tự: 
`KCSCPLEASESAVERENGOKUKYOJUROBEFORELASTSTATION`

![image](https://user-images.githubusercontent.com/80137840/212826811-f74a5179-1c31-4e90-a618-86d3685991b5.png)

Format lại thành flag
`KCSC{PLEASESAVERENGOKUKYOJUROBEFORELASTSTATION}`



# ezenc
Nội dung ciphertext đề bài cho dạng hexa: 
```
4e544d7a4d44526c4e5451314d544d7a4e7a51304e6a59794e6d51305a5463324e5745304e7a5a6a4e7a553159544d784d7a6b305954597a4d7a457a4f5451304e6a497a4d6a4d354e7a4d304f54557a4e4455324f4459324e54457a5a444e6b
```

Đưa lên Cipher Identifier nhận được suggest cao là ASCII Code

![image](https://user-images.githubusercontent.com/80137840/212831452-40b09402-9d75-47bd-9b67-c8f6d05d4243.png)

Convert Hex to Text ta được chuỗi: 
`NTMzMDRlNTQ1MTMzNzQ0NjYyNmQ0ZTc2NWE0NzZjNzU1YTMxMzk0YTYzMzEzOTQ0NjIzMjM5NzM0OTUzNDU2ODY2NTEzZDNk`

Tiếp tục đưa lên Cipher Identifier 

![image](https://user-images.githubusercontent.com/80137840/212832345-e237cf12-9b99-49b8-9ec1-9fd8091364db.png)

Decode base64 ta nhận được dạng hexa:
`53304e5451337446626d4e765a476c755a31394a63313944623239734953456866513d3d`

Lại đưa tiếp vào Cipher Identifier 

![image](https://user-images.githubusercontent.com/80137840/212832816-284f9e23-82c4-4b9a-8a1f-dde5431b7929.png)

Convert Hex to Text và decode base 64 lần nữa ta nhận được flag:

`KCSC{Encoding_Is_Cool!!!}`



## Waiting xor you
Đề bài cho source code **chal.py**:
```
def xor(a: bytes, b: bytes):
    return bytes([a[i % len(a)] ^ b[i % len(b)] for i in range(max(len(a), len(b)))])


flag = b"KCSC{???????????????????????????}"
key = b"??????"
print(xor(flag, key))
#b'>0\x0c,\x1a+:=\x100(5*,\x08*(2<=\x11!> E!\x006Q3VP"'
```

Source có 1 hàm xor bytes với bytes của flag và key (6 ký tự) với result là: 
`>0\x0c,\x1a+:=\x100(5*,\x08*(2<=\x11!> E!\x006Q3VP"`

Thực hiện flag xor result để tìm key
```
def xor(a: bytes, b: bytes):
    return bytes([a[i % len(a)] ^ b[i % len(b)] for i in range(max(len(a), len(b)))])


flag = b"KCSC{???????????????????????????}"
key = b"??????"

result = b'>0\x0c,\x1a+:=\x100(5*,\x08*(2<=\x11!> E!\x006Q3VP"'
print(xor(flag, result))
```

Output là:

![image](https://user-images.githubusercontent.com/80137840/212835677-b0e73357-099e-44c1-b8ed-feeae80fa085.png)

Nhận được 5 ký tự đầu của key là **us_oa**

Lúc này ta có thể brute-force ký tự thứ 6 với danh sách tất cả ký tự trong bảng ASCII. Tuy nhiên khi quay lại xem cái Description 

![image](https://user-images.githubusercontent.com/80137840/212836523-5b399df9-c074-4655-84d0-0b374806881a.png)

Đoán được ngay ký tự thứ 6 là **f**

Thay **key = b"us_oaf"** và xor result với key để lấy flag
```
def xor(a: bytes, b: bytes):
    return bytes([a[i % len(a)] ^ b[i % len(b)] for i in range(max(len(a), len(b)))])


flag = b"KCSC{???????????????????????????}"
key = b"us_oaf"

result = b'>0\x0c,\x1a+:=\x100(5*,\x08*(2<=\x11!> E!\x006Q3VP"'
print(xor(key, result))
```

Flag: ![image](https://user-images.githubusercontent.com/80137840/212837080-ef9dae3e-19ac-4c09-9231-7df6788349de.png)



## Baby RSA
Đề bài cho 2 bộ tham số RSA với N là 1 tích của 2 số nguyên tố lớn, e là số tự nhiên và nguyên tố cùng nhau với phi(N), c là ciphertext
```
N = 15352779128347791007085648503432481424157803925393171911336519959303041912793003445150925254969419519884885627602949531418218225326241330358578677264291299499045156352856967773874092740247954469116785697497470359167464514847916796070937222502678650971142025027485709803661507504065663359734963995261557205074306680610789459371027709841983679828401650412118581758223828022880963792279486668571818011466055318488192646258947512800694294415085962951256371066608809290272610036677808985446462843978518062681057733507143078031646346208413485310265372217830403150353055860675112625586559711701385861569315220697333861624379
e = 65537
c = 15234236089035375697324692533670087291506518940119036163416398391967780168919318354707846778624354698516063263617526552128038076384559799589892922339842617250512544697038702386359526750526178907382834958249547265193039648889826194155309648868936192999852133095813222074561116001151012735334802656112338051809650150133151593743932999203464490667768775427469247438829347671941888012366872257009578553525557727089061380208505227601870807413218975683275974505471293568473828250102456368913442644633180181134360763687437716261371150673736444389341962003188848553355141677598975486937134000420118129170359576583029403557942

N = 15982718555435618288754952825031769117547387692870819916928476182486552631450549525038004384299500928472276458295066304137369014377160187571033623657889062613801742400497641807643980044808976440676862201272127143957576575149606597154709398483099034525371596546592801110128376813970664993485013198718018226001957923124705027042095389185838776028755434052822406158434805165952649450734719704790287398587363744031940151465734319442206651654599805135818078308593766746643747762801233581535052852057500102870115114418044977691033773894430619259087481112470507634568658553796252929863357071876672708667512148351746343531117
e = 65537
c = 14885607973375889007078519123100974115225353700683145848346940830215842296236022064741140177725928924596370430750080147304522857101387236773374040772176304410951702328717963740412312728751613954861413504364980527717532790500428309863862561124898893373142700396901730889636915098343789818475628485817239154487704058551986711609340589253536488388398979374511706211200806320134259212830624064308312622387468199391611528640492645158491457258448456704967213884906875441766539265807657769147443850357508881684012458065494838709615700471413080742522071409893826661777251684652098457627030289338034729867701502662269612568405
```

Nhìn đề bài thế này ta có thể nghĩ đến 1 loại tấn công vào RSA đó là **RSA GCD Attack**

Cụ thể là lỗi sources of randomness khi tạo khóa RSA. Một số trình tạo số ngẫu nhiên của một số OS cũ không thực sự ngẫu nhiên và đôi khi tạo ra các khóa công khai RSA có chung thừa số nguyên tố. Khi đó ta sẽ tìm GCD của 2 số N này và tính ra tất cả các khóa bí mật rồi decrypt để tìm ra plaintext.

Code solve bài này:
```
from math import *
from Crypto.Util.number import *

N1 = 15352779128347791007085648503432481424157803925393171911336519959303041912793003445150925254969419519884885627602949531418218225326241330358578677264291299499045156352856967773874092740247954469116785697497470359167464514847916796070937222502678650971142025027485709803661507504065663359734963995261557205074306680610789459371027709841983679828401650412118581758223828022880963792279486668571818011466055318488192646258947512800694294415085962951256371066608809290272610036677808985446462843978518062681057733507143078031646346208413485310265372217830403150353055860675112625586559711701385861569315220697333861624379
# N1 = q1.p1
e = 65537
c1 = 15234236089035375697324692533670087291506518940119036163416398391967780168919318354707846778624354698516063263617526552128038076384559799589892922339842617250512544697038702386359526750526178907382834958249547265193039648889826194155309648868936192999852133095813222074561116001151012735334802656112338051809650150133151593743932999203464490667768775427469247438829347671941888012366872257009578553525557727089061380208505227601870807413218975683275974505471293568473828250102456368913442644633180181134360763687437716261371150673736444389341962003188848553355141677598975486937134000420118129170359576583029403557942

N2 = 15982718555435618288754952825031769117547387692870819916928476182486552631450549525038004384299500928472276458295066304137369014377160187571033623657889062613801742400497641807643980044808976440676862201272127143957576575149606597154709398483099034525371596546592801110128376813970664993485013198718018226001957923124705027042095389185838776028755434052822406158434805165952649450734719704790287398587363744031940151465734319442206651654599805135818078308593766746643747762801233581535052852057500102870115114418044977691033773894430619259087481112470507634568658553796252929863357071876672708667512148351746343531117
# N2 = q1.p2
e = 65537
c2 = 14885607973375889007078519123100974115225353700683145848346940830215842296236022064741140177725928924596370430750080147304522857101387236773374040772176304410951702328717963740412312728751613954861413504364980527717532790500428309863862561124898893373142700396901730889636915098343789818475628485817239154487704058551986711609340589253536488388398979374511706211200806320134259212830624064308312622387468199391611528640492645158491457258448456704967213884906875441766539265807657769147443850357508881684012458065494838709615700471413080742522071409893826661777251684652098457627030289338034729867701502662269612568405

# cal gcd
q1 = gcd(N1,N2)
p1 = N1 // q1  

# cal d1 = e^-1 mod phi(N1)
d1 = inverse(e, (p1-1)*(q1-1))

# decrypt RSA to plain (c1^d1 mod N1)
plain = pow(c1, d1, N1)

# convert to text
plaintext = long_to_bytes(plain1)
print(plaintext)
```

Flag:
`KCSC{All_I_Want_for_Chrismas_is___a_girlfriend T_T}`


