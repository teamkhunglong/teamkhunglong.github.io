---
layout: post
title: "SVATTT 2020 Online - Merklision"
date: 2020-10-24 17:00:00 +0700
category: capture-the-flag
author: minh
short-description: Giải bài Merklision - Vòng khởi động Sinh viên với An toàn thông tin 2020
---

# Intro

Nhắc đến CTF thì chắc hẳn bạn đọc của chiếc blog này không còn lạ gì nữa. Mình từng đi thi SvATTT 3 năm, từ 2015-2017, hay chơi mảng Crypto. Mình định tính là năm 2018 nghỉ thi CTF để ra trường đấy, cơ mà giờ đến vòng loại năm 2020 rồi mà mình vẫn chưa cầm được bằng đại học :))

Dù sao thì, sau cuộc thi, những cậu em ở UET-CTF chưa làm được bài crypto đã hỏi mình làm sao để làm được bài này.

![][1]{:height="50%" width="50%"}

Cuộc thi năm nay mình không ra đề cũng như không liên quan đến ban tổ chức. Với kinh nghiệm tham gia cuộc thi SvATTT, mình thường tìm hiểu về người ra đề để có được bức tranh toàn cảnh về cách giải bài. Ví dụ:
1. 2016 - Có 1 bài crypto 300 do anh Tân của đội `PiggyBird` ra đề, liên quan đến AES padding oracle. Hồi đó mình không giải được.
2. 2017 - Có 2 bài crypto do `cothan` ra đề, tên là Onion và NotSideChannel. Về cơ bản, chỉ cần nháp 50%, code 50% thì sẽ có flag.
3. 2018 - Có 1 chuỗi bài crypto do mình ra đề, liên quan đến ECC. Về cơ bản, chỉ cần nháp 20%, code 80% thì sẽ có flag.

Năm nay, người ra đề là `ndh`, một người anh cực bá đến từ KMA-HCM, đồng đội của mình trong team `Acebear`. Trước mình có làm một số bài của anh Hiếu. Nói chung, bài của anh Hiếu cần nháp 80% và code 20% thì mới có được flag. Như bài này là một ví dụ.

# Brief

Source code của bài có thế tìm thấy ở [đây](https://gist.github.com/minhtt159/af8e19e2ac7088be48889ccd5c6e0e0b#file-merklision-py)
- Nhận input `n` từ người dùng, từ đó sinh ra một chuỗi ngẫu nhiên có `n` phần tử, mỗi phần tử là 1 chữ cái thuộc `a-zA-Z`
- Đưa cho người dùng chuỗi ngẫu nhiên đó, yêu cầu người dùng nhập vào `2020` chuỗi khác, không được trùng lặp.
- Nếu `Merkle-Hash` từ input của người dùng đưa ra đúng với `Merkle-Hash` từ đầu bài sinh ra thì được coi là hợp lệ.

# Merkle Hash

Đầu tiên cần tìm hiểu merkle tree - merkle hash là gì. Đầu tiên, merkle tree là một cấu trúc dữ liệu đơn giản, cho phép một khối dữ liệu được băm trên toàn bộ khối dữ liệu một cách độc lập và phân tán.

Chiếc ảnh ở [Wikipedia](https://en.wikipedia.org/wiki/Merkle_tree) giải thích khá rõ về cấu trúc này.

![][2]{:height="100%" width="100%"}

Hash tree được sử dụng trong Hash-based cryptography, áp dụng khá tốt trong việc bảo toàn dữ liệu, nghĩa là dữ liệu gửi qua mạng nếu thỏa mãn đúng merkle hash thì khả năng cao dữ liệu đó toàn vẹn. Ví dụ có thể nói đến Bitcoin & Ethereum.

Vậy thì làm sao có thể tạo ra được 1 collision, mà đề bài lại bắt tạo ra 2020 collision?

# Collision

### Second Preimage Attacks với Merkle Tree

Second Preimage Attack nghĩa là mình được đưa cho một tập dữ liệu, và mình phải tìm một tập dữ liệu khác thỏa mãn hash như tập dữ liệu ban đầu.

Với Merkle Tree, nếu không kiểm tra kĩ đầu vào, rất dễ để tạp được đáp án như mong muốn. Như hình trên, ta có thể phân tích được một tập dữ liệu khác như sau:
1. Giả sử dữ liệu đầu vào có dạng `L1, L2, L3, L4`.
2. Tầng giữa sẽ lấy `H(L1)+H(L2)` và `H(L3)+H(L4)` làm tầng tiếp theo. 

Vì vậy, ta có thể đưa tập dữ liệu khác là `H(L1)+H(L2), H(L3)+H(L4)` thì sẽ sinh ra mã băm cuối tương tự như dữ liệu đầu vào mà vẫn thỏa mãn là không trùng lặp. Ví dụ:

```
M(1, 2, 3, 4) = M(H(1,2), H(3,4))
```

Mặc dù vậy, ta mới chỉ có `log2(n)` collision, với `0 < n < 2020` thì mới có khoảng 10 collisions.

### False implementation

Trong source code của chương trình, nếu độ dài của dữ liệu đầu vào là số lẻ, phần tử cuối cùng của chuỗi dữ liệu sẽ tự động được lặp lại

![][3]{:height="50%" width="50%"}

Do đó, cứ khi nào gặp bộ dữ liệu có độ dài lẻ, ta lại có 1 collision nữa bằng cách lặp phần tử cuối. Ví dụ:

```
M(1, 2, 3, 4, 5) = M(1, 2, 3, 4, 5, 5)
```

Mặc dù vậy, với mỗi tầng, ta có thể lặp phần tử cuối 1 lần. Mà tổng cộng cũng chỉ có 10 tầng.

### Nhân đệ quy ?

Nếu chỉ nghĩ một cách rời rạc hai cách đụng độ trên, ta có thể sinh ra được 20 nghiệm, ít hơn 100 lần so với yêu cầu đề bài. Vậy làm sao để có được hơn 100 lần nghiệm nữa? Hmm ... ngoài nhân đệ quy?

Chiến thuật như này:
1. Nếu dữ liệu đầu vào có dạng `1, 2, 3, 4, 5`, thì ta sẽ có đụng độ với `1, 2, 3, 4, 5, 5` (áp dụng 2)
2. Từ `1, 2, 3, 4, 5, 5`, thì ta sẽ có đụng độ với `H(1,2), H(3,4), H(5,5)` (áp dụng 1)
3. Từ `H(1,2), H(3,4), H(5,5)`, ta lại có đụng độ với `H(1,2), H(3,4), H(5,5), H(5, 5)` (áp dụng 2)
4. Nếu lật ngược lại tầng trước đó, ta sẽ có đụng độ với `1, 2, 3, 4, 5, 5, 5, 5` (mind blown)

Vậy từ `1` dữ liệu có độ dài bằng `5`, ta có thể sinh ra `4` collision như trường hợp vừa rồi (chưa tính đến các tầng tiếp theo).

Có thể suy ra được, độ dài lớn nhất mà có thể đụng độ với nhau được là lũy thừa của 2 đầu tiên lớn hơn `n` (với n = 5 thì max_length = 2**3 = 8).

Ta cần ưu tiên chọn `n` sao cho có thể sinh ra được càng nhiều tầng càng tốt.

Để làm được như vậy, `n = (((2*2-1)*2-1)*2-1)....; n < 2020`, và ta có `n = 1025`, `max_length = 2048`.

Nếu làm như vậy thì có bao nhiêu nghiệm? Mình cũng không biết nữa ...

# Solution

Có hai cách để sinh ra các trường hợp collision; cách khôn và cách ngu. Ở đây mình chọn cách ngu.

Mình chân thành xin lỗi công sức của các anh, các thầy đã dạy mình code những năm qua, nhưng mình lười nên brute được bao nhiêu thì brute thôi, giải được bài này đã ăn điểm rồi á ._.

Thuật toán của mình như sau:
1. Do kiểu gì cũng lập lại tầng đầu tiên để tìm đụng độ, mình sẽ loop để lặp thêm phần tử cuối cho đến độ dài `2048`.
2. Với mỗi nghiệm, mình sẽ tính merkle hash và lưu lại những đụng độ qua các tầng của nghiệm đó (áp dụng 1).
3. Mình lưu lại các nghiệm vào `set` như của đề bài, loại ra những nghiệm đã bị trùng lặp (lặp nhiều lắm :D).
4. Trả lại kết quả cho server.

Code mình có lưu lại tại [đây](https://gist.github.com/minhtt159/af8e19e2ac7088be48889ccd5c6e0e0b#file-merklision_solve-py)

```bash
$ python .\merklision.py
Maximum length can collide is 2048
There are 2047 collisions
Takes 11 sec to produce
```

# Outro

Trong thời gian thi (4 tiếng), hình như có 5 đội giải được bài này. Đối với một cuộc thi CTF online, như vậy cũng khá là khoai. Một team gồm 4 người với 4 bài nghĩa là mỗi người phải hoàn thành hoàn hảo 1 bài của mình. Như đứa em nói

![][4]{:height="50%" width="50%"}

[1]: {{ site.baseurl }}/assets/img/2020/10/get-help-merklision.png#center
[2]: https://flawed.net.nz/assets/hash_tree-svg.png
[3]: {{ site.baseurl }}/assets/img/2020/10/odd-length-merklehash.png#center
[4]: {{ site.baseurl }}/assets/img/2020/10/merklision-outro.png#center