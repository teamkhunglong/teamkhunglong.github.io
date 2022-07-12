---
layout: post
title: "How to mine with kubernetes"
date: 2021-09-06 09:00:00 +0700
category: operations
author: minh
short-description: ETH miner - Container Registry - Kubenetes
---

# Intro 

TL;DR: [ghcr-tictactoe](https://github.com/minhtt159/ghcr-tictactoe)

Ở post trước, mình có đề cập tới việc chạy miner sử dụng Kubernetes on cloud. Mình đã từng chạy thử và nó hoàn toàn có thể thực hiện được chỉ qua vài dòng code, nhiều khi còn miễn phí.

Tại post này, mình sẽ bày cho các bạn cách để tạo một workflow như vậy. Bài này gồm có các bước như sau:

1. [ETH Miner - GPU driver](#miner)
2. [Docker - Container Registry - Github](#cicd)
3. [Kubernetes on cloud](#kubernetes)

# Miner

Trước hết, ta sẽ cần biết cách sử dụng phần mềm đào coin. Có rất nhiều phần mềm dễ sử dụng với mức fee phải chăng như `Phoenix Miner` hay `T-rex Miner`. Những phần mềm này thường sẽ switch qua để đào cho author với mức fee là 1% với mỗi đồng mà bạn kiếm được. Do T-rex miner hỗ trợ Linux khá tốt, nên guide này sẽ tích hợp nói về T-rex.

Việc sử dụng T-rex đơn giản là đọc commandline options và điền vào các trường tương ứng ([link](https://github.com/trexminer/T-Rex))

# CICD

Mục đích cuối cùng của blog này là làm sao để scale khi bạn có nhiều tài nguyên. Khi ấy, mình sẽ nghĩ đến sử dụng Container.

Nhìn ở top-down level approach, mình sẽ tạo một `Deployment` trên `Kubernetes`, đặt `replica` với một số lượng nhất định các agent mà mình mong muốn.

Nhìn ở bottom-up level approach, mình cần tạo một `Docker image` và đẩy lên `Public container registry` (e.g. Dockerhub).

Nếu những thuật ngữ trên khó hiểu, thì có thể bạn không phải khán giả cho bài blog này.

Do đó, mình sử dụng Github, một nơi lý tưởng để làm việc này. Hơn nữa, nó miễn phí. Dù sao thì mình cũng cần một nơi để CI/CD, tiện có Github workflow, mình sẽ thử sử dụng nó xem sao.

## Step 1: Dockerfile

Tạo một Docker image trên máy dev để make sure là code chạy được trên môi trường production. Khi dev, có thể test bằng cách enable GPU cho container ([ref](https://docs.docker.com/compose/gpu-support/)).

Lưu ý:
- Trên môi trường thực tế, thành phần enable GPU engine cho container không phải là Docker.
- Do mình sẽ sử dụng lại tool của người khác, nên mình sẽ đụng vào ít thứ nhất có thể.

## Step 2: Github CI/CD

Tạo một Github repo, và setup CI/CD pipeline lên đó ([ref](https://docs.github.com/en/actions/guides/publishing-docker-images#publishing-images-to-github-packages)). Github thậm chí còn cho host free một container registry với dung lượng đến 500MB, quá đủ cho một mining container. 

Sau khi setup, Github sẽ tự build package cho bạn, và bạn có thể kéo container đó về chạy theo như mô tả trong package.

Lưu ý:
- Bạn có thể dự làm agent và đẩy lên một container registry khác, ví dụ như Gitlab & Dockerhub, thậm chí self-hosted-CR. Ở đây mình sử dụng Github để đơn giản hoá vấn đề.

# Kubernetes

Khi có được image trên `container registry`, bạn sẽ mang nó về deploy lên `kubernetes`. Có một vài vấn đề quan trọng cần lưu ý:

- Cài plugin vào node có GPU (ví dụ [k8s-device-plugin](https://github.com/NVIDIA/k8s-device-plugin))
- Đặt số lượng `replica` theo nhu cầu sử dụng, một vài `cloud provider` sử dụng `scaleset`, nên thậm chí bạn có thể đặt `replica` vô hạn nếu tài chính dư dả.
- Chọn `nodeSelector` để chỉ `schedule` miner vào những node có GPU.
- Nên đặt `hostAliases` cho các domain của miner, nếu không bạn sẽ gặp khó khăn khi giải trình với người quản lý DNS Server <(")

# Outro

Mình có up một chiếc demo public tại github của mình. Bạn hoàn toàn có thể fork ra rồi thay địa chỉ ví của bạn vào và dùng thôi. Dễ như úp mì tôm vậy. 

Link: [minhtt159/ghcr-tictactoe](https://github.com/minhtt159/ghcr-tictactoe)