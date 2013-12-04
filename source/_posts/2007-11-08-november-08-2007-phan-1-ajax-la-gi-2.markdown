---
layout: post
title: "November 08, 2007 - Phần 1_Ajax là gì? (2)"
author: hoatle
date: 2007-11-08 03:14
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

[Xin ghi rõ nguồn [Hoat Le’s blog](http://360.yahoo.com/wild_tiger8607) khi muốn đăng lại các bài
viết trong **Ajax Series**]

Cần thời gian cho nhiều việc khác, chuyện gì đã qua sẽ qua không nói lại nữa. Chúng ta tiếp tục với
Ajax Series, lâu rồi chưa sờ đến nó, lại tiếp tục cùng mọi người “ngâm cứu” nào. Lần này sẽ là giọng
như viết sách, không thích kiểu “informal” nữa vì hơi “bát nháo” :(. Đêm nay chỉ type thôi.

<!-- more -->

Ở Entry trước chúng ta đã tìm hiểu một số thông tin cơ bản về Ajax, sự ra đời của Ajax. Tiếp tục
trong phần này sẽ giúp các bạn tìm hiểu sâu hơn nữa về Ajax – thuật ngữ rất “hot” từ năm 2005.

**1.3 Sự phát triển của Web**

Năm 1990, khi Tim Berners-Lee lần đầu tiên đưa bản dự thảo cho thế giới Web (World Wide Web) thì ý
tưởng của ông khá giản đơn: tạo ra một mạng thông tin được kết nối với nhau sử dụng siêu văn bản
(hypertext) và bộ định danh tài nguyên thống nhất (Uniform Resource Identifiers - URIs). Khả năng
liên kết các loại tài liệu khác nhau từ khắp nơi trên thế giới đã tạo ra tiềm năng rất lớn cho những
người đang tìm kiếm học bổng vì mọi người có thể dễ dàng truy xuất các tài liệu tham khảo gần như
ngay tức khắc. Hơn nữa, phiên bản đầu tiên của ngôn ngữ đánh dấu siêu văn bản (HyperText Markup
Language - HTML) có rất ít tính năng, chỉ để định dạng và liên kết các tài liệu, đó là một nền không
phải để xây dựng phần mềm giàu tính tương tác mà chỉ là nơi chia sẻ các loại tài liệu minh hoạ và
văn bản đã thống trị thế giới in ấn. Web đã phát triển từ những trang web tĩnh như vậy.

Khi Web phát triển, các nhà kinh doanh sớm nhận ra khả năng tiềm ẩn đưa thông tin về các sản phẩm và
dịch vụ của mình tới đông đảo mọi người trên mạng. Thế hệ tiếp theo của Web đã có nhiều khả năng
định dạng và hiển thị thông tin hơn vì HTML cũng đã phát triển để đáp ứng nhu cầu phù hợp với những
kì vọng của những người sử dụng biết đến kiểu truyền thông mới này. Nhưng một công ty nhỏ - Netscape
– ngay sau đó đã nhanh chóng đẩy tốc độ phát triển của Web nhanh hơn rất nhiều.

Note: Bắt đầu từ năm 1994 Netscape bắt đầu cuộc chiến giữa các trình duyệt (browser wars) khi đưa ra
hàng loạt các thẻ HTML mở rộng như hiển thị màu chữ, hiện ảnh.. trong trình duyệt của mình mà trong
các trình duyệt khác sẽ báo lỗi hoặc ra kết quả hiện thị không như mong muốn, hoặc không hiện gì cả.
Nhưng mọi người thích những mở rộng này và đều muốn sử dụng trình duyệt của Netscape để duyệt web.
Đến năm 1996, trình duyệt của Netscape đã trở thành chương trình máy tính phổ biến nhất thế giới. Có
thể nói đây là thời kì hoàng kim nhất của Netscape cho đến khi Microsoft cũng phát triển, cuốn hút
người dùng bằng cách thêm những phần mở rộng không phải là chuẩn vào trình duyệt của mình mà trình
duyệt khác không hiển thị hoặc báo lỗi. Bắt đầu từ đây cuộc chiến giữa 2 ông trùm trình duyệt bắt
đầu, nảy sinh rất nhiều vấn đề không tương thích cho các nhà phát triển. Đến những năm 2000,
Internet Explorer đã khẳng định vị trí số 1 của mình, trở thành trình duyệt phổ biến nhất đi cùng
hệ điều hành Windows. Đến năm 2004, trình duyệt mã nguồn mở Mozilla Firefox chính thức ra phiên bản
1.0. Đến năm 2005 sản phẩm mã nguồn mở từ bộ Mozilla Suite của Netscape đã được bình chọn là sản
phẩm số 1. Mozilla Firefox hoàn toàn miễn phí và ngày càng được ưa chuộng bởi các nhà phát triển,
người dùng. Và hiện nay Mozilla Firefox đã trở thành trình duyệt số 1 được sử dụng nhiều nhất trên
thế giới.

**1.4 JavaScript**

Netscape Navigator là trình duyệt web chủ đạo thành công trước nhất và cũng là trình duyệt đầu tiên
đẩy nhanh các công nghệ web. Tuy nhiên, Netscape thường bị chỉ trích bởi các tổ chức tiêu chuẩn vì
đã tiến hành áp dụng những công nghệ mới và các mở rộng cho các công nghệ hiện hành trước khi các
chuẩn được ban hành (rất giống Microsoft cũng bị chỉ trích vì đã không theo các chuẩn khi phát triển
Internet Explorer). Một trong những công nghệ được Netscape phát triển là JavaScript.

Đầu tiên được đặt tên là LiveScript, JavaScript đã được Brendan Eich của Netscape tạo ra và có trong
trình duyệt phiên bản 2.0 (1995). Đây là lần đầu tiên các nhà phát triển có thể tác động tới trang
web để tương tác với người dùng. Thay vì phải bắt server phải thực hiện nhiệm vụ đơn giản như kiểm
tra tính hợp lệ của dữ liệu, chúng ta có thể làm cho trình duyệt có thể kiểm tra tính hợp lệ của dữ
liệu ngay mà không cần gửi tới server. Khả năng này rất quan trọng tại thời điểm đó khi hầu hết
người dùng Internet sử dụng modem 28.8 Kbps, nếu gửi yêu cầu tới *server* thì sẽ trở thành game đợi
chờ (Có lúc người ta nói vui với nhau: WWW – World Wide Wait). Giảm thiểu số lần người dùng phải đợi
*response* từ *server* chính là bước lớn đầu tiên tiến tới cách tiếp cận Ajax.

**1.5 Frames (Khung)**

Phiên bản đầu tiên của HTML có mục đích tạo ra các tài liệu đứng độc lập một mình và đến tận HTML
4.0 *frame* mới được chính thức giới thiệu. Ý tưởng hiển thị một trang web từ một số tài liệu được
gộp lại là một ý tưởng cấp tiến đầy tranh luận đã được Netscape chọn để đưa vào tính năng cho trình
duyệt trước khi hoàn thành HTML 4.0. Netscape Navigator 2.0 là trình duyệt đầu tiên hỗ trợ các
*frame* và cả JavaScript. Đây là một bước tiến quan trọng trong sự phát triển của Ajax.

Vào cuối những năm 1990 khi cuộc chiến giữa các trình duyệt (browser wars) giữa Microsoft và
Netscape nổ ra thì cả JavaScript và frame đều được chính thức hoá. Khi ngày càng có nhiều tính năng
được hỗ trợ bởi 2 trình duyệt, các nhà phát triển sáng tạo bắt đầu thử nghiệm sử dụng cả 2 tính năng
này của trình duyệt. Do một frame đại diện cho một *request* hoàn toàn độc lập tới *server* nên khả
năng kiểm soát một *frame* và nội dung của nó bằng JavaScript đã mở cánh cửa cho một số khả năng lí
thú.

Trong bài viết tới sẽ đề cập tới một số kỹ thuật cơ bản sử dụng *frame* để gửi yêu cầu tới *server*
mà không cần *load* lại trang.
