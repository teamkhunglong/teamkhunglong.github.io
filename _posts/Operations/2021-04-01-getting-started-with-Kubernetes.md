---
layout: post
title: "Getting started with Kubernetes"
date: 2021-04-01 09:00:00 +0700
category: operations
author: minh
tags: operations kubernetes
short-description: Kubernetes - Overview Concept (my pain in the ass)
---

TL;DR Blog cực kì xiao lone, bạn nên đọc trên blog [kubernetes.io](https://kubernetes.io/docs/home/) để có được content đầy đủ nhất

Tiếp tục câu chuyện về tập đoàn tư bản hàng đầu VN, anh lead mình bắt mình viết một cái guide kiểu Getting Started with Kubernetes, nên mình viết chiếc blog này. Cũng là để giới thiệu với những bạn nào mới muốn nhún chân vào làm về Kubernetes thì có thể hiểu được nó có những cái gì.

Dù website gốc có rất nhiều thông tin, mình sẽ chỉ tóm gọn lại rất cơ bản những thứ mình thích nói vào blog ở đây, như một cách giới thiệu về concept của Kubernetes.

Đây là bài 1 trong chuỗi series về Kubernetes được dịch và tóm gọn lại từ website gốc.

# Ý tưởng về Kubernetes 

Tại đây, mình sẽ giới thiệu các khái niệm cơ bản để hiểu rõ hơn về hệ thống cũng như các tính năng khái quát của một mạng Kubernetes. Từ đó, bạn có thể hiểu sâu hơn về cách vận hành của nó.

## Tổng quát

Phần này sẽ làm rõ về tổng quan một hệ thống Kubernetes và các thành phần tạo nên nó.

### Kubernetes là gì?

Kubernetes là một nền tàng (platform) mã nguồn mở, dễ dàng sử dụng cũng như mở rộng. Nhiệm vụ của Kubernetes là quản lý các công việc qua container hoặc quản lý các dịch vụ, dễ dàng tự động hoá cũng như cấu hình dịch vụ / công việc. Các dịch vụ, công cụ của Kubernetes được phổ biến và hỗ trợ rộng rãi.

![][1]{:height="100%" width="100%"}

Ngày xưa, các dịch vụ được chạy trên những server vật lý. Giả sử, nếu hai dịch vụ cùng chạy trên 1 server vật lý, nếu một dịch vụ dùng hết tài nguyên của hệ thống, dịch vụ kia sẽ không còn tài nguyên để chạy. Để khắc phục vấn đề này, mỗi dịch vụ sẽ phải chạy trên những server vật lý khác nhau. Việc mua thêm server vật lý có thể là một lời giải cồng kềnh, hơn nữa, còn phải nuôi nhiều nhân công để quản lý server vật lý.

Khi đó, công nghệ ảo hoá được sinh ra. Thay vì phải sử dụng nhiều server vật lý, ta chỉ cần dùng một server có sức mạnh lớn hơn, và chia tài nguyên cho từng máy ảo (VM). Mỗi máy ảo sẽ có đủ tính năng của một server vật lý bình thường, bao gồm cả một hệ điều hành hoàn chỉnh.

Hiện tại, nếu nhiều dịch vụ chỉ được phân chia vào từng VM như thiết kế cũ, nhưng môi trường hoạt động của chúng giống nhau (ví dụ cùng chạy trên Ubuntu 64-bit 18.04 LTS) thì phần tài nguyên để quản lý hệ điều hành sẽ bị lãng phí. Công nghệ Container sinh ra để giải quyết vấn đề này, bao gồm có những tính năng về chia sẻ CPU, RAM, file, ... như công nghệ ảo hoá nhưng lại khắc phục được điểm yếu khi phải quản lý cả hệ điều hành.

Ngoài ra, công nghệ container còn ưu việt hơn ở một số điểm:
- Tạo và triển khai ứng dụng theo công nghệ Agile dễ hơn so với VM.
- Quản lý CI/CD dễ dàng, tự động hơn so với VM.
- Có nhiều thang đo thông tin hơn so với VM, ví dụ như trạng thái của dịch vụ.
- Nhất quán về môi trường chạy dịch vụ (it works on my machine)
- Dễ dàng dựng trên các hệ thống khác nhau: vật lý (on-premise) hay cloud (Amazon, Microsoft, Google) với mọi loại hệ điều hành (Ubuntu, Windows)
- Các dịch vụ được quản lý phân tán, thay vì tập trung như VM.

#### Dùng Kubernetes khi nào?

Container là một cách tối ưu khi phát triển dịch vụ. Giả sử, bạn cần quản lý n-dịch vụ và không được có downtime, nhưng một dịch vụ chết, thì Kubernetes sẽ tự động cung cấp dịch vụ mới, thậm chí có thể không có downtime. Kubernetes có thể mở rộng quy mô của dịch vụ hay tạo thêm những dịch vụ dự phòng một cách dễ dàng.

Các tính năng của Kubernetes:
- Quản lý dịch vụ và cân bằng tải: Kubernetes có thể cung cấp dịch vụ ra mạng ngoài qua DNS name của dịch vụ. Nếu một dịch vụ đang gặp lưu lượng mạng lớn (high traffic), kubernetes có thể cân bằng tải lưu lượng mạng qua những node dịch vụ khác.
- Điều phối lưu trữ: Có thể dễ dàng tích hợp hệ thống lưu trữ vào mạng Kubernetes, ví dụ như ổ cứng vật lý hay dữ liệu trên cloud.
- Tự động triển khai và khôi phục (rollout & rollback): Kubernetes có thể tự động triển khai một phiên bản mới của dịch vụ và thu hồi tài nguyên của phiên bản cũ, cũng như khôi phục lại theo yêu cầu.
- Tự động lựa chọn tài nguyên: Kubernetes có thể nhận yêu cầu về tài nguyên (RAM, CPU) và chia sẻ vào các cụm Node phù hợp để chạy dịch vụ đó.
- Tự sửa chữa: Nếu một dịch vụ không hoạt động đúng theo kịch bản hoặc chết (fail health check), Kubernetes có thể xoá bỏ container đó và tạo một container mới.
- Quản lý thông số và mật mã: Kubernetes có thể quản lý các thông tin về mật khẩu, OAuth token, SSH Keys một cách tự động và sẽ chỉ cung cấp thông tin khi được cho phép.

#### Những điểm khác biệt giữa Kubernetes và hệ thống truyền thống 

Một hệ thống từ trước đến nay thường là một thể thống nhất. Ví dụ những tính năng như triển khai mã nguồn, mở rộng quy mô, cân bằng tải, ghi nhật kí, giám sát, cảnh báo thường được tích hợp trong một khối; thì Kubernetes sẽ hướng tới việc module hoá các công việc trên. Như kiểu chơi lego vậy.

Những thứ cần lưu ý khi dùng Kubernetes:
- Nếu ứng dụng chạy được bằng Container, thì sẽ chạy được trên Kubernetes. Những công việc xử lý được rất đa dạng, kể cả những công việc stateless / stateful ([tham khảo](https://www.redhat.com/en/topics/cloud-native-apps/stateful-vs-stateless)) hay tác vụ xử lý dữ liệu.
- Không cung cấp những dịch vụ ở cấp ứng dụng ví dụ như hệ thống xử lý dữ liệu (như Spark), hay cơ sở dữ liệu (như MySQL), hệ thống lưu trữ (như Ceph) một cách mặc định. Nhưng những ứng dụng này vẫn có thể được dựng và chạy trên mạng Kubernetes.
- Không yêu cầu mặc định các phương pháp giám sát hoặc cảnh báo, nhưng có thể tích hợp với các phương pháp chuyên nghiệp hơn để thu thập và trích xuất các thông tin cần thiết.
- Không bắt buộc phải dùng cấu hình ngôn ngữ/hệ thống, mọi API có thể được định nghĩa tuỳ ý.
- Không cung cấp bất kì hệ thống cấu hình, bảo trì, quản lý, tự sửa chữa một cách toàn diện nào.
- Không phải hệ thống điều phối đơn thuần, Kubernetes bao gồm các quy trình điểu khiển độc lập và có thể kết hợp được dễ dàng.

### Thành phần của Kubernetes

Khi bạn triển khai một mạng `Kubernetes`, bạn sẽ có một `Cluster`. Cluster bao gồm một hoặc nhiều worker, gọi là `Node`. Mỗi node sẽ chạy một hoặc nhiều ứng dụng được `containerized`.

Mỗi worker node có nhiệm vụ chạy các `Pods`. Một Pod là một container đang được chạy, một công việc có thể yêu cầu một hoặc nhiều Pod.

Lớp quản lý của mạng Kubernetes gọi là `Control Plane`, mình hay gọi là `server node` để phân biệt với `worker node`. Trong khi worker node làm nhiệm vụ chạy các công việc được yêu cầu, thì server node chỉ làm nhiệm vụ quản lý.

![][2]{:height="100%" width="100%"}

Trong môi trường production, một hệ thống Kubernetes thường có nhiều `server node` và `worker node`, cung cấp sự sẵn sàng cao (high availability - HA). Trong thực tế, mình thường có 2 server node và 3 worker node.

#### Thành phần quản lý

Thành phần quản lý sẽ đảm nhiệm việc đưa ra các quyết định cho một mạng Cluster, cũng như phát hiện và phản ứng trước một sự kiện nào đó trọng mạng. Ví dụ, ta muốn tạo 2 service front-end và sử dụng cân bằng tải thì sẽ phải đăng kí với `control plane`. Thành phần quản lý gồm các thành phần con như sau:

##### kube-apiserver 

Cung cấp chính các API trong mạng Kubernetes. Đây là front-end của Cluster. kube-api được thiết kế để mở rộng theo chiều ngang, có nghĩa là bạn có thể chạy nhiều kube-apiserver trên nhiều máy khác nhau và cân bằng lưu lượng mạng giữa các API server đó.

##### etcd

Là một nơi lưu trữ thông tin của mạng Kubernetes. Có thể sử dụng để lưu mật khẩu, OAuth token, SSH Keys, docker cred ...

Do là nơi lưu trữ thông tin nên hoàn toàn có thể sử dụng cơ sử dữ liệu bên ngoài khác ví dụ như MySQL.

##### kube-scheduler 

Nhiệm vụ chính của Scheduler là phân chia các Pod vào các Worker node một cách hợp lý. Ví dụ 1 Worker node có 16GB ram, khi ta chạy 3 Pod, Pod thứ 3 sẽ được phân chia vào một Worker node khác nếu còn tài nguyên.

##### kube-controller-manager 

Nhiệm vụ của Controller là để xử lý các công việc khác nhau:
- Node Controller: chịu trách nhiệm thông báo & phản hồi nếu một node bị chết.
- Job Controller: thực hiện và giám sát các Job, tạo một hoặc nhiều Pod tương ứng để thực hiện Job theo yêu cầu.
- Endpoints Sontroller: kết nối các thành phần dịch vụ và pod (ví dụ như gán IP ngoài tới hệ thống cân bằng tải, sau đó nối đến front-end)
- Service Account & Token controllers: cung cấp các thông tin được lưu trong etcd đến các Pod nếu có yêu cầu.

##### cloud-controller-manager 

Là thành phần kết nối Cluster đến các Cloud Provider. Những hệ thống ví dụ như Azure Kubernetes Service (AKS) sẽ có nhiều tính năng liên quan đến thành phần này. Ví dụ để kết nối AKS với ACR (Azure Container Registry) mà không cần đăng nhập qua Docker. Hoặc ví dụ để kết nối đến các load balancer của Cloud.

#### Thành phần trên mỗi worker node

Trên mỗi worker node sẽ gồm có 2 thành phần, làm nhiệm vụ nhận lệnh từ server node và duy trì các Pod. 

##### kube-proxy 

Là một network-proxy, làm nhiệm vụ duy trì kết nối mạng trong Node, giúp truyền tải các gói tin trong và ngoại Node

##### kubelet

Là `Agent Pod` chạy trên mỗi node, làm nhiệm vụ chạy các container. Kubelet sẽ lấy cấu hình `PodSpec` được nhận từ server node và dựng lên những Pod với cấu hình đó, đảm bảo việc Pod được chạy ổn định.

#### Container runtime

Là một phần mềm đảm nhiệm môi trường container. Có thể là Docker, [containerd](https://containerd.io/docs/), [CRI-O](https://cri-o.io/), ...

#### Addon

Là các dịch vụ khác của Kubernetes như DaemonSets, Deployments, ... thường nằm trong namespace kube-system. Những tính năng thường có bao gồm:
1. DNS: serve DNS records (chịu, không tìm được từ Tiếng Việt)
2. WebUI: giao diện Web để dễ quản lý (thậm chí từ điện thoại)
3. Resource Monitoring: quản lý tài nguyên, hiển thị các thông số hệ thống, thường được tích hợp trong giao diện Web.
4. Cluster-level Logging: self-explained :shrug:

### Kubernetes API 

API, là thành phần core trong Kubernetes, được cung cấp cho người dùng để tương tác với đối tượng (object) trong Kubernetes. Người dùng, những như các Node sẽ tương tác với mạng Kubernetes qua các API này.

Có thể kể đến `kubectl` hay `kubeadm` là những tool rất tiện lợi để tương tác với Kubernetes Cluster.

### Đối tượng trong Kubernetes

#### Kubernetes Object là gì

Kubernetes Object là một thực thể cụ thể trong hệ thống Kubernetes, những thực thể này mô tả trạng thái của Cluster. Cụ thể hơn:
- Ứng dụng nào đang được chạy, và được chạy trong Node nào.
- Tài nguyên có sẵn cho các ứng dụng.
- Các luật được áp dụng cho ứng dụng. Ví dụ như khả năng tự khởi động lại, tự sửa lỗi, hay tự nâng cấp.

Kubernetes Object có 2 trường cần lưu ý là `Spec` và `Status`.
- Spec: trang thái mong muốn của đối tượng. Ví dụ: ứng dụng này sẽ triển khai docker images nginx.
- Status: trạng thái hiện tại của đối tượng. Ví dụ: ứng dụng này có 1 phiên bản đang được chạy, 2 phiên bản khác đang được triển khai.

Tìm hiểu thêm về việc mô tả (describe) một đối tượng ở [đây](https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/#describing-a-kubernetes-object)

#### Quản lý Kubernetes Object

Trong đa số trường hợp, chúng ta sẽ sử dụng công cụ `kubectl` để quản lý các đối tượng trong mạng Kubernetes. Có 3 cách để điều khiển một đối tượng:
1. Imperative commands: sử dụng câu lệnh để điều khiển trực tiếp đối tượng.
2. Imperative object configuration: sử dụng file cấu hình để điều khiển đối tượng.
3. Declarative object configuration: sử dụng tập hợp các file cấu hình để điều khiển một hoặc nhiều đối tượng.

#### Name & ID 

Name và ID được sinh ra để phân biệt giữa các đối tượng trong một loại tài nguyên cụ thể. Ví dụ:
- 2 Pod không thể cùng tên là `myapp-123`
- Pod có thể tên là `myapp-123` và Deployment hay Job đồng thời cũng có thể tên là `myapp-123`

Để truy cập vào đối tượng này, có thể sử dụng API tại `/api/v1/pods/some-name`.

#### Namespace

Namespace được sinh ra với nhiệm vụ làm một môi trường ảo, phân biệt với môi trường thật. Giả sử ta chỉ có 1 Cluster vật lý, nhưng lại có 2 môi trường Dev và Prodcution, thì ta có thể tạo ra 2 namespace để phân biệt 2 môi trường với nhau.

Có thể xem những namespace với câu lệnh `kubectl get namespace`

Lưu ý, có những đối tượng `nằm trong namespace` ví dụ như mạng ảo; nhưng lại có những đối tượng `không nằm trong namespace` ví dụ như storage.

#### Label & Selector

Label là một cặp `key-value` để quản lý đối tượng dễ hơn, cụ thể hơn so với `namespace`. Thêm nữa, người dùng có thể tự tạo label một cách tuỳ ý. Ví dụ:
- "release" : "stable", "release" : "canary"
- "environment" : "dev", "environment" : "qa", "environment" : "production"
- "tier" : "frontend", "tier" : "backend", "tier" : "cache"
- "partition" : "customerA", "partition" : "customerB"
- "track" : "daily", "track" : "weekly"

Có thể sử dụng Selector hay NodeSelector để chỉ định Pod sẽ được chạy trên một node nào đó phù hợp.

#### Annotaion

Giống với Label, nhưng Annotation hướng đến những metadata lớn hơn và tự động so với Label. Ví dụ:
- Thông tin về timestamps, release IDs, git branch, PR numbers, image hashes, và registry address :shrug:
- Các endpoint về nhật kí, giám sát hoặc cảnh báo.
- Các thông tin về phiên bản thư viện 3rd party.
- Vân vân, ...

# Kết luận

Bài blog này đã giới thiệu qua một số thuật ngữ trong Kubernetes cũng như một vài use case khi nào nên sử dụng Kubernetes. Bài blog tiếp theo trong chuỗi series có thể sẽ nói về các ý tưởng về Container hay Workload, những real case scenario khi triển khai một công việc DevOps.
#GLHF

[1]: {{ site.baseurl }}/assets/img/2021/04/container_evolution.svg "Container Evolution"
[2]: {{ site.baseurl }}/assets/img/2021/04/components-of-kubernetes.svg "Components of Kubernetes"
