---
layout: post
title: "Khôi phục Folder Options, Task Manager, và Regedit"
author: hoatle
date: 2007-05-09 01:17
comments: true
categories:
    - "vi"
tags:
    - "360.yahoo.com"
cover:
description:
keywords:
published: true
---

Máy mình bị nhiễm virus từ lần chưa nối mạng và khổ sở vì nó (đọc Oh my lover để biết thêm chi tiết
). Sau khi update phần mềm diệt virus BitDefender thì không còn Folder Options, Task Manager
(Ctrl+Alt+Del), cả Regedit nữa. Hôm nay vừa đọc xong bài viết trên 24H post bài cho ai bị thì làm
theo hướng dẫn này khôi phục nhé.

<!-- more -->

Khi máy tính bị nhiễm một số loại virus hoặc thậm chí sau khi đã diệt sạch virus, bạn không tìm thấy
hàng chữ Folder Options trong menu Tools cũng như hàng chữ Task Manager bị mờ đi trong menu hiện ra
khi bấm chuột phải lên thanh taskbar, đồng thời bấm Start -> Run, gõ regedit thì không chạy được.
Để có lại ba thành phần này, bạn thực hiện các cách sau:

**Khôi phục Folder Options:**

Bạn bấm Start -> Run, gõ gpedit.msc rồi bấm Enter. Ở cửa sổ Group Policy hiện ra, trong khung bên
trái, lần lượt bấm dấu cộng (+) trước các hàng chữ: User Configuration; Administrative Templates;
Windows Components; bấm chuột lên hàng chữ Windows Explorer; bấm đúp chuột lên hàng chữ Remove the
Folder Options menu item from the Tools menu, bấm chọn Disable ở cửa sổ hiện ra và bấm OK.

Nếu vẫn chưa thấy Folder Options xuất hiện trong menu Tools, bạn thực hiện lại 2 lần thao tác trên:
Chọn Enable ở lần thứ nhất và Disable ở lần thứ hai.

**Khôi phục Task Manager:**

Trong khung bên trái của cửa sổ Group Policy nói trên, bạn cũng lần lượt bấm dấu cộng (+) trước các
hàng chữ: User Configuration, Administrative Templates, System, Ctrl+Alt+Del Options. Bấm đúp chuột
lên hàng chữ Remove Task Manager trong khung bên trái, bấm chọn Disable ở cửa sổ hiện ra, bấm OK.

Nếu Task Manager vẫn bị mờ hoặc thấy cửa sổ Windows Task Manager chỉ chớp lên khi bấm tổ hợp 3 phím
Ctrl + Alt + Del, bạn thực hiện lại thao tác trên với lựa chọn Enable và Disable như ở phần Folder
Options.

**Khôi phục lệnh Regedit**

Trong cửa sổ Group Policy, bạn lần lượt bấm dấu cộng (+) trước các hàng chữ: User Configuration,
Administrative Templates, System. Bấm đúp chuột lên hàng chữ Prevent access to registry editing
tools trong khung bên trái, bấm chọn Disable ở cửa sổ hiện ra, bấm OK. Có thể bạn cũng sẽ phải thực
hiện lại như khi khôi phục Folder Options, Task Manager để chạy được lệnh này.

Sau khi khôi phục 3 thành phần trên, bạn khởi động lại máy tính. Nếu chúng tiếp tục bị mất là máy
tính của bạn vẫn còn bị nhiễm virus. Do vậy, bạn tiếp tục cập nhật chương trình diệt virus đang dùng
hoặc cài chương trình diệt virus khác để quét toàn bộ đĩa cứng và đĩa flash USB.
