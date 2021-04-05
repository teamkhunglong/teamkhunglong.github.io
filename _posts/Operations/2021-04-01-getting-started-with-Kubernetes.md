---
layout: post
title: "Getting started with Kubernetes"
date: 2021-04-01 09:00:00 +0700
category: operations
author: minh
short-description: Kubernetes - my pain in the ass
---

TL;DR Blog cực kì xiao lone, bạn nên đọc trên blog [kubernetes.io](https://kubernetes.io/docs/home/) để có được content chính xác nhất

Tiếp tục câu chuyện về tập đoàn tư bản hàng đầu VN, anh lead mình bắt mình viết một cái guide kiểu Getting Started with Kubernetes, nên mình viết chiếc blog này. Cũng là để giới thiệu với những bạn nào mới muốn nhún chân vào làm về Kubernetes thì có thể hiểu được nó có những cái gì.

Dù website gốc có rất nhiều thông tin, mình sẽ chỉ tóm gọn lại rất cơ bản những thứ mình thích nói vào blog ở đây, như một cách giới thiệu về concept của Kubernetes.

# Understand the basics

The Concepts section helps you learn about the parts of the Kubernetes system and the abstractions Kubernetes uses to represent your cluster, and helps you obtain a deeper understanding of how Kubernetes works.

## Tổng quát

Get a high-level outline of Kubernetes and the components it is built from.

### Kubernetes là gì?

Kubernetes là một nền tàng (platform) mã nguồn mở, dễ dàng sử dụng cũng như mở rộng. Nhiệm vụ của Kubernetes là quản lý các công việc trong container hoặc quản lý các dịch vụ, dễ dàng tự động hoá cũng như cấu hình dịch vụ / công việc. Các dịch vụ, công cụ của Kubernetes được phổ biến và hỗ trợ rộng rãi.

![][1]{:height="100%" width="100%"}

Ngày xưa, các dịch vụ được chạy trên những server vật lý. Giả sử, nếu hai dịch vụ cùng chạy trên 1 server vật lý, nếu một dịch vụ dùng hết tài nguyên của hệ thống, dịch vụ kia sẽ không còn tài nguyên để chạy. Để khắc phục vấn đề này, mỗi dịch vụ sẽ phải chạy trên những server vật lý khác nhau. Việc mua thêm server vật lý có thể là một lời giải cồng kềnh, hơn nữa, còn phải nuôi nhiều nhân công để quản lý server vật lý.

Khi đó, công nghệ ảo hoá được sinh ra. Thay vì phải sử dụng nhiều server vật lý, ta chỉ cần dùng một server có sức mạnh lớn hơn, và chia tài nguyên cho từng máy ảo (VM). Mỗi máy ảo sẽ có đủ tính năng của một server vật lý bình thường, bao gồm cả một hệ điều hành hoàn chỉnh.

Hiện tại, nếu nhiều dịch vụ chỉ được phân chia vào từng VM như thiết kế cũ, nhưng môi trường hoạt động của chúng giống nhau (ví dụ cùng chạy trên Ubuntu 64-bit 18.04 LTS) thì phần tài nguyên để quản lý hệ điều hành sẽ bị lãng phí. Công nghệ Container sinh ra để giải quyết vấn đề này, bao gồm có những tính năng về chia sẻ CPU, RAM, file, ... như công nghệ ảo hoá.

Ngoài ra, công nghệ container còn ưu việt hơn ở một số điểm:
- Tạo và triển khai ứng dụng theo công nghệ Agile dễ hơn so với VM.
- Quản lý CI/CD dễ dàng, tự động hơn so với VM.
- Có nhiều thang đo thông tin hơn so với VM, ví dụ như trạng thái của dịch vụ.
- Nhất quán về môi trường chạy dịch vụ (it works on my machine)
- Dễ dàng dựng trên các hệ thống khác nhau: vật lý, cloud (Amazon, Microsoft, Google) với mọi loại hệ điều hành (Ubuntu, Windows)
- Các dịch vụ được quản lý phân tán, thay vì tập trung như VM.

#### Dùng Kubernetes khi nào?

Container là một cách tối ưu khi phát triển dịch vụ. Giả sử, bạn cần quản lý n-dịch vụ và không được có downtime, nhưng một dịch vụ chết, thì Kubernetes sẽ tự động cung cấp dịch vụ mới, thậm chí có thể không có downtime. Kubernetes có thể mở rộng quy mô của dịch vụ hay tạo thêm những dịch vụ dự phòng một cách dễ dàng.

Các tính năng của Kubernetes:
- Quản lý dịch vụ và cân bằng tải: Kubernetes có thể cung cấp dịch vụ ra mạng ngoài qua DNS name của dịch vụ. Nếu một dịch vụ đang gặp lưu lượng mạng lớn, kubernetes có thể cân bằng tải lưu lượng mạng qua những node dịch vụ khác.
- Điều phối lưu trữ: Có thể dễ dàng tích hợp hệ thống lưu trữ vào mạng Kubernetes, ví dụ như ổ cứng vật lý hay dữ liệu trên cloud.
- Tự động triển khai và khôi phục (rollout & rollback): Kubernetes có thể tự động triển khai một phiên bản mới của dịch vụ và thu hồi tài nguyên của phiên bản cũ, cũng như khôi phục lại theo yêu cầu.
- Tự động lựa chọn tài nguyên: Kubernetes có thể nhận yêu cầu về tài nguyên (RAM, CPU) và chia sẻ vào các cụm Node phù hợp để chạy dịch vụ đó.
- Tự sửa chữa: Nếu một dịch vụ không hoạt động đúng theo kịch bản hoặc chết (fail health check), Kubernetes có thể xoá bỏ container đó và tạo một container mới.
- Quản lý thông số và mật mã: Kubernetes có thể quản lý các thông tin về mật khẩu, OAuth token, SSH Keys một cách tự động và sẽ chỉ cung cấp thông tin khi được người dùng định nghĩa.

#### Không dùng Kubernetes khi nào? 

to-be-continue

### Thành phần của Kubernetes

Một mạng Kubernetes gồm thành phần quản lý (control plane) và một hoặc nhiều máy gọi là Node.

### Kubernetes API 

API, là thành phần core trong Kubernetes, được cung cấp cho người dùng để tương tác với thực thể (object) trong Kubernetes. Người dùng, những như các Node sẽ tương tác với mạng Kubernetes qua các API này.

### Thực thể trong Kubernetes

[1]: {{ site.baseurl }}/assets/2021/04/container_evolution.svg "Container Evolution"