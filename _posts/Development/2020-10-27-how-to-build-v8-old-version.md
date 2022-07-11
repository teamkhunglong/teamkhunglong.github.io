---
layout: post
title: "How to build v8 (but old version)"
date: 2020-10-27 18:00:00 +0700
category: development
author: minh
short-description: I want to build old version of v8, what now?
---

-----

# Why?

Một ngày đẹp trời nào đó, bạn muốn build bản cũ của v8 engine để làm theo mấy hướng dẫn exploit chẳng hạn. Nhưng khi làm theo [hướng dẫn](https://v8.dev/docs/build "Building V8 from source") thì lại thấy lỗi như thế này.

![][1]{:height=100% width=100%}

```
Error at //gni/v8.gni:193:3: Dependency not allowed.
  source_set(target_name){ ...
```

Đại khái là không hiểu lắm, nhưng mà nếu pull bản mới nhất về thì vẫn build được :( chs.

Những lỗi về compiling như vậy tìm trên Google khá là khó, và không được trả lời rõ ràng. Không chỉ có v8, mà khá nhiều dự án mã nguồn mở cũng như vậy, ví dụ như WebKit/JavascriptCore. Vậy giờ sao?

# What?

Về cơ bản, mỗi project của google đều được cập nhật qua `depot_tool/gclient` và đều được cập nhật cùng nhau. Nếu muốn build `chromium` từ source với `v8` từ source, version của `chromium` phải match với version `v8`.

`Gclient` ngoài việc pull code về qua mỗi bản cập nhật thì còn quản lý `submodule`. Version của các submodule không giống với build profile thì cũng không build được. 

# Solution

Lướt qua internet với từ khóa `Building old revisions`, mình tìm được bài [này](https://chromium.googlesource.com/chromium/src/+/master/docs/building_old_revisions.md). Vậy nên ở đây mình dịch ra tiếng Việt cho dễ đọc.

## Lấy phiên bản chuẩn của depot_tools

Giả sử trên source `v8` bạn đã checkout branch hoặc commit cần build rồi. Bạn cần chuyển `gclient` về thời điểm đó.

```
# Lấy thời điểm của phiên bản đã checkout:
~/v8/src $ COMMIT_DATE=$(git log -n 1 --pretty=format:%ci)

# Checkout phiên bản của depot_tools qua thời điểm đó:
~/depot_tools $ git checkout $(git rev-list -n 1 --before="$COMMIT_DATE" master)
~/depot_tools $ export DEPOT_TOOLS_UPDATE=0
```

## Dọn dẹp repo của v8

Do `gclient` hay commit mới có thể thêm một vài file khác, bạn cần clean repo của v8

```
~/v8/src $ git clean -ffd
```

## Cập nhật lại các gói phụ thuộc

Kiểm tra lại phiên bản của các `submodule` trùng khớp trên `gclient`

```
~/v8/src $ gclient sync -D --force --reset
```

## Build

Cuối cùng, bạn build lại như bình thường. Vậy là được!

[1]: {{ site.baseurl }}/assets/2020/10/v8_orig_build_bug.png#center