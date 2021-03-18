---
layout: post
title: "What do you need?"
date: 2021-03-16 21:50:00 +0700
category: operations
author: minh
short-description: This blog seems cool, what now?
---

Đây sẽ là một series thập cẩm tiếng anh / tiếng việt chẳng ra gì nhưng mà là nơi để mình lưu lại các trải nghiệm về devops. Những bài trong blog này được tham khảo bởi nhiều nguồn khác nhau; trong đó hầu hết là github & youtube. Mình sẽ cố gắng ref nhiều nhất có thể. Nếu các bạn quan tâm và có câu hỏi gì, bạn có thể inbox cho mình qua các phương tiện liên lạc có thể có.

# What do you need?

Điều đầu tiên khi bạn bấm vào tab này, bạn phải tìm hiểu được mình muốn cái gì.

Do thể loại của tab này là DevOps, mình sẽ nói nhiều về các vấn đề về hệ thống mạng. Với những nhu cầu khác nhau, hệ thống mạng của nhà mỗi người cũng khác nhau. Kể cả nhà chung cư có cùng một thiết kế, tùy thuộc vào gia chủ, cách thiết kế mạng của mỗi nhà lại khác nhau. 

![][1]{:height="50%" width="50%"}

Hệ thống mạng này đã đủ để sử dụng thoả mãn những nhu cầu cơ bản như truy cập internet, chơi game với độ trễ thấp.

Mặc dù vậy, giả sử một ngày đẹp trời, bạn muốn điều khiển máy tính ở nhà "một cách an toàn" chẳng hạn. Bạn sẽ làm gì?

# Remote control home PC

Với những tiện ích có sẵn, chắc chắn các bạn sẽ chọn những dịch vụ như [TeamViewer](https://www.teamviewer.com/en/), [AnyDesk](https://anydesk.com/en), [Chrome Remote Desktop](https://remotedesktop.google.com/). Những dịch vụ này hoạt động rất tốt công việc của mình. Bên cạnh đó, có một vài điểm yếu chết người như sau:
1. TeamViewer: Phải trả phí nếu không dùng "cá nhân"
2. AnyDesk: Như TeamViewer nhưng lại ít chức năng hơn
3. Chrome Remote Desktop: **MIỄN PHÍ** nhưng phải dùng qua Chrome, không pass-through được vài tổ hợp phím liên quan đến trình duyệt, ví dụ Ctrl-W

Do mình lười, lại còn nghèo, nên mình quyết định mua một chiếc VPS cơ bản nhất với mức giá 5$/tháng. Rõ ràng là việc mua VPS rẻ hơn mua TeamViewer (24.9$), mà mua VPS lại còn làm được nhiều thứ nữa. Ví dụ như sau:

![][2]{:height="100%" width="100%"}

Nếu mình kết nối các thiết bị với VPS / VPN, các máy này sẽ nhìn nhau như mạng local. Khi đó, mình có thể sử dụng các dịch vụ free để điều khiển máy tính sử dụng các giao thức như RPD hay VNC. 

Như vậy, mình có thể cầm laptop / điện thoại / máy tính bảng để kết nối remote về máy nhà mà chỉ mất 5$/tháng.

Nếu không muốn mất tiền, bạn có thể sử dụng Chrome Remote Desktop. Ngoài việc nó miễn phí, phần mềm này còn tự thay đổi đường mạng tối ưu thay vì phải đi lên server của Google.

## Lưu ý

Nhiều bạn nghĩ rằng có thể tạo VPN Server trên ISP Modem rồi mở port ra ngoài, làm vậy sẽ đỡ tốn 5$. Nếu hợp đồng mạng không cấp IP tĩnh, luôn có những dịch vụ NoIP cấp cho bạn một domain miễn phí rồi tự trỏ lại về IP của nhà bạn. 

Mình không bảo rằng cách này sai, nhưng việc mở port modem tại nhà tạo nên một attack surface khá lớn. Hơn nữa, chưa chắc ISP đã cho bạn mở port modem. Để mà nói, 5$ mà để đỡ bị hack thì ai mà chẳng thích chứ :3

Do mình đã mua domain rồi, nên mình chọn mua VPS rồi dùng Cloudflare trỏ về. Đây hoàn toàn là lựa chọn cá nhân, mình thấy tiện thì mình làm thôi.

# Homelab 101?

Giả sử, bạn muốn lắp mấy cái camera an ninh tại nhà, bạn mua một hộp camera box về và nối với một chiếc camera. Mở một port trên modem rồi kết nối tới app điện thoại để xem trực tiếp.

Mấy hôm sau, bạn muốn host một chiếc blog tại nhà, ví dụ như blog này chẳng hạn. Bạn tạo một chiếc VM rồi expose port đó ra mạng internet.

Mấy hôm sau nữa, bạn muốn nghịch smarthome một chút, ví dụ như mở cửa gara, bật / tắt bình nóng lạnh, bật / tắt đèn. Bạn lại tạo một chiếc VM rồi expose port ra mạng internet.

Bạn có niềm đam mê với phim ảnh, bạn đã lưu được cả một hệ thống vài trăm GB tài liệu học tập trên máy tính PC ở nhà, nhưng bạn lại muốn lên giường xem hoặc là đi ra ngoài vẫn xem được.

Nói chung, những dịch vụ / tiện ích là vô vàn, và việc mở port trên modem là một việc khá là risky =)) Chỉ tốn 5$/tháng; mình đã có một mạng ảo khá an toàn để dựng những dịch vụ như vậy, biết đâu lại mở ra cho mình nhiều cơ hội mới.

Do đó, mình mới refactor lại hệ thống mạng ở nhà mình như hình dưới.

![][3]{:height="100%" width="100%"}

# Kết

Series DevOps của blog này thực chất là để mình log lại những lựa chọn của mình cũng như để mình nhớ cách setup các thứ nhỡ sau này có vấn đề gì phải troubleshoot; cũng như để các bạn đang muốn tìm hiểu về homelab / smarthome tham khảo các thứ.

Hi, that's it for today.

[1]: {{ site.baseurl }}/assets/2021/03/normal-topo.png "Normal Topo"
[2]: {{ site.baseurl }}/assets/2021/03/normal-vps-network.png "Normal VPS Network"
[3]: {{ site.baseurl }}/assets/2021/03/my-home-network.png "My Home Network"