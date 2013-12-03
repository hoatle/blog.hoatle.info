---
layout: post
title: "July 02, 2007 - Được xả hơi, sướng!!"
author: hoatle
date: 2007-07-02 12:14
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

Vừa từ quê lên, được nghỉ xả hơi một ngày thui cũng sướng đã đời, ở nhà nằm xem TV và giảng giải cho
đứa em mình những câu thắc mắc chẳng hỏi được ai. Chuyện, những dịp như thế này nó phải tận dụng là
phải rùi. 2 tuần mình với về nhà một lần cơ mà, mà về từ tối hôm thứ 7 thì chiều chủ nhật lại ra
đây. Mà công nhận giờ mình nhiều việc ghê, sướng!!. Mình chỉ sợ không có việc mà làm thui, nhưng chả
bao giờ có chuyện hết việc cả, chỉ khi nào mình không thích làm nữa thì mới hết việc. he..he. Được
làm những công việc mình thích thật thú vị, nó cứ tạo cho mình một niềm đam mê khó tả. Cứ làm được
cái này rồi thì mình lại muốn phải hoàn hảo nó, cải tiến nó và phát triển nó không ngừng.

<!-- more -->

Nó ở đây không phải là cái gì to tát cả, chỉ là những đoạn chương trình, những thuật toán theo đuổi
mình thui. Đừng nghe thấy thuật toán mà bảo chả hiểu gì, từ ngữ chuyên môn :P. Thật ra thuật toán
rất đơn giản, nó một tập hợp các bước, quá trình để đi đến cái mình cần có. Ví dụ một thuật toán cưa
cẩm nhé. Thuật toán này phải nói là cực kì thú vị, phức tạp và gian nan. Mình chỉ đưa ra một thuật
toán rất đơn giản để bạn hỉu về cái này thui, nhé!!

Dữ liệu bài toán: bạn đang đi trên đường có thấy một cô gái trông “dễ xương” -> có ý định muốn làm
wen với mục đích vô cùng “trong sáng” he he.

Bắt đầu:

- Đến làm wen:

    + Không cho làm wen -> Cố mà làm wen, khiến người ta lưỡng lự. Còn ko thì ráng chịu, thất bại
      lun, hic. Tốt nhất là đi tìm iem khác nhé, good luck. Khi tìm được lại bắt đầu thuật toán này.

    + Lưỡng lự -> Bắt chuyện đến khi chịu gật đầu làm wen mới thui.

    + Gật đầu làm wen: Thế là xong bước làm wen rùi nhé, chuyển sang bước tiếp theo.

- Chinh phục:
    + Tặng hoa, nói lời ngon ngọt (không hề dụ dỗ ke ke)

    + Rủ đi chơi, nói những câu lãng mạn, mủi lòng

    + Làm cho người ta vui, giận hờn (vu vơ) -> Cứ tiếp tục như vậy cho đến khi điểm cộng dành cho
      bạn lên vùn vụt. Đến khi đạt đến độ iu rùi sang bước típ.

- Tỏ tình:

    + Một màn tỏ tình lãng mạn, không cho người ta từ chối được.

    + Nếu từ chối quay lại bước trên nhé

    + Đồng ý -> còn gì mà ngần ngại nữa, chúc mừng nhé.!!

** Chú ý: trên chỉ là thuật toán vui vui, cấm trẻ em dưới tuổi mẫu giáo áp dụng, còn người lớn chắc
chả ai áp dụng cái này. Và từ thuật toán đơn giản như trên dựa vào các ngôn ngữ lập trình mà viết
chương trình cưa bạn gái. Để mình viết một chương trình bằng javascript theo thuật toán trên nhé.

```javascript
var answer, tryCount, lovePoints, response;

tryCount = 0; // Đếm xem số lần cố gắng ý mà, nếu quá 3 lần thì thui luôn

step1: answer = prompt("Cho tớ làm wen nhé?","đi mà :)"); // hỏi xem tình hình chiến sự ra sao (thăm dò ý mà)

if (answer == "no") { // Tức là câu trả lời của cô ấy đấy
  if(tryCount < 3) {
    tryCount = tryCount + 1 // hoặc tryCount++
    goto step1;
  } else {
    alert("Cô ấy thật sự không phải là người bạn cần. GoodLuck and Try another girl!");
    return false;
  }
} else if (answer == "ứ ừ") { // Đang lưỡng lự đấy
  while(answer != "ứ ừ") { // lặp cho đến khi nào không còn trả lời ứ ừ nữa thì thôi
    answer = prompt("Hãy trả lời thật cho tớ bít đi mà",""); // Nhớ tâm trạng chút
  }
  if(answer == "yes") {
    goto step2;
  } else {// Tức answer là "no” rùi đấy
    goto step1; // Bắt đầu lại từ Mo rùi
  }
} else if (answer == "yes") { // Còn chờ gì nữa mà không thẳng tiến
  goto step2;
}

// Bước chinh phục
step2: while (lovePoints < AskForLovePointTime) {
  /*Lặp đi lặp lại những việc trong ngoặc này tới khi đạt tới điểm tỏ tình thì thui */
  /* đây là hàm dụ dỗ, trả về số điểm tình cảm cho bạn; hàm này phức tạp,
     coi là vậy đi */
  lovePoints = tangHoa();
  lovePoints = lovePoints + noiLoiNgonNgot();
  lovePoints = lovePoints + ruDiChoi();
  lovePoints = lovePoints + lamNguoiTaVui();
  lovePoints = lovePoints + lamNguoiTaGianHonVuVo();
  lovePoints = lovePoints + lamLanh();
  lovePoints = lovePoints + chiemTinhCam();
  /* Đáng lẽ các hành động nàyphải ngẫu nhiên, nhưng thé này cho đỡ phức tạp wa */
}

step3: response = toTinhLangMan(); // To tinh rùi đấy, nếu đồng ý thì response = "yes"
if (response == "yes") {
  /* Những việc gì thì có trời mới bít ke ke (trong sáng tí đi, tớ không vít típ vì nó
     phức tạp và dài lắm */
  _%^##%@%_();
else {// Tức là response == "no" đấy
  goto step2;
}
```

Nhìn thí này chắc mấy bạn hơi bị nhức đầu, nhưng tớ lí tưởng hoá rùi đấy, đơn giản nhất rùi chứ thực
ra cái này mà hiệu quả thì jờ này tớ chả đơn côi một mình nghĩ ra cái trò này. Hum nay là ngày xả
hơi thứ hai của tớ mà. Tất cả những công việc còn lại để đến ngày mai. Jờ là thời gian chăm sóc
Blog, tớ vít cái Entry khác đây. Ở đây nó không cho thụt đầu dòng, làm cho đoạn trên nhìn lại đau cả
mắt. Nhớ là chương trình cưa cẩm trên chỉ là mô phỏng thui, chứ chắc chắc có (nhiều) lỗi lắm, đố
chạy đươc. Vít cho vui thui, cơ bản từ thuật toán tới chương trình nó là vậy.
