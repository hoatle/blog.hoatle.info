---
layout: post
title: "Tại sao cần kiểm thử phần mềm?"
author: hoatle
date: 2013-12-20 16:22
comments: true
categories:
    - "vi"
tags:
    - "kiểm thử phần mềm"
    - "software testing"
    - "QA"
cover: /images/2013/12/software-testing.jpg
description: Tại sao cần kiểm thử phần mềm?
keywords: tại sao, kiểm thử, chất lượng, phần mềm
published: true
---

{% img center /images/2013/12/software-testing.jpg Kiểm Thử Phần Mềm - Software Testing %}

Làm gì cũng cần kiểm tra, đánh giá thì mới biết được liệu nó có đạt được những gì được mong đợi, có
sai sót gì không. Tôi không hình dung được liệu trên thế giới này có gì không phải kiểm thử không?
Ngay cả quá trình phát triển của con người cũng trải qua hàng triệu năm được tự nhiên kiểm thử với
nhiều nhánh phát triển khác nhau. Có thể nói kiểm thử cũng có quy luật của nó, tôi gọi là "bảo toàn
kiểm thử".

<!-- more -->

"Bảo toàn kiểm thử" nghĩa là thế nào? Nếu bạn nắm định luật "bảo toàn năng lượng"[^1] thì bạn cứ
thay  "năng lượng" bằng "kiểm thử".

- Bạn dùng một thiết bị, đồ vật nào đó? Nó đã được kiểm thử trước khi đến tay bạn.

- Bạn chuẩn bị nâng cấp hệ điều hành cho chiếc điện thoại của mình? Các nhà phát triển đã kiểm thử
trước khi phân phối cho bạn. Ngay cả vậy thì bạn cũng vẫn muốn nghe ngóng những người khác sau khi
nâng cấp có bị vấn đề gì không trước khi quyết định nâng cấp nó? Những người dùng trước đó cũng thực
hiện công việc kiểm thử cho bạn.

Còn vô số ví dụ như vậy để biết rằng kiểm thử là một phần không thể thiếu trong cuộc sống, và trong
bài viết này tôi nói cụ thể về kiểm thử trong phần mềm.


Khi làm kiểm thử trong phần mềm, chúng ta thường dùng các công cụ để tự động hoá quá trình kiểm thử
này. Nếu không tự động hoá được thì bạn phải kiểm thử bằng tay. Vậy kiểm thử tự động hay bằng tay,
cái nào tốt hơn?

Trước khi có tự động thì phải làm bằng tay, tuy nhiên khi làm bằng tay lặp lại nhiều lần thì nên
(phải) tự động hoá nó để tối ưu hoá sức lao động của máy móc và giải phóng sức lao động của con
người. Như chúng ta đã biết, máy tính làm một tác vụ nào đó lặp đi lặp lại rất chính xác và nhanh
khi được lập trình, đấy chính là điểm mạnh duy nhất của máy tính để chúng ta tận dụng nó. Nhưng để
tự động nó cần phải học cách sử dụng công cụ, cần phải nắm vững công cụ mới làm được. Còn kiểm thử
bằng tay thì chi phí thấp hơn, nhanh hơn vào giai đoạn đầu. Qua quá trình làm việc, tôi thấy được
quy luật sau:

- Kiểm thử tự động có chi phí lớn trong giai đoạn đầu nhưng sẽ giảm dần theo thời gian.

- Kiểm thử bằng tay có chi phí thấp trong giai đoạn đầu nhưng sẽ tăng dần theo thời gian.

Vậy nên để trả lời câu hỏi kiểm thử tự động hay bằng tay chỉ cần xem xét quy luật trên. Nếu dự án
của bạn đủ dài, đủ lớn thì cần đầu tư nhiều cho tự động hoá kiểm thử.

Một lý do khác cần tự động hoá kiểm thử là khi các trường hợp cần kiểm thử tăng dần theo thời gian,
nếu bạn không kiểm thử được hết thì khi phần mềm được cập nhật rất dễ gây nhiều lỗi. Đây là một bài
học đắt giá mà tôi đã phải trả khi còn làm dự án eXo Social. Trong 3 năm tham gia dự án, bắt đầu năm
thứ 2 tôi đã tập trung nhiều vào tự động hoá kiểm thử, nâng dần tỉ lệ bao quát ("coverage"). Sau một
thời gian dài nỗ lực thì tỉ lệ hệ thống được kiểm thử từ 2-3% được nâng lên hơn 10%, trong đó các
thành phần chủ chốt ("core component") có tỉ lệ không dưới 70% (nếu tôi nhớ không nhầm), đó là cả sự
nỗ lực cố gắng không ngừng nghỉ của cả nhóm phát triển. Mặc dù vậy, tôi cũng đã mắc một sai lầm nghiêm
trọng khi để một bạn mới tham gia nhóm thay đổi nhiều code ở tầng có tỉ lệ kiểm thử thấp, sau đó phần
mềm đã có nhiễu lỗi cũ cũng như mới xảy ra. Tin tôi đi, đó là trải nghiệm không hề dễ chịu chút nào.

Sau bài học đó, tôi càng bị ám ảnh nhiều hơn với kiểm thử và quy trình kiểm thử. Nếu chúng ta có cơ
hội được làm việc với nhau, bạn sẽ thấy tôi có những yêu cầu rất khắt khe, có thể bạn cho là vô lý,
nhưng đó là từ những bài học, kinh nghiệm tôi đã đúc rút khi làm một dự án liên tục trong vòng hơn
3 năm với eXo Social và các dự án sau này.

Thật ra đến thời điểm này đầu tư cho tự động hoá kiểm thử phần mềm có chi phí không quá cao, học
công cụ cũng không khó, chỉ cần tìm hiểu một chút là bạn có thể làm được rồi. Tuy nhiên chi phí tổ
chức tự động hoá kiểm thử sao cho thật khoa học lại là cả một vấn đề lớn, nếu không có thể nó lại
đẩy thêm chi phí, gánh nặng cho phát triển phần mềm.

Kiểm thử có 4 cấp độ ("testing level") như sau:

- `unit testing`: kiểm thử từng đơn vị độc lập, riêng lẻ. Cụ thể trong phần mềm sẽ là các "method"
  hoặc "function". Bạn cần kiểm tra đầu vào và đầu ra của từng đơn vị độc lập ấy. Tôi xin nhấn mạnh
  "từng đơn vị độc lập, riêng lẻ" thêm một lần nữa.

- `integration testing`: kiểm thử các "module" hay "component" khi chúng tương tác với nhau.

- `system testing`: kiểm thử cả một hệ thống hoàn chỉnh khi toàn bộ các "module" hay "component"
  được tích hợp.

- `acceptance testing`: kiểm thử cả một hệ thống hoàn chỉnh từ A đến Z như được cài đặt cho người
  dùng cuối.

Càng ở cấp độ sau thì chi phí kiểm thử càng tốn kém hơn. Tuy nhiên, tự động hoá kiểm thử cho các cấp
độ này hoàn toàn làm được, và thực sự là tôi đang làm rồi. Càng tự động hoá được nhiều, thì về lâu
dài bạn sẽ tiết kiệm được rất nhiều chi phí. Chính vì thế mà "automation" là một trong những triết
lý phát triển của Teracy[^2] - startup chúng tôi đang dành tâm huyết gây dựng.


Hôm trước bạn của tôi có hỏi trên Facebook[^3]:

{% blockquote Vinh Quốc Nguyễn https://www.facebook.com/kureikain/posts/10152118115309113 %}

Nếu như unit test đã pass hết. thì tại sao mọi ng lại cần tới acceptance test, functional (or integrate) test nhỉ?

{% endblockquote %}

Và tôi có trả lời thế này:

{% blockquote %}

- mỗi cái test 1 kiểu mà, unit test là test đơn vị method, functional test là test vài method liên quan với nhau, integration test là test ở mức các module với nhau, acceptance test là test 1 hệ thống người dùng sử dụng được rồi. Theo ý mình hiểu nôm na là thế, nên không có sự chồng chéo giữa các test level đâu.

- ví dụ như test lắp ráp hệ thống xe máy đi, unit test là test từng bộ phận (bánh răng, ốc vít, ống xả...), test unit (từng cái 1) thì ok, rồi lắp 1 số bộ phận làm bánh xe, động cơ xe. Mình vẫn phải test bánh xe, động cơ xe (functional) chứ kể cả unit test ok rồi. Rồi lắp bánh xe, động cơ xe, khung xe lại thành xe hoàn chỉnh thì cần test là xe nổ máy, vào số thì bánh xe phải chạy, đồng hồ phải hiển thị km/h... (integration test). Rồi sau đấy đi thử thật trên đường (acceptance test). Như vậy bước nào cũng cần. Khi viết test cần phân biệt các level của test thì tránh được sự chồng chéo.

{% endblockquote %}


Nhiều người (ngay cả tôi) có thể nhầm "functional testing" là 1 cấp độ kiểm thử ("testing level"),
nhưng thực ra nó là một kiểu kiểm thử ("testing type"). Kent Beck [^4], tác giả của cuốn "Extreme
Programming", cũng có trả lời câu hỏi phân biệt giữa "unit testing", "functional testing" và
"integration testing"[^5].

Một số kiểu kiểm thử tôi có thể liệt kê ra ở đây:

- `smoke testing`

- `regression testing`

- `functional testing`

- `compatibility testing`

- `acceptance testing`

- `performance testing`

- `security testing`

- `destructive testing`

- `usability testing`

- `accessibility testing`

- `A/B testing`

- ...

Để tổ chức kiểm thử thì mỗi một kiểu kiểm thử bạn cần kiểm thử ở các cấp độ khác nhau. Sự giao thoa
của các kiểu và cấp độ kiểm thử sẽ cho ta bức tranh khá hoàn chỉnh về kiểm thử phần mềm. Bạn có thể
xem thêm thông tin cụ thể hơn ở phần xem thêm ở cuối bài viết.

Hy vọng bài viết có thể giúp bạn hiểu thêm về kiểm thử phần mềm. Tôi sẽ viết cụ thể về các công cụ
cũng như cách tổ chức, sắp sắp tự động hoá kiểm thử phần mềm thế nào trong các bài viết sau.

Chúc bạn vui khi tìm hiểu về kiểm thử và kiểm thử phần mềm!


Xem Thêm
--------

- http://en.wikipedia.org/wiki/Software_testing

Hình Ảnh
--------

- http://sanjeevanisolutions.net/SoftwareTesting.aspx

[^1]: http://vi.wikipedia.org/wiki/B%E1%BA%A3o_to%C3%A0n_n%C4%83ng_l%C6%B0%E1%BB%A3ng
[^2]: http://dev.teracy.org/docs/intro.html#about-teracy
[^3]: https://www.facebook.com/kureikain/posts/10152118115309113
[^4]: http://en.wikipedia.org/wiki/Kent_Beck
[^5]: http://www.quora.com/What-is-the-difference-between-unit-testing-functional-testing-and-integration-testing
