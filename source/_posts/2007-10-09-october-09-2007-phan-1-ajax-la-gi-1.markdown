---
layout: post
title: "October 09, 2007 - Phần 1_Ajax là gì? (1)"
author: hoatle
date: 2007-10-09 03:28
comments: true
categories:
    - "vi"
tags:
    - "360.yahoo.com"
    - "JavaScript"
cover:
description:
keywords:
published: true
---

He he, phần 2 của Ajax Series mình cũng được mấy trang rùi mà hình như ông vannessar bận quá hay sao
ý, bảo dịch phần 1 mà mãi chả thấy nói gì. Mà ông ý cũng bận lắm, không để thời gian, anh em chờ
đợi, tớ sẽ tiếp tục nhiệm vụ cao cả là hoàn thành xong cái Ajax Series này. Vì post liên tục nên
phải có thứ tự thì theo dõi mới dễ. Nhất định sau này sẽ biên tập thành cuốn ebook dùng cho ngon.
Để không khí thêm thân mật, giờ tớ dùng cách viết *informal* 1 chút để anh em nào đọc đỡ *sleepy*
nhá. Okie, giờ chúng ta đi vào tìm hiểu phần đầu tiên:

<!-- more -->


**PHẦN I – Ajax là gì?**

Vì thời gian có hạn, không giông dài đưa đẩy lung tung, tớ sẽ giúp anh em có cái nhìn toàn diện về
Ajax, thực ra nó không phải là cái gì cao siêu, huyền bí mà kinh khủng như ai nghĩ, nó chỉ là 1 cách
tiếp cận hơi mới thôi. (Nhưng mà nói thật lần đầu tớ được chiêm nghiệm, lấy được responseText đã là
niềm tự hào lắm rồi, sướng run lên ấy chứ!)

1.1 Tổng quan 1 tí :D

Ui, đọc mà thấy trúc trắc ghê ta. Ghi nguyên văn ra đây nhé.

*From 2001 to 2005, the World Wide Web went through a tremendous growth spurt in terms of the
technologies and methodologies being used to bring this once-static medium to life. Online brochures
and catalogs no longer dominated the Web as web applications began to emerge as a significant
portion of online destinations. Web applications differred from their web site ancestors in that
they provided an instant service to their users. Whether for business process management or personal
interests, developers were forced to create new interaction paradigms as users came to expect richer
functionality.*

Khoảng từ những năm 2001 tới 2005, thế giới web của chúng ta đã có sự chuyển mình rất lớn khi nhìn
lại các công nghệ và phương pháp đã từng được sử dụng để tạo ra môi trường web - còn tĩnh. Các sách
quảng cáo hay danh mục liệt kê trực tuyến không còn thống trị Web nữa vì các ứng dụng web bắt đầu
nổi lên và trở thành một phần quan trọng, có ý nghĩa rất lớn trong sự phát triển của thế giới web.
Giờ đây các ứng dụng web không còn giống với tổ tiên trước đây của mình nữa (hì, dù tổ tiên là thế
hệ đi trước có mấy năm, công nghệ thay đổi từng giờ, từng ngày mà :P), các web site tổ tiên trước
đây còn chậm chạm chứ chả phục vụ mọi nguời nhanh như bây giờ. Dù muốn quản lý quá trình kinh doanh
hay chỉ là giây phút nông nổi nhất thời, thì anh em – những nhà phát triển (oai thế) bắt buộc phải
tạo ra nhửng kiểu tương tác mới khi người dùng (những người truy cập web site của quý vị) ghé thăm
cần có nhiều chức năng hơn từ các web site.

(Đoạn trên là 1 ví dụ, có thể bạn nào đọc thấy chả giống TA trên viết gì cả thì cũng nói luôn, tớ
phải dùng cách viết *informal*, *comunicative* mà, bạn nào thắc mắc là thiếu ý mới lo :(. Giờ tớ
type liền mạch cho nhanh cái nhá.)

Được có thêm các công nghệ đã có lúc ít được sử dụng và biết đến (Ajax là 1 ví dụ) trong các trình
duyệt, thế giới web đã có một bước tiến dài, phá tan (*đập tan* cho nó mấu) kiểu web truyền thống –
cứ mỗi lần có dữ liệu mới hay có một phần mới của ứng dụng được truy cập thì lại phải tải lại toàn
trang (*full page loading*). Các công ty bắt đầu có những thử nghiệm để tải lại động các phần của
trang web, chỉ truyền tới máy người dùng 1 lượng dữ liệu rất nhỏ, kết quả trả lại nhanh hơn, tốt hơn
và tất nhiên làm cho người dùng có những trải nghiệm thú vị hơn.

Người đứng đầu trong sự chuyển dịch này chính là gã khổng lồ Google. Sau khi gã khổng lồ tìm kiếm
được đưa lên mạng, các thử nghiệm được tiến hành bởi các kỹ sư của Google bắt đầu nổi lên trên 1
site của mạng Google có tên là Google Labs. Rất nhiều các dự án của Google Labs như Google Suggest
và Google Maps không bao giờ tải hết trang mà liên tục được cập nhật. Sự đổi mới này bắt đầu mang
tới trình duyệt giao diện giống giao diện phần mềm trên desktop, đánh dấu bước đầu của thời đại phát
triển web mới, và thực sự nó đã làm được.

Rất rất nhiều các sản phẩm thương mại cũng như mã nguồn mở bắt đầu tiến bước sử dụng kiểu ứng dụng
web mới mẻ này. Những dự án này giải thích công nghệ họ đã dùng với nhiều thuật ngữ khác nhau như
*JavaScript remoting*, *web remote procedure call*, và *dynamic updating*. Tuy nhiên ngay sau đó có
1 thuật ngữ nổi hẳn lên.

1.2 Ajax được ra đời

Vào tháng 2/2005, Jesse James Garrets của Adaptive Path, LLC đã công bố một bài báo trực tuyến có
tựa đề “Ajax: A new approach to Web Application” – Ajax: Một hướng tiếp cận mới cho ứng dụng web.
Anh em nào muốn đọc thì xem ở đây: http://www.adaptivepath.com/ideas/essays/archives/000385.php
Trong bài viết này, Garrets đã giải thích vì sao lại đặt niềm tin vào các ứng dụng web sẽ xoá bỏ
khoảng cách giữa các ứng dụng web và các ứng dụng desktop truyền thống. (Trông vẫn còn trẻ nên tớ
mạn phép được gọi bằng anh). Anh đã kể ra các công nghệ mới và một số dự án của Google là những ví
dụ điển hình cho thấy các tương tác người dùng dựa trên nền desktop truyền thống giờ đã được sử dụng
như thế nào trên web. Sau đó là 2 câu thổi bùng lên cơn bão lửa của niềm thích thú, hứng khởi cũng
như những tranh cãi. (Đến đây hơi bị buồn ngủ roài, cố nốt mấy câu nữa đi ngủ là vừa…). 2 câu đó:
*Google Suggest and Google Maps are two examples of a new approach to web applications that we at
Adaptive Path have been calling Ajax. The name is shorthand for Asynchronous JavaScript + XML, and
it represents a fundamental shift in what’s possible on the Web*. Google Suggest và Google Maps là
2 ví dụ có hướng tiếp cận mới cho các ứng dụng web mà chúng tôi ở Adaptive Patch đã gọi đó là Ajax.
Tên này là viết tắt cho *Asynchronous JavaScript + XML*, và nó tiêu biểu cho bước chuyển căn bản
những gì có thể trên web.

Bắt đầu từ sau bài báo này, làn sóng các bài viết về Ajax, các ví dụ code, và các cuộc tranh luận
bắt đầu nổ ra trên web. Các nhà phát triển viết trên blog về nó (còn giờ tớ cũng đang viết trên blog
về nó :D), các tạp chí công nghệ viết về nó, và các công ty bắt đầu có những sản phẩm gắn với nó.
Nhưng để hiểu Ajax là kí gì, trước tiên anh em cần phải hiểu sự phát triển của một số công nghệ dẫn
đến sự phát triển của nó.

Đến đây thì buồn ngủ wá, thôi hẹn 1 dịp freetime khác rùi lại nói típ.

Àh, wen. Tuy đây không phải là bản quyền nhưng ai muốn đăng lại toàn bộ hay 1 phần bài viết này xin
hãy ghi rõ nguồn và đường link. Thanks!

