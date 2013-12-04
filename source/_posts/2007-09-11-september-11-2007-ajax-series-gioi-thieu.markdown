---
layout: post
title: "September 11, 2007 - Ajax Series_Giới thiệu"
author: hoatle
date: 2013-12-04 20:19
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

Sau một thời gian ngâm cứu khá lâu (nhưng chưa kĩ lắm về Ajax, tự nhiên thấy hứng viết các entry về
chủ đề này. Tất nhiên những entry này sẽ tìm hiều Ajax từ đầu đến cuối (mình dựa vào sách để viết –
dịch). Chia sẻ cho những bạn nào không thích đọc bằng tiếng Anh. Dù sao mình vẫn thích đọc bản gốc,
các bạn nên đọc bản gốc mới thú, mới hiểu và nắm chắc vấn đề. Tuy nhiên trong quá trình dịch, chỗ
nào cần giải thích mình sẽ giải thích thêm luôn cho dễ hiểu. Cuốn “Professional Ajax” mình cho là
thâu tóm hơi bị đầy đủ các kỹ thuật Ajax. Khỏi dài dòng văn tự. Chúng ta bắt đầu nhé. Cuốn sách hơi
bị dài, khi nào rảnh rỗi có hứng mình lại viết tiếp. Các bạn có thể tìm cuốn sách này đọc, còn muốn
đọc tiếng Việt thì đọc cái này cũng hơi bị ổn. Mình viết entry này vì trên một số diễn đàn thấy
nhiều bạn thích tìm đọc tiếng Việt :> (Mỗi tội hơi lâu, đang học dịch ở trường mà -> có thời gian
ngồi type một lúc cho đỡ phí!).

<!-- more -->

**GIỚI THIỆU:**

Với những kỹ năng JavaScript nâng cao, các nhà phát triển web đã tạo ra những trải nghiệm mới cho
người duyệt web trong các ứng dụng của mình. Phá vỡ kiểu mẫu cổ điển “click-and-wait”
(“nhấn-và-đợi”) đã thống trị thế giới web ngay từ buổi sơ khai, giờ đây các nhà phát triển có thể
đem những tính năng chỉ có ở các ứng dụng desktop vào trang web bằng cách sử dụng kỹ thuật Ajax.

Ajax là một thuật ngữ chỉ việc sử dụng các yêu cầu HTTP bất đồng bộ (asynchoronous HTTP requests)
được khởi tạo bằng JavaScript để lấy được dữ liệu từ server mà không cần tải lại trang web. Các yêu
cầu này có thể được tạo ra và thực thi bằng rất nhiều cách và sử dụng rất nhiều định dạng truyền tải
dữ liệu khác nhau để truyền tới trình duyệt cho JavaScript xử lý. Việc kết hợp lấy dữ liệu từ xa và
tương tác với DOM (Document Object Model - mô hình đối tượng tài liệu) đã tạo ra một thế hệ các ứng
dụng web mới dường như không còn tuân theo các quy tắc truyền thống về những gì có thể diễn ra trên
web. Các công ty lớn như Google, Yahoo! và Microsoft… đã tạo ra và chia sẻ nhiều nguồn tài nguyên
đặc biệt hướng tới mục tiêu tạo các ứng dụng web chạy và trông giống như các ứng dụng trên desktop.

Các entry về Ajax này sẽ nói đến các khía cạnh của Ajax, bao gồm các cách khác nhau bạn có thể khởi
tạo các yêu cầu HTTP tới server “behind the scene” và các định dạng dữ liệu khác nhau để truyền cho
nhau giữa trình duyệt và server. Bạn sẽ học được các kỹ thuật và kiểu mẫu Ajax khác nhau để thực thi
giao tiếp client-server trên website hay các ứng dụng web của bạn. (máy khách: gửi yêu cầu tới máy
chủ – máy chủ: đáp lại yêu cầu của máy khách. Thực ra máy chủ phải gọi là máy phục vụ mới đúng –
nhưng mà toàn gọi là máy chủ thì cứ gọi vậy đi, đỡ gây nhầm lẫn; còn máy khách thì nên gọi là máy
người dùng thì dễ hiểu hơn :)

**AI NÊN ĐỌC CÁC ENTRY NÀY?**

Các entry này dành cho tất các các bạn quan tâm tới kỹ thuật này, các bạn phát triển các ứng dụng
web, các bạn có trình độ JavaScript trung cấp muốn hiểu nhiều hơn về ngôn ngữ này, nâng cao lên
trình độ pro :D. Àh, những bạn nào quen với các công nghệ: XML, XSLT, PHP, C#, HTML, CSS, các dịch
vụ web thì đừng bỏ qua các entry này nhé. Thật ra bạn chỉ cần biết HTML, CSS, JavaScript là có thể
sử dụng đến các kỹ thuật Ajax rồi.

**CÁC VẤN ĐỀ ĐƯỢC ĐỀ CẬP ĐẾN?**

Tất nhiên không gì khác ngoài việc giới thiệu, hướng dẫn các kỹ thuật, kiểu mẫu và các trường hợp
sử dụng Ajax.

Series entry này bắt đầu đi tìm hiểu nguồn gốc Ajax, sự phát triển của web, và các công nghệ mới
trực tiếp dẫn tới sự phát triển của các kỹ thuật Ajax. Chúng ta sẽ bàn chi tiết hơn về các frame,
JavaScript, cookies, XML, và XMLhttp liên quan như thế nào tới Ajax.

Sau phần giới thiệu này, chúng ta sẽ nói đến các kỹ thuật Ajax cụ thể. Các yêu cầu “behind the
scene” được tạo ra bằng cách sử dụng các frame ẩn (hidden), các iframe động (dynamic) (chú ý frame
và iframe sẽ được nói chi tiết sau); các cách sử dụng này sẽ được so sánh và đối chiếu, giải thích
khi nào thì nên sử dụng cách nào hơn cách nào. Để bàn luận kỹ và rõ ràng hơn, chúng ta sẽ xem xét
các yêu cầu HTTP (requests) và đáp trả HTTP (responses) được diễn ra như thế nào.

Một khi bạn đã có kiến thức cơ bản về các loại yêu cầu khác nhau, chúng ta sẽ đi sâu khám phá các
ví dụ khi nào và bằng cách nào sử dụng Ajax trong website và ứng dụng web. Các thuận lợi cũng như
bất lợi khi sử dụng các kiểu định dạng truyền dữ liệu khác nhau như: text thường (không theo định
dạng nào), HTML, XML, và JSON. Sau đó là bàn đến các dịch vụ web và làm sao sử dụng chúng để thể
hiện được các kỹ thuật Ajax.

Phần cuối cùng (chả biết có làm đến đây không nữa) sẽ hướng dẫn bạn làm một ứng dụng web Ajax đầy
đủ, hoàn thiện: AjaxMail sẽ kết hợp các kỹ thuật đã nói ở trên lại với nhau. Mình cũng sẽ giới thiệu
một số thư việc Ajax được thiết kế để việc giao tiếp Ajax dễ dàng hơn.

**CÁCH PHÂN CHIA AJAX SERIES?**

Để tiện việc theo dõi, series này sẽ được chia thành 10 phần. Mỗi phần sẽ được chia nhỏ tiếp theo
lượng từ mà phân bố. Các phần theo thứ tự sẽ là:

- Phần 1: “Ajax là gì? ” – giải thích nguồn gốc Ajax và các công nghệ liên quan. Mô tả quá trình
  phát triển của Ajax khi web phát triển, và ai (nếu có) có quyền sở hữu thuật ngữ và các kỹ thuật này.

- Phần 2: “Ajax cơ bản” – giới thiệu các cách khác nhau để thực hiện giao tiếp Ajax, bao gồm kỹ
  thuật frame ẩn, inframe động và XMLHttp. Các thuận lợi cũng như bất lợi đối với mỗi cách tiếp cận,
  và các hướng dẫn khi nào thì kỹ thuật nào được sử dụng.

- Phần 3: “Các kiểu mẫu Ajax” – tập trung vào các kiểu mẫu sử dụng Ajax. Có rất nhiều cách kết hợp
  Ajax vào website và các ứng dụng web. Tất cả sẽ được tổ thức thành kiểu mẫu thiết kế thuận tiện
  để kết hợp sử dụng Ajax thực tế.

- Phần 4: “XML, XPath, và XSLT” – giới thiệu XML, XPath, và XSLT là các công nghệ bổ sung Ajax. Tập
  trung vào cách sử dụng XML – định dạng truyền dữ liệu và XPath, XSLT để truy xuất và hiển thị thông
  tin.

- Phần 5: “Syndication với RSS/ ATom”. – sử dụng Ajax với các định dạng tập hợp dữ liệu RSS và ATom
  để tạo ra tập hợp tin tức trên nền web.

- Phần 6: “Các dịch vụ web” – Đem các dịch vụ web vào bức tranh Ajax. Các ví dụ giải thích cách gọi
  các dịch vụ web từ máy khách (máy người dùng) cũng như làm sao tạo các proxy bên server để làm
  việc với các hạn chế truy cập dưới chính sách bảo mật của trình duyệt.

- Phần 7: “JSON” - Giới thiệu JSON (JavaScript Object Notation – Chú giải đối tượng JavaScript).
  Nghe dịch như vậy cũng hơi khó hiểu, đây là cách biểu diễn đối tượng JavaScript theo cách khác
  ngắn gọn hơn, dễ dàng sử dụng hơn. JSON có thể được sử dụng để thay thế cho các giao tiếp Ajax.
  Chúng ta cũng bàn đến những thuân lợi cũng như bất lợi khi sử dụng XML và text thông thường.

- Phần 8: “Website Widgets” – Tập hợp các kỹ thuật từ các phần trước tập trung tạo ra các Ajax
  Widget có thể chèn vào website của bạn.

- Phần 9: “AjaxMail” – Hướng dẫn bạn hoàn thành một ứng dụng web – AjaxMail. Đúng như tên gọi của
  nó, đây là một hệ thống email trên nền Ajax. Tất nhiên ứng dụng này sử dụng rất nhiều kỹ thuật
  Ajax khác nhau được nói đến ở các phần trước. Đến phần này chắc là mình cũng có thể làm xong một
  cái ứng dụng dễ hiểu hơn, khi đó có thể mình thay bằng ứng dụng mình viết (dự định thôi!)

- Phần 10: “Ajax Frameworks” – Nói đến 3 Ajax Framework: JPSPAN cho PHP, DWR cho Java và JSP,
  Ajax.NET cho .NET framework.


Bình luận
---------

- \[broken] (2007-9-11 11:38:00):

*Nói đến các framework cho ajax thì trên kia mới chỉ là FW cho phía server thôi :D Những framework
cho phía client hỗ trợ lập trình JS cũng rất quan trọng và đem lại những cảm giác khác biệt rõ rệt
nhất cho người sử dụng :D Đó là EXT, ầu yé, và nhiều nữa, YUI, mootools, prototype ...*

*Aniwei, cuốn này có vẻ rất hay :D Nhất là việc dành nguyên 1 chương cho JSON :D*

- hoatle (2007-9-11 11:49:00):

*Ừh, Những FW cho client rất quan trọng vì ứng dụng web là hướng tới người dùng cơ mà :D. Đọc xong
mấy chương đầu thấy thích là viết entry ngay, các kỹ thuật trong sách nêu ra cũng hay, dễ hiểu.
Càng về sau mới khó :<*

- \[broken] (2007-9-11 11:49:00):

*tiếp tục dịch đi ^ ^ hay tôi cả ông dịch xen ké chương cho nhanh \:D/*

- hoatle (2007-9-11 11:53:00):

*uh, vậy ông dịch chương chẵn, tôi chương lẻ nhé. Dịch vậy cho nhanh, có gì hỏi nhau cũng dễ.*

- \[broken] (2007-9-12 12:09:00):

*vấn đề là chương ông đã dịch mới chỉ là introduction. Giờ tôi sẽ dịch chương 1:'What is ajax?',
dành cho ông chương kĩ thuật cơ bản để nghiên cứu nhá :D*

- hoatle (2007-9-12 12:37:00):

*Okie, thế cũng được.*
