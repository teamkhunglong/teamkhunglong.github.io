---
layout: post
title: "How to DevOps 101"
date: 2021-03-31 09:00:00 +0700
category: operations
author: minh
short-description: Getting started with DevOps
---

ref: [link 1](https://www.youtube.com/watch?v=5pxbp6FyTfk) [link 2](https://www.youtube.com/watch?v=9pZ2xmsSDdo)

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

Đến đây, mọi thứ có khi sẽ không còn vui vẻ như lúc đầu. Có thể bạn sẽ bắt đầu debug từ 8h tối hôm trước đến 6h sáng hôm sau mà không biết tại sao nó lại thế. Nhưng điều đó quan trọng, đây là xương sống của mọi thứ sau này. 

Level này lại gồm 3 phần nhỏ, nhưng thật ra mỗi phần lại có thể là một bài blog riêng biệt. 

## Hệ thống mạng (networking)

Không thể nào mà làm DevOps mà không biết về networking. Nếu mà ở trên nói về phần Dev, thì ở đây làm về phần Ops. Nếu OS là bê tông, thì Network là móng nhà. Đã rất nhiều lần mình phải đập hệ thống đi xây lại từ đầu vì mình thay đổi Network architecture. Vậy nên, việc có kiến thức về hệ thống mạng rất quan trọng.

Mình học Khoa học Máy tính (CompSci), không phải chuyên ngành về Network, nên những kiến thức ở đây mình cũng chỉ học tay ngang, khi cần cái gì mình sẽ học. Ở bước này, bạn nên đã có một dịch vụ nào đó đang chạy để định hình được làm sao để expose dịch vụ đó ra mạng Internet. Mình thì hay dùng nginx cho dễ, hoặc python http-server còn dễ hơn. 

Ý tưởng của phần này là hiểu được flow của các gói tin. Nếu khi lập trình, bạn cần phải hiểu control flow của chương trình; thì ở đây, bạn cần hiểu làm sao để người dùng sử dụng được dịch vụ của bạn.

Bắt đầu từ việc dễ nhất như **DHCP/NAT** là gì, làm sao để expose dịch vụ của bạn ra ngoài NAT. Trong lúc đó, bạn nên hiểu được **subnet** là gì? **gateway** là gì? Do hầu hết các dịch vụ cơ bản đều sử dụng giao thức (protocol) cơ bản như TCP / HTTP, bạn cũng nên đọc qua về các giao thức này. 

Sau khi vui vẻ đủ dùng, bạn cần hiểu được **DNS** ý tưởng như thế nào cũng như hoạt động ra làm sao. Ví dụ như việc bạn truy cập vào blog này sử dụng domain [teamkhunglong.com](https://teamkhunglong.com) thay vì một địa chỉ IP nào đó. Với mô hình nhỏ hơn như Kubernetes, thông thường những dịch vụ chạy trên đó cũng được tương tác với nhau hay được quản lý qua domain thay vì IP.

Sau đó, chúng ta cần trang bị những kiến thức cụ thể về DevOps ví dụ như Load Balancer hay Proxy Server. Làm sao khi người dùng truy cập vào domain [teamkhunglong.com](https://teamkhunglong.com), sau khi phân giải tên miền đến địa chỉ front-end, làm sao để nó được kết nối đến back-end. Những thuật toán load-balencing gồm có những gì. Làm sao để dựng proxy server để những VM / Container đứng sau mạng ảo có thể kết nối được với internet bên ngoài.

Thêm nữa, điều khá quan trọng và không thể thiếu được đó là firewall. Làm sao để chặn truy vấn đến các cổng được mở ra mạng Internet, làm sao để forward cổng dịch vụ được yêu cầu từ trong VM / Container ra mạng ngoài và chặn những cổng dịch vụ khác không cần thiết (ví dụ như port 22 SSH).

## Containerization

Nãy giờ nói về VM / Container nhiều rồi, mình cũng cần phải nói qua xem đây là cái gì.

Nếu bạn đang sử dụng Windows mà muốn dùng thử qua Ubuntu, khả năng cao bạn sẽ sử dụng phần mềm ảo hoá (virtual machine) ví dụ như VMWare. VMWare hay những phần mềm ảo hoá khác ví dụ như VirtualBox, Nox, Qemu, ... có nhiệm vụ giả lập một môi trường khác, đơn cử trong trường hợp này là Windows ảo hoá Linux. Công nghệ này gọi là **Virtualization**.

Bên cạnh đó, nếu bạn không cần giả lập cả một hệ điều hành, mà bạn vẫn muốn môi trường của mình được sạch sẽ khi deploy dịch vụ, tránh trường hợp *"ơ anh ơi nó chạy trên máy em bình thường mà"*; thì bạn phải có một công nghệ khác gọi là **Containerization**.

Trong trường hợp bạn cần có cả ảo hoá lẫn container hoặc các dịch vụ quản lý khác; hệ thống **Containerized on Virtualized** khá ổn và đa số các dịch vụ online đang sử dụng.

![][1]{:height="100%" width="100%"}

Nói tóm lại, công nghệ Containerization được định nghĩa là một môi trường độc lập, riêng biệt với hệ điều hành chủ. Ở đây, mình sẽ ưu tiên dùng Docker vì có nhiều hướng dẫn online để getting started with Docker, cũng như mình sử dụng Docker hàng ngày, thậm chí để build chiếc blog này ở local.

## Dịch vụ đám mây (cloud serivce)

Cuộc chơi DevOps hiện nay có 3 dân chơi chính là Amazon (AWS), Microsoft (Azure) và Google (Cloud). Về cơ bản, những công ty này tạo ra các dịch vụ để giúp công ty / doanh nghiệp deploy dịch vụ nhanh hơn, cũng là nguồn thu nhập chính.

Những tính năng có thể kể đến ví dụ như Datablob / Datalake, Virtual Machine / Virtual Network, Public IP, SQL Server, đến những dịch vụ khủng như Application Insight, Container Registry, Key Vault / Event Grid hay thậm chí có thể quản lý cả một mạng Kubernetes.

Tất cả những dân chơi này đều cung cấp phiên bản dùng thử hay phiên bản miễn phí cho người chơi thử nghiện. Một ngày đẹp trời, bạn mở billing ra thấy vài chục ngàn $ cũng là chuyện bình thường.

Mình thì không có nhiều tiền, nên mình thường làm homelab tại nhà và mua các linh kiện tương ứng. Dù sao thì làm homelab on the budget thì cũng oke, nếu không làm được thì mở quán net cũng được. Chứ mỗi tháng đóng họ cho Cloud Service cũng hơi căng thẳng.

# Level 3

Sau khi có xương sống cho một hệ thống DevOps, những thứ sau *optional but crucial, your choice* :shrug:

Đến bước này, tất cả lựa chọn đều là của bạn, nhưng về cơ bản, để làm DevOps chuẩn bài nên có những bước như sau

## Infrastructure as code

Cơ sở hạ tầng nghe to lắm, nhưng thực ra chỉ có 3 phần lớn cơ bản:
- Dev / Test
- Staging
- Production

Ý tưởng của 3 hệ thống riêng biệt như vậy là để Dev code những tính năng, sau đó chạy qua 1 lượt Unittest. Sau đó, chương trình / dịch vụ được build ra artifacts để đến bước Staging. Ở bước này, đội tester sẽ có hàng để check lại một lượt cuối trước khi ra Production. Bởi quản lý 3 hệ thống về cơ bản giống nhau, ta không nên làm thủ công mà nên tự động chúng. Và lúc đó, Teraform vào việc.

## CI/CD

Trong đầu mình mỗi khi nhìn vào Continuous Intergration / Continuous Delivery thì mình nghĩ ngay đến term "tự diễn biến / tự chuyển hoá".

Về cơ bản, code của Dev khi được push lên Dev branch, nó sẽ được verify bởi nhiều yếu tố khác nhau:
1. Code có build được không?
2. Code có pass unit test không?
3. Code có "đẹp" không?
4. Code có đảm bảo an toàn bảo mật / các tiêu chuẩn ISO không?
5. Code có va chạm với các code cũ không?
6. Code mới được phủ bao nhiêu phần trăm?

Những yếu tố trên không đảm bảo đầy đủ, nhưng ý mình là nó sẽ có một vài tiêu chuẩn như vậy. Để được merge vào master / main, code của Dev phải đảm bảo được tất cả những thứ đó. Nhưng mà, để mà commit nào cũng làm thủ công thì hơi căng thẳng, nên ta cần phải có CI/CD.

Tool để làm CI/CD thì vô vàn, dễ nhất là dựng 1 VM rồi đăng kí vào Agent pool để mỗi khi có commit nó sẽ tự động kéo về build. Vấn đề là, đến khi có nhiều Dev, việc 1 agent không thể đảm nhiệm được hết công việc; vì vậy, chúng ta cần nhiều Agent và chạy on-demand. Có thể kể đến Travis-CI, Jenkins làm nhiệm vụ này rất tốt. Thậm chí, ta có thể sử dụng Kubernetes để làm CI/CD. Ý tưởng vẫn như cũ.

## Orchestration

Để nói về DevOps mà không có Orchestration thì chắc không gọi là DevOps. Làm sao có thể tự động hoá mà không có kịch bản? 

Ví dụ thế này, mình đang làm một work flow tương tác với database. Mỗi khi nào có data mới được đẩy vào database, mình cần phải gọi một worker để deal với database đó. Câu hỏi đặt ra là làm sao để tối ưu?

Hoặc là, mình có 1 chiếc front-end, 1 chiếc back-end, 1 chiếc load-balancer, 1 chiếc database, hoặc sau này mình sẽ cần scale lên nhiều front-end chẳng hạn. Làm sao để có thể tự động hoá được, và làm sao để có redundancy?

Khi ấy, thay vì làm thủ công các công việc, ta có để đóng hết vào trong Container và đưa vào một hệ thống quản lý như Kubernetes. Ý tưởng của Kubernetes quản lý các Container theo "kịch bản". Ngoài ra, Kubernetes có thể tạo được redundancy nhanh chóng, có thể scale dễ dàng. Như ý tưởng bên trên, ta có thể tạo một service làm CI/CD agent và chạy trên hệ thống Kubernetes vì về cơ bản agent bản chất cũng là một Container. Ngoài Deployment Application, ta có thể tạo Job, chạy on-demand.

Người chơi hệ Kubernetes có rất nhiều trên thị trường. Hiện tại mình đang tự dựng vài node cluster ở nhà, cũng như sử dụng Azure Kubernetes Service ở công ty. Theo như mình biết, Amazon cũng có dịch vụ này.

Thậm chí, ta có thể tạo kịch bản ngay trên giao diện với Azure App Insights cũng như Rancher cho custom Node. Ez devops?

## Monitoring

Cuối cùng, cũng không kém phần quan trọng, đó là monitoring. Làm sao để biết được khi nào thì job completed, khi nào thì service hang? Resource dùng đã hết chưa, hay dùng bao nhiêu %? Có cần scale hệ thống lên tiếp không hay bị bottle-neck ở đâu?

Khi ấy, ta cần một tool làm nhiệm vụ giám sát hệ thống. Cũng có rất nhiều tool để làm việc này, trong số đó có Prometheus, Splunk, ... làm nhiệm vụ này rất tốt, và có giao diện web, thay vì phải dùng kubectl cli.

# Kết luận

Sau khi tổng kết lại, ta có Tech Stack như sau để nhúng một chân vào cuộc chơi DevOps. Trông có vẻ nhiều, nhưng không hẳn là phải master hết tất cả công cụ để có thể làm được. Hi, chúc các bạn may mắn ~~

![][2]{:height="100%" width="100%"}

[1]: {{ site.baseurl }}/assets/img/2021/03/deployment-and-container.png "Deployment & Container"
[2]: {{ site.baseurl }}/assets/img/2021/03/devops-big-picture.png "DevOps big picture"