---
layout: post
title: "Crypto Mining"
date: 2020-04-26 17:00:00 +0700
category: hacks
author: minh
short-description: Down to the rabbit hole - ETH mining
---

# Mục tiêu

Với lượng kiến thức ít ỏi của mình, mình đào coin, bởi vì:
1. Do dịch Covid, mọi người có thời gian rảnh ở nhà trading, không chỉ giá crypto mà giá chứng khoán cũng biến động đáng kể, về cơ bản là tăng.
2. Do dịch Covid, nguồn cung chip bán dẫn (SoC) không đáp ứng đủ nhu cầu của thị trường, nên tất cả mọi linh kiện điện tử đều bị trì trệ theo một cách nào đó; trong đó có card màn hình (GPU), là thành phần chính trong việc đào tiền ảo, cụ thể ở đây là ETH. Vì vậy, thị trường càng khó để đào ETH, cũng dẫn đến việc giá ETH tăng.
3. Do mình cần chạy Homelab, về cơ bản ở nhà mình đã có nhiều PC/workstation/server. Hầu hết những máy này không sử dụng đến chức năng xử lý đồ hoạ, nên mình còn thừa rất nhiều chân cắm GPU.
4. Mình đã có sẵn một vài chiếc GPU ở nhà qua những năm tháng đi học và tích góp mua máy tính. Việc sử dụng tối đa năng suất của những chiếc card này khiến mình cảm thấy đỡ phí số tiền mình đã bỏ ra.

Sau tất cả những lý do trên, mình quyết định đào coin để kiếm tiền trả chi phí sinh hoạt hàng tháng (điện - nước - mạng) cũng như kiếm thêm một chút để được ăn cơm có thịt.

Mình sẽ không đào coin nếu mình không có kiến thức về Công nghệ Thông tin, hoặc mình phải đầu tư hệ thống từ đầu.

# Phương pháp

Với các "dân đào chuyên nghiệp", họ sẽ xây một máy đào gồm nhiều GPU (khoảng 6-8 chiếc). Vốn đầu tư cho những linh kiện khác ngoài GPU khá thấp, thường là một chiếc mainboard Tàu với nhiều slot PCI-e, cộng thêm các linh kiện khác như CPU / RAM / ổ cứng ở mức tối thiểu, nguồn cũng không phải loại cực tốt. Họ sẽ ưa chuộng loại hệ điều hành giành riêng cho việc đào coin có thể ví dụ như HiveOS. Khi sử dụng cách làm này, máy đào chỉ có nhiệm vụ đào coin và không thể làm việc gì khác. Đây vừa là ưu điểm, vừa là khuyết điểm.

Đối với mình, do mình đã có một vài chiếc Workstation từ trước, nên việc mình cắm thêm GPU vào để đào coin sẽ làm tối ưu năng suất của những máy tính hiện có. Với cách làm này, mình có thể tận dụng CPU / RAM còn thừa để làm những ứng dụng khác, xoay quanh những dịch vụ Homelab chẳng hạn.

Do các phần mềm đào coin chủ yếu nằm trên hệ điều hành Windowx hay hệ điều hành Linux-based, nên mình cần phải có cách nào đó để cung cấp môi trường cho những chiếc card. Tại đây, mình sử dụng phương pháp ảo hoá Windows sử dụng Proxmox và passthrough GPU vào máy ảo. Từ đây, mình bắt đầu đâm đầu vào rabbit hole và không có lối thoát. 

Mọi chuyện sẽ rất đơn giản nếu mình chỉ cần tạo một vài máy ảo Ubuntu để học lập trình, nhón chân vào DevOps, nhưng khi nói chuyện về việc sử dụng phần cứng, cụ thể ở đây là GPU thì lại là một câu chuyện khác. Phương pháp của mình không sử dụng cài đặt trực tiếp hệ điều hành lên máy tính, nên máy ảo ở chế độ mặc định sẽ không biết nó đang có những phần cứng gì. Để cung cấp phần cứng cho máy ảo, ta cần một tính năng đó là IOMMU (Input–output memory management unit)

Ở thế giới server, khi nói về những card màn hình có chức năng ảo hoá (SR-IOV - Single-root input/output virtualization), thì thường nó sẽ có giá trên trời. Bạn có thể tham khảo giá card RTX A6000 và RTX 3090 bởi hai con chip xử lý giống y hệt nhau, cùng số CUDA core. Mình không có tiền để mua những card enterprise, nên mình sẽ dùng những chiếc card consumer như chiếc RTX 3080 mà mình phải giấu ny mua với giá 24.5tr.

Khi sử dụng những linh kiện thông thường, để passthrough thì CPU / Mainboard cần phải có trong danh sách hỗ trợ IOMMU. Do mình thường sử dụng các CPU hiệu năng cao, nên tất cả CPU mình sử dụng đều hỗ trợ tính năng này.

Tiếp đến việc chọn hệ điều hành, để sử dụng môi trường ảo hoá, có 3 công nghệ lớn nhất hiện nay là QEMU-KVM, Xen và VMware ESxi. Vẫn là câu chuyện do mình nghèo, nên mình sử dụng đồ opensource và free, nên mình lựa chọn QEMU-KVM. Thêm nữa, có nhiều hệ điều hành hỗ trợ QEMU-KVM, nhưng mình thấy hệ điều hành thân thiện người dùng nhất là Proxmox.

Sau khi cài đặt Proxmox, mình tiến hành cài VM Windows và Passthrough GPU. Việc chọn Windows hay HiveOS ở bước này thì tuỳ mỗi người, nhưng mình cũng cần dùng Windows ở một vài trường hợp, nên mình chọn Windows. ~~(Down to the rabbit hole: sau khi chạy thì mình nhận ra Windows khá là unstable)~~

Sau khi cài đặt VM Windows, mình sẽ cài đặt các phần mềm cần thiết và tham gia vào mining pool. Do hiệu năng đào của mình thấp, nên mình lựa chọn ethermine, pool này có lựa chọn payout chỉ từ 0.1 ETH, khá phù hợp với năng suất đào của mình.

Nếu như thông thường, giả sử máy đào bị not-resonding, bạn cần phải bật/tắt một cách vật lý; thì khi sử dụng Proxmox, bạn có thể bật/tắt máy ảo qua giao diện web như khi sử dụng VMWare hay VirtualBox.

Việc cuối cùng phải làm chỉ là ngồi đợi tiền về ví thôi :D Hi

# Kết

Bài blog đầu tiên này có thể là wall-of-text, nhưng mình sẽ cố gắng edit lại vào đợt rảnh 30/4-1/5 tới. Thanks you all.