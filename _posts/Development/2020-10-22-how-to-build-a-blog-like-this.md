---
layout: post
title: "How to build a blog like this"
date: 2020-10-22 10:00:00 +0700
category: development
author: minh
tags: development github jekyll
short-description: Github Pages + Jekyll + Google Analytics
---

-----

# Làm sao để tạo được một blog như thế này?

## Động lực làm blog

Nếu bạn đã follow mình từ trước, có thể bạn đã biết mình có một chiếc blog ở domain [minhtt159.wordpress.com](https://minhtt159.wordpress.com "wordpress blog"). Trong quá trình sử dụng, mình đã gặp một vài vấn đề:
1. Wordpress cứ thỉnh thoảng lại gửi mail sale 20-30-50% nhằm dụ mình bỏ tiền ra, làm rác luồng mail.
2. Wordpress load rất chậm, dù không có post nào thì điểm [Google PageSpeed Insights](https://developers.google.com/speed/pagespeed/insights/) cũng chỉ được tầm 6x điểm.
3. Wordpress free theme khá xấu, lại còn không customize domain được, mà mình lại tốn 300k để mua domain này rồi, không dùng thì phí á!
4. Sau khi học tin học cơ sở 1 và được điểm B, do [website xấu](https://minhtt159.github.io "good old github page"), mình luôn muốn làm một chiếc website cá nhân đẹp đẹp một tí.

Dù như vậy, việc chuyển đổi qua chiếc blog như này có thể gặp phải nhiều khó khăn:
1. Toàn bộ source code của chiếc blog này sẽ được public tại trang github. Nếu website sử dụng theme hay animation gì đẹp đẹp, sẽ rất dễ được người khác bế đi như web của [Juno_okyo](https://j2team.dev/blog/canh-bao-extension-giao-dien-cu "anh gì ơi mở block cho em vào group h4x0r với :(").
2. Learning Curve khá lớn. Đối với người ít code web như mình, việc tạo ra một chiếc blog đẹp đẹp có đủ HTML/CSS/JS tốn khá nhiều công sức.

## Làm blog như thế này cần những gì?

### Domain

Đầu tiên, tất nhiên rồi, bạn phải có một domain.

![NameCheap Domain]({{ site.baseurl }}/assets/img/2020/10/name-cheap-domain.png#center "Name Cheap Domain")

Mình vô tình được quản lý một vài domain hay ho, vậy nên mình biết làm sao để mua một chiếc. Ở đây, mình sử dụng `NameCheap` vì thế giới hay dùng. Nếu tiếng anh là một trở ngại đối với bạn, ở Việt Nam có một vài dịch vụ cũng làm việc tương tự như `GoDaddy`, `Nhân Hòa`, `Hostinger`, ...

Với giá 13$/năm đối với domain `.com`, tính ra chưa đến 1k/ngày, mà mình lại có một chiếc blog riêng xịn sò như này thì tội gì không đầu tư một chút.

#### DNS Provider (Optional)

Mình không biết các trang web lớn họ trỏ DNS qua dịch vụ nào, nhưng ở đây, mình dùng `Cloudflare` vì nó free và có nhiều tiện ích. Ngoài ra, nghe nói một công ty lớn nào đó đang triển khai giải pháp tương tự, bạn có thể xem qua tại [Cloudrity](https://cloudrity.com.vn/ "yêu VCS <3").

![CloudFlare Analytics]({{ site.baseurl }}/assets/img/2020/10/cloudflare-analytics.png#center "CloudFlare Analytics"){:height="70%" width="70%"}

Khi config domain, bạn có thể tạo một [CNAME record](https://en.wikipedia.org/wiki/CNAME_record) để trỏ domain của bạn về trang github.

#### Mail Service (Optional)

Khi quản lý mail của `matesctf.org`, mình được tiếp cận với những hệ thống mã nguồn mở rất bá, trong đó có Zoho. Zoho cho phép bạn tạo một Email Hosting miến phí, điểm bất lợi là bạn chỉ có thể tạo số lượng user giới hạn (hình như là 5 users). Do đó, từ bây giờ bạn có thể gửi thư điện tử cho mình qua email [minhtt159@teamkhunglong.com](mailto:minhtt159@teamkhunglong.com).

### Github Pages

#### Domain của trang Github

Do mình chỉ cần làm website tĩnh (không kết nối database, không cung cấp dịch vụ, ...) nên mình sử dụng [Github Pages](https://pages.github.com/). Thay vì phải mua một chiếc VPS cấu hình cao và quản lý Webserver, mình có thể sử dụng công cụ miễn phí như của Github. Khó khăn mình đã nói ở trên, nhưng sự đánh đổi là hợp lý với trường hợp của mình.

Sử dụng Github Pages giúp mình yên tâm được một việc rằng tất cả nội dung trên blog đều là nội dung tĩnh, khỏi phải lo về vấn đề hacker tấn công vào Webserver (nói vậy thôi chứ mấy anh hacker đừng deface em nhé).

#### Blog Framework

Khi làm việc cùng những người anh, mình đã dần học hỏi được những công cụ tốt / framework tốt. Ví dụ như người anh có chiếc blog [Develbranch](https://develbranch.com) cũng sử dụng framework tương tự.

Tất nhiên, bạn có thể tự code HTML/CSS/JS như việc mình làm hồi học tin học cơ sở 1. Cơ mà, do mình gà, nên có framework thì mình dùng vậy.

Ở đây, mình dùng framework [Jekyll](https://jekyllrb.com/) với theme [Odin](https://github.com/TeaGuns/odin). Kho theme của Jekyll không xịn sò, không nhiều animation giống các trang lớn như [VCS](https://viettelcybersecurity.com) nhưng cũng đủ đẹp để mình được thỏa sức sáng tạo. Hơn nữa, những blog này mình viết hoàn toàn sử dụng markdown nên không phải lo khi đọc trên các phiên bản trình duyệt hay điện thoại khác.

#### Google Analytics

Làm web gì mà không chạy SEO? Thật ra, mình rất thích tính năng này của Wordpress. Nhờ có nó, mình biết được bài nào có nhiều lượng view hơn bài nào. Giả sử, đến thời gian này trong năm, mọi người hay search google ra những writeups cũ của mình ở những giải Sinh viên với An toàn thông tin những năm trước chẳng hạn.

Do không dùng Wordpress nữa, mình phải tự chạy Analytics cho blog. Mình nghĩ rằng không có công cụ nào khác tuyệt vời hơn [Google Analytics](https://www.google.com/analytics/). Sau khi tạo một chiếc data stream, họ gửi cho mình một đoạn byte để mình add vào [header của blog](https://github.com/teamkhunglong/teamkhunglong.github.io/commit/f73d61d37edc49743f069c1d1979d55481afe5e6). Việc còn lại là của Google lo thôi!

![Google Analytics]({{ site.baseurl }}/assets/img/2020/10/google-analytics.png#center){:height="70%" width="70%"}

### Logo

Nói chung là chiếc blog này không thể đẹp được nếu không có logo xịn sò :D

![Logo]({{ site.baseurl }}/assets/img/2020/10/teamkhunglong-demo.png#center)