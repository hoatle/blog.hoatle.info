---
layout: post
title: "Thêm đối số vào message bundle trong OpenSocial"
author: hoatle
date: 2010-01-16 21:18
comments: true
categories:
    - "vi"
tags:
    - "OpenSocial"
cover:
description: Thêm đối số vào message bundle trong OpenSocial
keywords: Thêm đối số vào message bundle trong OpenSocial
published: true
---

Bài toán
--------

- Khi làm việc với message bundle trong OpenSocial để dùng nhiều ngôn ngữ trong ứng dụng tùy thuộc
vào ngôn ngữ người dùng
([localization](http://wiki.opensocial.org/index.php?title=Localizing_OpenSocial_applications)) đôi
khi bạn cần phải thêm đối số động vào chuỗi hiển thị.

Ví dụ có chuỗi chào như này: Hello {user} trong đó user sẽ được thay bằng username tương ứng của
người dùng. Nhưng với OpenSocial api hiện tại thì không làm thế nào để thêm đối số vào được mà chỉ
có thể lấy được message tương ứng theo key cung cấp.

- Do vậy đây là cách làm của tớ: viết một thêm 1 class `eXo.social.Locale.getMsg(key)` và class này
cung cấp api cũng tương tự như với class `Prefs` để lấy `lang`, `country`, `msg` (class `Prefs` còn
cung cấp nhiều api khác nữa): prefs.getMsg(key). Class `eXo.social.Locale` cung cấp thêm phương thức
`eXo.social.Locale.getMsg(key, [val1, val2,...]);` để thêm đối số vào "message bundle".

<!-- more -->

Giải pháp
---------

- Viết class `eXo.social.Locale`:

```javascript
/**
 * Locale.js
 * Utility for Locale, dynamic binding message bundle with arguments
 * Usage:
 * eXo.social.Locale.getLang(); the same as prefs.getLang();
 * eXo.social.Locale.getCountry(); the same as prefs.getCountry();
 * eXo.social.Locale.getMsg(key); the same as prefs.getMsg(key);
 * eXo.social.Locale.getMsg(key, args); dynamic binding argument to message bundle
 * @author  hoatle
 * @since   October 27, 2009
 * @copyright   eXo Platform
 */

(function() {
    //prefs object to get lang, country, message bundle
    var prefs;

    /**
     * private function to lazily initialize prefs object
     */
    function getPrefs() {
        if (!prefs) {
            prefs = new gadgets.Prefs();
        }
        return prefs;
    }
    /**
     * Class definition
     */
    var Locale = function() {

    }
    /**
     * gets current lang
     * @static
     */
    Locale.getLang = function() {
        prefs = getPrefs();
        return prefs.getLang();
    }
    /**
     * gets current country
     * @static
     */
    Locale.getCountry = function() {
        prefs = getPrefs();
        return prefs.getCountry();
    }
    /**
     * alternative for prefs.getMsg(key)
     * uses to getMsg with provided key and substitute args
     *
     * eg: Test for {0}, {1}
     * If args does not match num of {\d}, warning and try to replace by corresponding index.
     * {0} should be replaced by args[0], etc.,
     * If args not provided, functions as prefs.getMsg(key)
     * @param   key String
     * @param   opt_args Array
     * @static
     */
    Locale.getMsg = function(key, opt_args) {
        prefs = getPrefs();
        if (!key) {
            debug.warn('key is null!');
            return '';
        }
        var msg = prefs.getMsg(key);
        if (msg === '') {
            debug.warn('Can not find resource bundle with key = ' + key);
            return msg;
        }
        if (!opt_args) return msg;

        //checks if number of {\d} in msg matches opt_args.length
        var regex = /{\d+}/g;
        var matches = msg.match(regex);
        if (matches.length !== opt_args.length) {
            debug.warn("required " + matches.length + " args, provided: " + opt_args.length);
        }
        //substitutes by index: {0} in msg should be replaced by opt_args[0] and so on
        for (var i = 0, l = matches.length; i < l; i++) {
            var index = matches[i].match(/\d+/g)[0];
            //TODO should improve performance
            var strToReplace = opt_args[index];
            if (!strToReplace) {
                debug.warn('matches[' + i + ']: ' + matches[i] + ' but no opt_args[' + index + ']');
            } else {
                msg = msg.replace(matches[i], opt_args[index]);
            }
        }
        return msg;
    }
    //Expose
    window.eXo = window.eXo || {};
    window.eXo.social = window.eXo.social || {};
    window.eXo.social.Locale = Locale;
})();
```

Trong class trên không có gì đáng nói ngoài cách dùng regular expression để thay thế chuỗi với
pattern là `{0}, {1}, {2}` và lấy các index trong `{}` để thay bằng `opt_args[index]` tương ứng.
Bạn có thể xem thêm vài viết của [@sanglt](http://twitter.com/sanglt):
[Sử dụng regular expression trong JavaScript](http://www.sanglt.com/content/su-dung-regular-expression-trong-javascript).

- Chú ý: Class `eXo.social.Locale` dùng debug được @cowboy viết, đây là cách debug/log tuyệt vời và
tớ rất thích. Giờ trong tất cả các dự án hay ứng dụng nào tớ cũng dùng, sau này nhìn vào console là
biết lỗi gì ở đâu ngay, chứ dùng alert thì đúng là cực hình. Các bạn cũng nên sử dụng cách debug/log
này :).

Download ứng dụng ví dụ đơn giản với cách thêm đối số vào "message bundle" tại
http://github.com/hoatle/opensocial/downloads

Mã nguồn tớ để ở đây: http://github.com/hoatle/opensocial/tree/master/message-bundle

Đây là file ứng dụng xml:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Module>
    <ModulePrefs title="Arguments Binding Message Bundle"
                 description="Simple-App for arguments binding with message bundle"
                 author_email="hoatlevan@gmail.com"
                 author_affiliation="eXo Platform">
        <Locale messages="locale/ALL_ALL.xml" />
        <Locale lang="en" messages="locale/en_ALL.xml" />
        <Locale lang="vi" messages="locale/vi_ALL.xml" />
        <Require feature="opensocial-0.8" />
    </ModulePrefs>
    <Content type="html">
    <![CDATA[
        <link rel="stylesheet" type="text/css" href="style/style.css" />
        <script type="text/javascript" src="script/debug.js"></script>
        <script type="text/javascript" src="script/eXo/social/Locale.js"></script>
        <script type="text/javascript" src="script/app.js"></script>
        <p>Resource bundle rendered by server: <strong>__MSG_hello_world__</strong></p>
        <p>Resource bundle rendered by JavaScript:</p>
        <div id="helloMsg"></div>
        <div id="helloMsgArgs"></div>
    ]]>
    </Content>
</Module>
```

Có thể thấy ở trên `__MSG_hello_world__` sẽ được thay thế bằng message bundle tương ứng với key là
"hello_world" (tớ để tất cả các file message bundle trong thư mục `locale`).

Để sử dụng class `eXo.social.Locale`, chúng ta có file app.js:

```javascript
function run() {
    var prefs = new gadgets.Prefs(),
        helloWorld = prefs.getMsg('hello_world');
    alert(helloWorld); //"Hello world!" if current language is English
                       //"Chào thế giới!" if current language is Vietnamese

    //eXo.social.Locale usage
    var Locale = eXo.social.Locale;
    var helloMsgEl = document.getElementById('helloMsg'),
        helloMsgArgsEl = document.getElementById('helloMsgArgs');

    helloMsgEl.innerHTML = Locale.getMsg('hello_world');
    helloMsgArgsEl.innerHTML = Locale.getMsg('hello_user_to_place', ['hoatle', 'Vietnam']);
}

gadgets.util.registerOnLoadHandler(run);
```

Bạn có thể chạy ứng dụng này ở bất kì OpenSocial container nào. Chúc bạn code vui :D.

Lưu ý: Có thể sử dụng OpenSocial templates để thêm đối số vào message bundle nhưng hiện nay hầu hết
các container chưa hỗ trợ hết.
