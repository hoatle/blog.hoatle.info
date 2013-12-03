---
layout: post
title: "Tạo giao diện tab đơn giản với CSS và jQuery"
author: hoatle
date: 2008-12-20 19:55
comments: true
categories:
    - "vi"
tags:
    -
cover:
description: Tạo giao diện tab đơn giản với CSS và jQuery
keywords:
published: true
---

Đang phải làm việc với layout + giao diện, được dịp xem lại một số web interface. Gói interface này
là những interface được sử dụng nhiều như Tab Interface, Header Interface... Tiện đây, tớ giới thiệu
làm một cái Tab Interface, có thể sử dụng lại được. Tab Interface này sử dụng HTML + CSS + JQuery.
Xem demo tại đây: http://labs.hoatle.net/resource/design/tab-interface/

<!-- more -->

Đoạn code HTML cho cái Tab Interface:

```html
<div id="tab-wrapper">
    <ul id="tab-menu">
        <li><a href="#" class="tab-menu-active">Tab 1</a></li>
        <li><a href="#">Tab 2</a></li>
        <li><a href="#">Tab 3</a></li>
    </ul>
    <div id="tab-content">
        <p>If one examines subpatriarchialist material theory, one is faced with a choice: either accept the presemioticist paradigm of reality or conclude that the task of the artist is deconstruction, given that reality is equal to art. It could be said that the subject is contextualised into a Batailleist 'powerful communication' that includes language as a totality. Marx uses the term 'precapitalist semiotic theory' to denote the bridge between narrativity and society.</p>
        <p>Any number of desituationisms concerning Sartreist absurdity may be discovered. In a sense, the textual paradigm of consensus states that reality has significance. Baudrillard uses the term 'surrealism' to denote the absurdity, and subsequent rubicon, of substructuralist class. It could be said that la Tournier[4] holds that the works of Pynchon are modernistic. The premise of the textual paradigm of consensus states that the significance of the observer is social comment. However, in Gravity's Rainbow, Pynchon examines textual materialism; in The Crying of Lot 49 he denies subcultural discourse.</p>
    </div>
</div>
```

Dùng CSS để style cho đoạn HTML trên:

```css
/**
 * $Id$
 * author: hoatle
 * website: hoatle.net
 * file: tab-interface.css
 * style for tab-interface
 */
#tab-wrapper {
    margin: 0 auto;
    border: 0.1em dotted red;
    padding: 1em 0 0;
}

#tab-menu {
    border-bottom: 0.1em solid #ababab;
    color: #000000;
    margin: 1em 0 0;
    padding: 0 0 0 1em;
}
#tab-menu li {
    display: inline;
    list-style-type: none;
    overflow: hidden;
}
#tab-menu li a {
}
#tab-menu a {
    color: #676767;
    background: #dcdcdc;
    font: bold;
    font-size: 1.4em;
    border: 0.1em solid #ababab;
    padding: 0.2em 0.5em 0;
    text-decoration: none;
}
#tab-menu a.tab-menu-active {
    background-color: #fefefe;
    border-bottom: 0.3em solid #ffffff;
    color: #3a3a3a;
}
#tab-menu a.tab-menu-hover {
    background-color: #f0f0f0;
}
/*
#tab-menu a:active {
    background-color: #ffffff;
    color: #3a3a3a;
    border-bottom: none;
}
#tab-menu a:hover {
    background-color: #f0f0f0;
}
*/
#tab-menu a:visited {
    color: #666666;
}
#tab-content {
    background-color: #ffffff;
    text-align: justify;
    padding: 1em;
    border: 0.1em  solid #ababab;
    border-top: 0.2em solid #ababab;
    z-index: 1;
}
```

Để ý có đoạn comment sau đây vì khi dùng JQuery thì đoạn event trên không cần thiết nữa (bị lặp
thì đúng hơn). Nếu không dùng đến JQuery thì uncomment đoạn này:

```css
#tab-menu a:active {
    background-color: #ffffff;
    color: #3a3a3a;
    border-bottom: none;
}
#tab-menu a:hover {
    background-color: #f0f0f0;
}
```

Cuối cùng là JavaScript cho sau đây, vì lâu lắm nên đoạn này bị bừa bộn + thể nào cũng có đoạn code
dở hơi?

```javascript
/**
 * $Id$
 * author: hoatle
 * website: hoatle.net
 * file: tab-interface.js
 * This js file will control the tab-interface behavior
 */

$(document).ready(function() {
    $('#tab-menu:first').css('padding-left', '0').append('<li><a href=#>Tab More</a></li>'); //On the fly :)
    var nav_height = $('#nav').css('height');
    //alert('nav_height: '+nav_height);
    var content_height = $('#content').css('height');
    //alert('content_height: '+content_height);
    var common_height =  nav_height > content_height? nav_height : content_height;
    //alert(common_height);
    $('#nav').css('height', common_height);
    $('#content').css('height', common_height);


    $('#main-nav ul li a')
        .click(function(event) {
            event.preventDefault();
            $('#main-nav ul li a').removeClass('main-nav-active')
            $(this)
            .removeClass('main-nav-hover')
            .addClass('main-nav-active');
            $('#tab-content').hide();
            $('#tab-menu li a').fadeOut('slow').fadeIn('slow');
            //$('#main-content').fadeOut('slow').fadeIn('slow');
            delay($('#tab-content'), 1500);
            $('#secondary-content').hide('slow');
        })
        .hover(
            function() {
                $(this).addClass('main-nav-hover');
            },
            function() {
                $(this).removeClass('main-nav-hover');
            }
        );
    $('#tab-menu li a')
        .click(function(event) {
            event.preventDefault();
            $('#tab-menu li a').removeClass('tab-menu-active');
            $(this).removeClass('tab-menu-hover');
            $(this).addClass('tab-menu-active');
            $('#tab-content').fadeOut('slow').fadeIn('slow');
        })
        .hover(
            function() {
                if(!$(this).hasClass('tab-menu-active')) {
                    $(this).addClass('tab-menu-hover');
                }
            },
            function() {
                $(this).removeClass('tab-menu-hover');
        });

});

function delay(obj, time) {
    window.setTimeout(function() {
        obj.fadeIn('slow');
    }, time);
}
```

Vậy là xong. Tạo 1 trang html rồi rồi include 2 file: tab-interface.css và tab-interface.js vào
phần header [Nhớ include cả file thư viện Jquery.js], phần body thì chứa đoạn code HTML đã nói ở
trên:

```html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>Simple Tab Interface - JQuery - hoatle.net</title>
    <link rel="stylesheet" type="text/css" href="tab-interface.css" media="screen" />
    <script type="text/javascript" src="jquery.js"></script>
    <script type="text/javascript" src="tab-interface.js"></script>
</head>

<body>
<div id="tab-wrapper">
    <ul id="tab-menu">
        <li><a href="#" class="tab-menu-active">Tab 1</a></li>
        <li><a href="#">Tab 2</a></li>
        <li><a href="#">Tab 3</a></li>
    </ul>
    <div id="tab-content">
        <p>If one examines subpatriarchialist material theory, one is faced with a choice: either accept the presemioticist paradigm of reality or conclude that the task of the artist is deconstruction, given that reality is equal to art. It could be said that the subject is contextualised into a Batailleist 'powerful communication' that includes language as a totality. Marx uses the term 'precapitalist semiotic theory' to denote the bridge between narrativity and society.</p>

        <p>Any number of desituationisms concerning Sartreist absurdity may be discovered. In a sense, the textual paradigm of consensus states that reality has significance. Baudrillard uses the term 'surrealism' to denote the absurdity, and subsequent rubicon, of substructuralist class. It could be said that la Tournier[4] holds that the works of Pynchon are modernistic. The premise of the textual paradigm of consensus states that the significance of the observer is social comment. However, in Gravity's Rainbow, Pynchon examines textual materialism; in The Crying of Lot 49 he denies subcultural discourse.</p>
    </div>
</div>
</body>
</html>
```

Tab Interface cơ bản là vậy. Có thể từ HTML structure như vậy làm cái Tab Interface dạng ngang
(giống như trong trang Home ở Twitter) chứ không dọc thế này. Mọi thứ đều được làm đơn giản, tớ
thích sự đơn giản :).
