---
layout: post
title: "How to DevOps 101"
date: 2021-03-31 09:00:00 +0700
category: operations
author: minh
short-description: Getting started with DevOps
---

ref: [link](https://www.youtube.com/watch?v=5pxbp6FyTfk)

# Giới thiệu

Blog này viết dựa trên bài ref ở trên, bên cạnh đó mình sẽ biến đổi một chút để phù hợp hơn với use case của mình. Dù sao, mình cũng phải làm việc viết doc này do lead mình bắt mình làm :)

Bài blog này sẽ giới thiệu qua những gì cần thiết để nhón chân vào thế giới DevOps. Mình sẽ không giới thiệu quá nhiều về công dụng của nó vì việc này có thể trở thành một bài blog mới. Tại đây, mình sẽ lướt qua một vài công nghệ cần có để bắt đầu DevOps.

# Level 1

Ở bước 1, mình sẽ cần 3 phần nhỏ, bào gồm: ngôn ngữ lập trình, quản lý mã nguồn và hệ điều hành. Đây là 3 thứ tối quan trọng nếu bạn làm IT nói chung và DevOps nói riêng.

## Ngôn ngữ lập trình (Programming Language)

Gì thì gì, làm IT không biết code ít thì cũng biết code nhiều. Một người anh của mình bất cứ khi nào có ai hỏi anh ý về một vấn đề nào đó, anh ý đều bảo "Học lập trình đi". Lương anh ý gấp 3 lần mình, thu nhập của anh ý cũng phải gấp 10, nên chắc là anh ý nói đúng. Mình cũng thấy đúng.

Khi bắt đầu học lập trình, mình bắt đầu học code C/C++. Nếu như ngày xưa, mọi người hay học code bằng Pascal; thì bây giờ, ngành IT nói chung đã khá là dễ thở. Bạn có thể học code bằng C++ hay Java, thậm chí là học **Python** để nhập môn lập trình. Python là một ngôn ngữ rất dễ sử dụng, dễ bắt đầu. Cái gì quan trọng thì phải nói 3 lần. Vì vậy, nếu chưa biết về lập trình, hay muốn nhón chân vào DevOps thì nên học Python.

Khi học Python, bạn cũng muốn xem qua về các kĩ thuật tự động (automation). Làm sao dùng Python để tạo một HTTP request, GET/POST các thứ đồ; nâng cao hơn thì học cách sử dụng một thư viện, dùng API.

Ngoài ra, cũng nên xem qua những ngôn ngữ lập trình khác như JavaScript (TypeScript) / Ruby để cuộc sống dễ dàng hơn. Thêm nữa, bạn cần phải học C/C++ bởi để cần hiểu rõ bản chất của lập trình hay muốn học những kĩ thuật nâng cao thì không ngôn ngữ nào dễ bằng C.

## Quản lý mã nguồn (Source Control)

Đến năm 2021 rồi, ở tập đoàn tư bản to nhất VN, có những người lương mấy ngàn $, **vẫn chia sẻ mã nguồn dưới dạng USB, hoặc nén lại và gửi qua Google Drive** ?? :D ?? Không cần biết bạn có bằng thạc sĩ / tiến sĩ nước ngoài hay gì, nếu bạn lập trình, làm ơn hãy biết một chút về việc quản lý mã nguồn.

Để quản lý mã nguồn (versioning), cách dễ nhất là dùng **Git**. Những dự án từ ngày xưa có thể dùng *subversion* (svn), nhưng hầu hết bây giờ mọi người đều dùng Git hết. Từ những bài tập lớn ở trên trường, đến những dự án tầm cỡ thế giới kiểu Chromium đều dùng Git. Vì vậy, phải biết dùng Git. Để học dùng Git, tại thời điểm này, bạn có thể thử đẩy code lên Github.

Nói đến Github, mình cần nói thêm là ngoài Github, còn rất nhiều kho lưu trữ mã nguồn (repository) khác ví dụ như Gitlab, Azure Devops, ... Các dịch vụ lưu mã nguồn rất nhiều, đa số đều miễn phí.

Quay ngược lại về versioning, sau khi bạn chọn được repo phù hợp với bản thân, nếu bạn mới bắt đầu thì nên có một versioning tool phù hợp. Có rất nhiều tool có giao diện hoặc được tích hợp với hệ thống. Kể ra ví dụ như: TortoiseGit, Source Tree, ... Thật ra, mọi người khi bắt đầu học Git, họ thường dùng luôn dòng lệnh (terminal / command line), cũng để hiểu được các cơ chế của Git. Như mình làm chiếc blog này cũng quản lý đa số trên VSCode

Một lưu ý nhỏ nếu bạn muốn học hành chuẩn chỉ về cách quản lý mã nguồn là nên học cách dùng CMake. Thay vì để tất cả code vào 1 file, hay để tất cả file vào 1 folder, thì bạn nên học cách chia các tính năng ra nhiều file / folder, tương tự như code Java vậy. Việc này nhằm mục đích về sau đọc code đỡ bị *pain in the ass*

## Hệ điều hành (Operating System)

Dùng hệ điều hành gì thì cũng làm IT được thôi, làm DevOps cũng thế. Mình thì quen dùng macOS, nhưng mà Windows thì cũng quá tuyệt vời. Nhưng để học một cách chuẩn chỉ, nhất là về DevOps, bạn phải biết về Linux.

Nhiều bạn năm 1 năm 2, mới học IT, luôn bị choáng ngợp bởi các thư viện cần thiết để bắt đầu lập trình. Ví dụ như là: cùng là code C/C++ nhưng dùng DevC++ hay CodeBlocks ngon hơn (assume là các bạn quen với Windows chẳng hạn); hoặc là tại sao không build được, nó cứ báo lỗi gì ý.

Mình không bảo Linux khủng hơn Windows hay macOS, nhưng những khó khăn bạn đang gặp phải thường giải quyết rất dễ trên Linux. Cụ thể là Ubuntu là một Linux Distro khá thân thiện với người dùng, và cộng đồng cũng hỗ trợ thân thiện hơn nếu bạn dùng Ubuntu. Dù sao, hệ điều hành cũng chỉ là một công cụ, bạn thích cái nào thì dùng cái đó thôi. Như mình, mình dùng macOS khá lâu rồi, nên mình hiểu được cách sử dụng hệ điều hành này. Nếu bạn quen Windows, việc đó cũng oke.

Nếu bạn muốn nhón chân vào DevOps, bạn nên biết sử dụng Linux và những command cơ bản. Cách hệ điều hành quản lý người dùng / quản lý file. Lại nói về tập đoàn tư bản to nhất VN, vẫn là những người lương ngàn $, **không hiểu ý tưởng chown / chmod là gì; scp báo không có quyền mà ngồi cả một buổi chiều không xử lý được; hay là không biết copy folder mà không có giao diện; không biết mount ổ cứng cơ bản**

Khi làm quen với Linux, bạn cần biết sử dụng một vài text editor cơ bản như nano / vim. Để học vim hay emacs thì lại là có thể là một bài blog cực dài khác, nhưng về cơ bản, bạn có thể dùng bất kì công cụ gì mà bạn muốn, miễn là nó work.

Ngoài ra, để làm Devops, bạn cần biết về cách quản lý network bằng câu lệnh sử dụng những tool cơ bản như netstat hay iptables. Thêm nữa, bạn cần biết về SSH / Public key + Private key, *authorized_keys* là gì, *known_hosts* là gì. Nếu bạn đã setup Github ở bước trên, khả năng cao bạn đã biết dùng privatekey để đẩy code lên Repo khá oke rồi, SSH cũng tương tự vậy.

# Level 2

to be continue 