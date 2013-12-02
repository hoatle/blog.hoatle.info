---
layout: post
title: "giới thiệu cái music-engine nào"
author: hoatle
date: 2008-12-16 12:13
comments: true
categories:
    - "vi"
tags:
    -
cover:
description:
keywords:
published: true
---

Cũng suy nghĩ khá nhiều để viết 1 cái ứng dụng OpenSocial và cuối cùng tớ đi đến quyết định viết cái ứng dụng music-engine này.

<!-- more -->

Music-engine nghĩa là thế nào? Music-engine của tớ sẽ đi tìm càng nhiều thông tin về các ca khúc càng tốt (tên, ca sĩ, nhạc sĩ, link nhạc...) và sắp xếp lại vào cơ sở dữ liệu trên Google Apps.

Music-engine sẽ cung cấp dịch vụ cho các ứng dụng OpenSocial của tớ. Người dùng có thể tìm kiếm, nghe, download, tạo và lưu playlist ưa thích. Ngoài ra, với tính năng của mạng xã hội, người dùng còn có thể gửi tặng ca khúc, playlist yêu thích cho bạn bè.

Mỗi người dùng sẽ có riêng 1 kênh (có thể tự động) cập nhật những bài hát họ đang nghe. Giống như Twitter trả lời câu hỏi "bạn đang làm gì?" thì với Music-Engine thì bạn sẽ trả lời câu hỏi "Bạn đang nghe gì?"

Vẫn còn một số tính năng quan trọng nữa nhưng có lẽ để sau, phải hoàn thành sớm sớm còn đăng kí SE Asia Contest chứ ;))

Về vấn đề bản quyền? Music-engine sẽ chỉ tìm và lưu trữ thông tin chứ không lưu nhạc trên server (có muốn cũng chả được). Một số trang tìm kiếm có kiểu cache, tức là lưu file nhạc về máy chủ của mình. Việc này có phải là sao chép bất hợp pháp? Còn đối với Music-Engine, mọi hoạt động của người dùng như tìm kiếm, download hay các hoạt động khác thì đều từ phía người dùng, Music-Engine không có bất kì mối liên hệ nào cả :D.

Chỉ là một số ý tưởng để chia sẻ. Tớ đã hoàn thành cơ bản xong mô hình cơ sở dữ liệu cũng như thử nghiệm crawl xong 1 trang nhạc.

Vì Google Apps hiện tại chỉ hỗ trợ Python, thế nên hầu như sẽ code bằng Python trên server.

Vì tớ làm việc với PHP khá lâu và cũng có kinh nghiệm viết một cái news crawler mấy tháng trước. Bây giờ sẽ cải thiện cho nó thành music-crawler, không phải là news nữa.

Bạn nào thích code cùng thì cứ liên hệ. Còn nhiều thứ phải làm quá, dù gì thì đây cũng là dự án làm cho vui :).
