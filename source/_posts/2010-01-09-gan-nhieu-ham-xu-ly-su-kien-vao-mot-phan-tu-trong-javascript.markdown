---
layout: post
title: "Gán nhiều hàm xử lý sự kiện vào một phần tử trong JavaScript"
author: hoatle
date: 2010-01-09 02:06
comments: true
categories:
    - "vi"
tags:
    - "JavaScript"
cover:
description: Gán nhiều hàm xử lý sự kiện vào một phần tử trong JavaScript
keywords: Gán nhiều hàm xử lý sự kiện vào một phần tử trong JavaScript
published: true
---

Chiều nay đang lơ tơ mơ vì vừa ngủ trưa xong (bình thường không ngủ trưa thì thôi chứ cứ ngủ trưa
xong là lơ tơ mơ, chỉ muốn ngủ hết chiều cho sướng :d) thì có bạn hỏi trên group phpvietnam như
thế này:

**"Em có một input có thuộc tính onclick="doSomeFunction();" bây giờ muốn thêm
một hàm nữa ví dụ như onclick="doSomeFunction(); doSomeFunction2();". Công
việc này có làm bằng Javascript được không ah? Em cám ơn mọi người."**

*Nguồn*: http://groups.google.com/group/phpvietnam/browse_thread/thread/c7a8688875a320c3

<!-- more -->

Trả lời bạn ý xong là hết cả buồn ngủ :P, tiện thể tối về viết lại kinh nghiệm cho cái blog đỡ
tủi thân :P. Khi xử lý sự kiện trong JavaScript có 4 mô hình đăng kí sự kiện được phát triển qua
thời gian. Tớ cũng nói thêm về cách sử dụng và xử lý ngữ cảnh (context) với từ khóa `this` trong các
hàm xử lý. Trong hàm xử lý phải làm sao đạt được 2 mục đích: truyền tham số vào hàm xử lý phải là
`event object` và từ khóa `this` trong hàm xử lý sự kiện đó phải là phần tử đã được đăng kí sự kiện.

**1. Inline Event Registration Model (Mô hình cổ xưa và quen thuộc nhất)**

Từ những ngày đầu khi có JavaScript và xử lý sự kiện thì chỉ có 1 cách duy nhất để gán hàm xử lý sự
kiện cho một phần tử và hiện nay nhiều người vẫn làm theo cách này. Đây là cách cổ xưa và nguyên
thủy nhất:

```html
<a href="#" onclick="doSomething();">link</a>
```

Mọi người đã quá quen với cách làm như trên, đặc biệt là từ khi viết những dòng code JavaScript đầu
tiên. Viết như vậy không có gì sai cả mà nó còn tiện, nhanh, dễ hiểu và ngày xưa đến nay người ta
vẫn làm thế đấy thôi :P. Tuy nhiên, khi JavaScript phát triển hơn thì cách tiếp cận khác đi chút vì
có nhiều vấn đề nảy sinh như: làm như trên không tách biệt cấu trúc (structure - html) và hành vi
(behavior - JavaScript), làm cho code rối tinh rối mù lên, nhất là khi bạn phải lấy dữ liệu AJAX về
rồi apply template vào thì rất mệt.

Ta có hàm xử lý sự kiện `doSomething` như sau:

```javascript
function doSomething(evt) {
  alert(arguments[0]); // arguments[0] the same as evt
  alert(this);
}
```

Với trường hợp này thì `evt` là `undefined` và `this` chính là `window object`. Giờ làm thế nào để
`evt` là `event object` và `this` là element thì làm theo cách sau:

```html
<a href="#" onclick="doSomething(event);">link</a>
```

Như này là đã truyền được `event` vào event handler rồi nhé. Theo tớ suy luận và thấy thì khi
element được `click` thì nó sẽ sinh ra sự kiện `onclick` như sau:

```javascript
//[Native Code]
onclick(event) {
  //event handler được gọi theo cách này
  doSomething(event);
}
```

Nhớ là phải để `event` là tham số của `doSomething(event)` chứ ko được dùng tên nào khác. Nếu dùng
tên `evt` chẳng hạn thì sẽ xảy ra `exeption` do:

```javascript
[Native Code]
onclick(event) {
  //Gọi event handler mà có đối số là evt
  doSomething(evt); //Xảy ra exception ở đây vì evt là undefined.
}
```

Đây là native code nên nó không cho `evt` là `undefined (null)` chứ trong các hàm bình thường thì
truyền tham số là `undefined (null)` thì không vấn đề gì, ko có exception gì hết :D.

Chú ý: đoạn code trên được test với chrome thì ko thấy lỗi mà vẫn chạy ầm ầm chứ IE, Firefox, Opera
đều xảy ra lỗi hết. Không biết nên chê hay khen bạn chrome đây :d.

Vậy là đến đây lấy được `event object` rồi, từ `event object` này lấy được rất nhiều thông tin khác
nhau như tên sự kiện, vị trí con trỏ chuột.v.v... (`evt.type`; `evt.charCode`...)

Giờ đến việc xử lý từ khóa `this` phải là element chứ không phải là `window object` làm như sau:

```html
<a href="#" onclick="doSomething.call(this, event)">link</a>
```

Khi đó trong Native Code sẽ là:

```javascript
onclick(event) {
  //this ở đây là element
  doSomething.call(this, event);
}
```

Trên chính là đoạn code hoàn chỉnh khi muốn lấy `this` và `event object`. Tớ nói kỹ ở đây thôi,
mấy đoạn sau sẽ không nói lại mấy cái này nữa.

**2. Traditional Event Registration Model**

Đây cũng là cách khá nhiều người làm khi bắt đầu muốn tách biệt giữa cấu trúc và hành vi trên trang
web. Trong code JavaScript sẽ đăng kí hàm xử lý sự kiện còn html thì chỉ là html mà thôi.

```html
<a href="#" id="mylink">link</a>
```

Sau đó trong JavaScript đợi dom load hết thì cho đoạn code sau được thực thi:

```javascript
var linkEl = document.getElementById('myLink');
linkEl.onclick = function() {
  doSomething();
}
```

Đây là cách truyền thống được dùng cũng không phải là ít và hiện nay nó tương thích trên tất cả các
trình duyệt lớn nên ko có gì đáng ngại cả :). Trong mô hình này thì `event object` sẽ được truyền
luôn vào hàm xử lý sự kiện, còn `this` trong hàm xử lý sự kiện cũng là element luôn :D.

Có thể làm thế này khi trong hàm `doSomething` muốn có `event object` và `this` là phần tử sinh ra
sự kiện.

```javascript
linkEl.onclick = function(evt) {
  doSomething.call(this,evt);
}
```

Trong trường hợp `doSomething` nhận thêm vài tham số thì nên viết như này:

```javascript
function doSomething(evt, param1, param2) {
//code implementation
}


linkEl.onclick = function(evt) {
  var param1, param2;
  doSomething.call(this, evt, param1, param2);
  // Giống với: doSomething.apply(this, [evt, param1, param2]);
}
```

Tiếp đến là mô hình thứ 3 và 4 trong xử lý sự kiện. W3C model và Microsoft (IE) model. Sau đó kết
hợp hai mô hình 3 và 4 này được giải pháp khá hoàn chỉnh và có thể sử dụng ngon lành đối với mọi
trình duyệt lớn :).

**3. W3C Event Registration Model**

Theo mô hình chuẩn của bạn W3C thì đây là cách đăng kí sự kiện cho một element, có thể đăng kí
cùng lúc nhiều hàm xử lý cho 1 element:

```javascript
element.addEventListener(eventType, listener, useCapture);
```

`eventType` ở đây có thể là: click, mouseover, mouseout.v.v...

`listener` chính là hàm xử lý sự kiện được thực thi khi có sự kiện `eventType` xảy ra.

`useCapture` bạn nên để là `false` để thống nhất với trình duyệt IE, cái này liên quan tới event
phase mà tớ sẽ nói sau vào một bài viết khác.

Giờ có thể sử dụng như sau:

```html
<a href="#" id="mylink">link</a>
```

```javascript
//javascript, chỉ chạy trên các trình duyệt Firefox, Opera, Chrome
// ko chạy được trên IE
var linkEl = document.getElementById('myLink');
linkEl.addEventListener('click', function() {
    alert(arguments[0]); //event object
    alert(this); //linkEl
}, false);
```

Rất may là `event object` lại được truyền và `this` trỏ luôn đến element nên có thể gọi
`doSomething` luôn:

```javascript
linkEl.addEventListener('click', function(evt) {
    doSomething.call(this, evt);
}, false);
```

Với cách này bạn có thể add bao nhiêu hàm xử lý sự kiện tùy ý, khi có 1 sự kiện xảy ra thì các hàm
xử lý sự kiện đã đăng kí sẽ được thực thi và theo W3C đưa ra thì các hàm này thực thi có thể không
theo thứ tự đăng kí và hiện tại bạn không thể gọi phương thức nào của element để kiểm tra xem sự
kiện nào đó có bao nhiêu hàm xử lý sự kiện đã được đăng kí.

Nhưng muốn bỏ một hàm xử lý đăng kí sự kiện thì làm thế nào? Có luôn:

```javascript
    element.removeEventListener(eventType, listener, useCapture);
```

Cái này rất hiếm khi dùng. Khi muốn `remove` được một `listener` nào thì `listener` đó phải có tên.
Cách `add` của tớ ở trên kia dùng `anonymouse function` thì không thể `remove` được. Muốn `remove`
được thì phải làm theo cách này:

```javascript
var myListener = function() {
  alert(arguments[0]);
  alert(this);
 //cho chạy một lần đầu rồi remove listener đi luôn
  this.removeEventListener('click', myListener, false);
}
linkEl.addEventListener('click', myListener, false);
```

Đấy là theo W3C, còn Microsoft lại làm theo cách khác.

**4. Microsoft Event Registration Model**

Bạn IE thì lại chơi kiểu khác, bạn ý không dùng `addEventListener` mà lại dùng:

```javascript
    element.attachEvent(onEventType, handler);
```

Ví dụ:

```javascript
var linkEl = document.getElementById('myLink');
//Chỉ chạy trên IE
linkEl.attachEvent('onclick', function() {
  alert(arguments[0]); //event object
  alert(this); //linkEl
})
```

Muốn remove một handler (listener) thì dùng `detachEvent` cũng làm tương tự giống mô hình W3C ở trên:

```javascript
var myListener = function(evt) {
  alert(evt);
  alert(this);
  this.detachEvent('onclick', myListener);
}
```

Chú ý vì IE không có 2 event phase là `capture` và `bubble` mà chỉ có `bubble` phase nên khi sử dụng
với mô hình của W3C thì luôn dùng `false` với `useCapture` cho an toàn, nếu hiểu kỹ sự khác biệt của
2 phase này và có mục đích thì mới nên dùng `true`.

**5. Cuối cùng là cách kết hợp mô hình W3C với M$ (IE) thì ta có thể thiết kế và sử api đơn giản như sau:**

```javascript
addEventListener(element, eventType, listener, useCapture);
removeEventListener(element, eventType, listener, useCapture);
```

Phải luôn giữ `event object` được truyền vào tham số của listener và từ khóa this trong listener
phải trỏ đến element. Code như sau:

```javascript
/**
 * Cross browser add event listener method. For 'evt' pass a string value with the leading "on" omitted
 * e.g. addEventListener(window,'load',myFunctionNameWithoutParenthesis,false);
 * @param    obj object to attach event
 * @param    evt event name: click, mouseover, focus, blur...
 * @param    func    function name
 * @param    useCapture    true or false; if false => use bubbling
 * @static
 * @see        http://phrogz.net/JS/AttachEvent_js.txt
 */
 function addEventListener(obj, evt, fnc, useCapture) {
    if (obj === null || evt === null || fnc ===  null || useCapture === null) {
       alert('all params are required for addEventListener');
        return;
    }
    if (!useCapture) useCapture = false;
    if (obj.addEventListener){
        obj.addEventListener(evt, fnc, useCapture);
    } else if (obj.attachEvent) {
        obj.attachEvent('on'+evt, function(evt) {
            fnc.call(obj, evt);
        });
    } else{
        myAttachEvent(obj, evt, fnc);
        obj['on'+evt] = function() { myFireEvent(obj,evt) };
    }
    //The following are for browsers like NS4 or IE5Mac which don't support either
    //attachEvent or addEventListener
    var myAttachEvent = function(obj, evt, fnc) {
        if (!obj.myEvents) obj.myEvents={};
        if (!obj.myEvents[evt]) obj.myEvents[evt]=[];
        var evts = obj.myEvents[evt];
        evts[evts.length] = fnc;
    }
    var myFireEvent = function(obj, evt) {
        if (!obj || !obj.myEvents || !obj.myEvents[evt]) return;
        var evts = obj.myEvents[evt];
        for (var i=0,len=evts.length;i<len;i++) evts[i]();
    }
}
/**
 * removes event listener.
 * @param    obj element
 * @param    evt event name, 'click', 'blur'. 'focus'...
 * @func    function name to be removed if found
 * @useCapture true or false; false -> bubbling event phase
 * @static
 * //TODO make sure method cross-browsered
 */
 function removeEventListener(obj, evt, func, useCapture) {
    if (obj.removeEventListener) {
        obj.removeEventListener(evt, func, useCapture);
    } else if (obj.detachEvent) {//IE
        obj.detachEvent('on'+evt, func);
    }
}
```

Khi đó cách sử dụng đơn giản như sau:

```javascript
  var linkEl = document.getElementById('myLink');
  addEventListener('click', function(evt) {
    doSomething.call(this, evt);
  }, false);
```

Hy vọng tớ sẽ sớm viết thêm về event phase sau, chúc bạn code vui :D.
