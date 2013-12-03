---
layout: post
title: "Root role trong Nautilus"
author: hoatle
date: 2008-12-12 19:15
comments: true
categories:
    - "vi"
tags:
    - "Ubuntu"
cover:
description: Root role trong Nautilus
keywords:
published: true
---

Khi sử dụng Ubuntu, quyền mặc định sẽ là người dùng bình thường, không phải là quyền "root".
(Với quyền "root" thì có thể làm mọi thao tác đến hệ thống).

Trong terminal, các thao tác cần đến quyền root thì tất cả các lệnh đều phải có "sudo"
[superuser do == root] ở trước.

<!-- more -->

Ví dụ: `computername: directory$ sudo mv file_path dir_path` [Di chuyển 1 file sang một thư mục mới,
thường dùng sudo khi làm việc với file hệ thống không nằm trong home dir].

Nhưng dùng lệnh copy, move trong terminal chỉ copy và move các file chứ không thể copy hoặc move
thư mục.

Vừa download FileZilla về, giải nén ra ở Desktop thì được 2 thư mục con là bin và share. Có thể sử
dụng luôn khi click vào filezilla trong bin, nhưng tớ muốn copy vào thư mục cài đặt thông thường
là `/usr` [Trong `/user` có 2 folder là `bin` và `share`]. Có thể copy vào `/usr/local` [Cũng có 2
folder là `bin` và `share`]. Có thể phải mất một thời gian mới quen được cách sắp xếp file trong
Linux, khác nhiều so với Windows. Mới đầu dùng thì hơi bị loạn :D.

Vậy là tớ quyết định move 2 cái folder của FileZilla là `bin` và `share` sang `/usr`.

Dùng Nautilus [Giống Windows Explorer trong Windows] với quyền thông thường thì không thể copy,
delete, move trong File System. Mới đầu tớ dùng terminal để move file trong bin của FileZilla vào
folder bin trong /usr. Còn lại folder share lại có thêm mấy cái folder con nữa, trong mấy cái folder
con này lại có folder con nữa, nếu dùng terminal thì chắc chết :(.

Hoặc là có cách copy, move cả folder mà tớ chưa biết, chưa search được ???

Cách nhanh nhất là dùng Nautilus với quyền root. Vào terminal type: `sudo nautilus`. Thế là ổn. Giờ
copy, paste, delete thoải mái :D.
