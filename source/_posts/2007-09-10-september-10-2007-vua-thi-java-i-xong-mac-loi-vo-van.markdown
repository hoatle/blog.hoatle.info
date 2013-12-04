---
layout: post
title: "September 10, 2007 - Vừa thi Java I xong, mắc lỗi vớ vẩn!"
author: hoatle
date: 2007-09-10 09:27
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

Tuần này thứ 2 (hôm nay) thi lý thuyết và thứ 5 thi thực hành Java I. Làm bài cũng không có gì khó
lắm, nhưng ít nhất cũng bị mắc 2 lỗi rất vớ vẩn. Lúc làm bài 2 câu này chọn nhanh lắm, có nghĩ gì
đâu. Coi thường nó quá, đến khi xem lại lần 2 cũng xem qua (tự tin quá mà). 2 lỗi này đều về kiểu
dữ liệu: hỏi kiểu int có mấy byte? (Mình chọn 2 byte nhưng thực ra là 4 byte -> Nhầm lung tung, cái
này đáng lẽ không thể quên vậy mà…? ) Và giá trị nhỏ nhất của char? (Mình chọn -128 mà cái này lại
là giá trị nhỏ nhất của byte.) Thật ra là 0 mới phải, câu này cũng hơi khó, mình biết nhưng mỗi tội
không thèm nghĩ (hừm). Kiểu char có giá trị từ \u0000 tới \uFFFF (thập lục phân). Đấy là 2 lỗi mà
sau khi finish xong ra ngoài mới giật mình, về nhà kiểm tra lại thì đúng là sai. Còn lại 19 câu
không biết có sai câu nào nữa không. Sau mỗi lần sai thì để còn nhớ, chứ không sai thì không nhớ
được.

<!-- more -->

Tối thứ 5 thi thực hành tiếp. Thường mình không sợ thi lý thuyết, nhưng thực hành thì cũng hơi bị
ngại. Lý thuyết chỉ cần nhớ, còn thực hành cần tư duy và làm cái bài thực hành mới nhanh được. Mấy
bài cuối sách giờ mình vẫn chưa gõ code, chưa nắm vững được. Hôm ý mà thi cũng hơi lo, lúc rối lên
là hỏng tất. Cố thực hành mấy bài cuối thì đỡ run hơn. Căn bản mấy bài cuối đó trình bày dàn trải,
lộn xộn quá. Xem đến đấy là nản rồi, nhiều cái nghĩ cũng chả cần thiết. Hôm thứ 7 tuần trước C0610K
thi lại có bài về Date với lại Calender, mà trong sách có mỗi 2 ví dụ về 2 thằng này. Cứ tưởng chỉ
giới thiệu thôi.

Hôm nay thi lý thuyết được về sớm, cố gắng xem lại mấy bài cuối sách rồi còn xử lý tiếng Việt select
từ database ra nữa. Làm bằng PHP với MSSQL, cái câu lệnh với database hơi khác, không hiểu sao vẫn
chưa lấy được tiếng Việt, có phải có codepage như asp không nữa? Tức quá, select mãi không xong
tiếng Việt thì làm xong làm xong được. Mà cuối tuần này người ta đã đòi hoàn chỉnh hòm hòm rồi, hôm
nay mà chưa xử lý xong tiếng Việt thì cũng hơi lo.
