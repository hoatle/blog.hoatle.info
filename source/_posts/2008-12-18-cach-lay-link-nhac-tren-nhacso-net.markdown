---
layout: post
title: "Cách lấy link nhạc trên nhacso.net"
author: hoatle
date: 2008-12-18 01:21
comments: true
categories:
    - "vi"
tags:
    -
cover:
description: Cách lấy link nhạc trên nhacso.net
keywords:
published: true
---

Có rất nhiều trang nhạc tương tự không cho download và đó lại càng là mục tiêu để mọi người tìm cách
down nhạc ở những trang này. Các file media ở NhacSo cũng không chất lượng. Ở đây tớ lấy môt trang
điển hình, còn nhiều trang khác cũng hầu như có kỹ thuật tương tự, chủ yếu là phải biết phân tích
cách ẩn đường dẫn tới file media hoặc xml. Hầu như bây giờ các trang dùng xml hoặc json để lấy dữ
liệu qua XHR (XML Http Request hay còn gọi là Ajax).

Các bước tiến hành:

<!-- more -->

**1. Phân tích cái Media Player trong phần HTML Code**

Có thể thấy trong phần code trên NhacSo có đoạn mã nhúng media:

```html
<object height="300" width="100%" viewastext="" type="application/x-oleobject"
standby="Loading Microsoft Windows Media Player components..."
codebase="http://activex.microsoft.com/activex/controls/mplayer/en/nsmp2inf.cab#Version=6,4,5,715"
classid="CLSID:22d6f312-b0f6-11d0-94ab-0080c74c7e95">
<param value="/Music/nghe_album.aspx?id=100039571" name="FileName"/>
<param value="false" name="TransparentAtStart"/>
<param value="true" name="AutoStart"/>
<param value="false" name="AnimationatStart"/>
<param value="false" name="ShowControls"/>
<param value="false" name="ShowDisplay"/>
<param value="999" name="playCount"/>
<param value="0" name="displaySize"/>
<param value="100" name="Volume"/>
<embed height="300" width="100%" displaysize="0" volume="100animationAtStart=0"
playcount="999" autostart="1" transparentatstart="0" name="MediaPlayer"
src="/Music/nghe_album.aspx?id=100039571"
pluginspage="http://www.microsoft.com/Windows/MediaPlayer/" type="application/x-mplayer2"/>
</object>
```

Đáng chú ý nhất chính là:

```html
<param value="/Music/nghe_album.aspx?id=100039571" name="FileName"/>
```

Hoặc trong đoạn embed cũng tương tự thế:

```html
src="/Music/nghe_album.aspx?id=100039571"
```

**2. Thấy được cái link "đáng ngờ", giờ thì thử open nó trên trình duyệt xem thế nào :)**

Ghép vào với tên miền thì được đường dẫn http://www.nhacso.net/Music/nghe_album.aspx?id=100039571.
Tớ dùng firebug trên Firefox để tiện theo dõi các hoạt động, request client-server.

Khi copy + paste địa chỉ mới này vào trình duyệt sẽ được redirect tới 1 trang khác, và dữ liệu trả
về là một dạng playlist (xml). Đây chính là dữ liệu chứa các thông tin về bài hát, tất nhiên là cả
link bài hát. Ví dụ dữ liệu trả về của địa chỉ trên sẽ là:

```xml
<ASX Version="3"><param name="encoding" value="utf-8" /><TITLE> Tinh Trong Mat Biec Quoc Thai Nhom Cat

 Trang Tinh Trong Mat Biec </TITLE><ENTRY><TITLE> Tinh Trong Mat Biec Quoc Thai Nhom Cat Trang Tinh Trong

 Mat Biec </TITLE> <AUTHOR>Nhom Cat Trang</AUTHOR><REF HREF="mms://210.245.126.171/Music/NhacTre/TinhTrongMatBiec_NhomCatTrang

/wma32/TinhTrongMatBiec_TinhTrongMatBiec_NhomCatTrang_02.wma"/><REF HREF="http://210.245.126.171/Music

/NhacTre/TinhTrongMatBiec_NhomCatTrang/wma32/TinhTrongMatBiec_TinhTrongMatBiec_NhomCatTrang_02.wma"/

></ENTRY><ENTRY><TITLE> Con Duong Den Lop Le Quoc Thang Nhom Cat Trang Tinh Trong Mat Biec </TITLE>

<AUTHOR>Nhom Cat Trang</AUTHOR><REF HREF="mms://210.245.126.171/Music/NhacTre/TinhTrongMatBiec_NhomCatTrang

/wma32/ConDuongDenLon_TinhTrongMatBiec_NhomCatTrang_03.wma"/><REF HREF="http://210.245.126.171/Music

/NhacTre/TinhTrongMatBiec_NhomCatTrang/wma32/ConDuongDenLon_TinhTrongMatBiec_NhomCatTrang_03.wma"/><

/ENTRY><ENTRY><TITLE> Them Nghe Ba Mang Quoc Thai Nhom Cat Trang Tinh Trong Mat Biec </TITLE> <AUTHOR

>Nhom Cat Trang</AUTHOR><REF HREF="mms://210.245.126.171/Music/NhacTre/TinhTrongMatBiec_NhomCatTrang

/wma32/ThemNgheBaMang_TinhTrongMatBiec_NhomCatTrang_04.wma"/><REF HREF="http://210.245.126.171/Music

/NhacTre/TinhTrongMatBiec_NhomCatTrang/wma32/ThemNgheBaMang_TinhTrongMatBiec_NhomCatTrang_04.wma"/><

/ENTRY><ENTRY><TITLE> Toi Va Ban Vu Dinh An Nhom Cat Trang Tinh Trong Mat Biec </TITLE> <AUTHOR>Nhom

 Cat Trang</AUTHOR><REF HREF="mms://210.245.126.171/Music/NhacTre/TinhTrongMatBiec_NhomCatTrang/wma32

/ToiVaBan_TinhTrongMatBiec_NhomCatTrang_05.wma"/><REF HREF="http://210.245.126.171/Music/NhacTre/TinhTrongMatBiec_NhomCatTrang

/wma32/ToiVaBan_TinhTrongMatBiec_NhomCatTrang_05.wma"/></ENTRY><ENTRY><TITLE> Em Di Trong Thu Roi Quoc

 Thai Nhom Cat Trang Tinh Trong Mat Biec </TITLE> <AUTHOR>Nhom Cat Trang</AUTHOR><REF HREF="mms://210

.245.126.171/Music/NhacTre/TinhTrongMatBiec_NhomCatTrang/wma32/EmDiTrongThuRoi_TinhTrongMatBiec_NhomCatTrang_06

.wma"/><REF HREF="http://210.245.126.171/Music/NhacTre/TinhTrongMatBiec_NhomCatTrang/wma32/EmDiTrongThuRoi_TinhTrongMatBiec_NhomCatTrang_06

.wma"/></ENTRY><ENTRY><TITLE> Mai Truong Men Yeu Le Quoc Thang Nhom Cat Trang Tinh Trong Mat Biec </TITLE

> <AUTHOR>Nhom Cat Trang</AUTHOR><REF HREF="mms://210.245.126.171/Music/NhacTre/TinhTrongMatBiec_NhomCatTrang

/wma32/MaiTruongMenYeu_TinhTrongMatBiec_NhomCatTrang_07.wma"/><REF HREF="http://210.245.126.171/Music

/NhacTre/TinhTrongMatBiec_NhomCatTrang/wma32/MaiTruongMenYeu_TinhTrongMatBiec_NhomCatTrang_07.wma"/>

</ENTRY><ENTRY><TITLE> Tuoi Hong Em Den Nguyen Hoa Nhom Cat Trang Tinh Trong Mat Biec </TITLE> <AUTHOR

>Nhom Cat Trang</AUTHOR><REF HREF="mms://210.245.126.171/Music/NhacTre/TinhTrongMatBiec_NhomCatTrang

/wma32/TuoiHongEmDen_TinhTrongMatBiec_NhomCatTrang_08.wma"/><REF HREF="http://210.245.126.171/Music/NhacTre

/TinhTrongMatBiec_NhomCatTrang/wma32/TuoiHongEmDen_TinhTrongMatBiec_NhomCatTrang_08.wma"/></ENTRY><ENTRY

><TITLE> Loi Nhan Nhu Quoc Thai Nhom Cat Trang Tinh Trong Mat Biec </TITLE> <AUTHOR>Nhom Cat Trang</AUTHOR

><REF HREF="mms://210.245.126.171/Music/NhacTre/TinhTrongMatBiec_NhomCatTrang/wma32/LoiNhanNhu_TinhTrongMatBiec_NhomCatTrang_09

.wma"/><REF HREF="http://210.245.126.171/Music/NhacTre/TinhTrongMatBiec_NhomCatTrang/wma32/LoiNhanNhu_TinhTrongMatBiec_NhomCatTrang_09

.wma"/></ENTRY></ASX>
```
Từ đây có thể dùng XML Parser để thấy thông tin cần.

**3. Lấy tự động**

Tớ dùng PHP + cURL. Tất nhiên có thể dùng bất kỳ ngôn ngữ nào cũng được, miễn là có thể tạo request
http là được. Tớ viết 1 class Indexer có chức năng là thu thập thông tin bài hát và ghi vào cơ sở
dữ liệu. Đầu vào là các link site nhạc được hỗ trợ, đầu ra là một đối tượng thuộc class Song
(abstract class).

Chỉ cần có có link nhạc bất kì là được rồi. Đây là Indexer class:

```php
<?php
/*
 * Indexer.class.php
 *
 * Indexer Class: Factory Design Pattern
 *
 */
class Indexer {
    private function __construct() {
        // No constructer
    }
    public static function factory($indexURL) {
        $urlInfo = parse_url($indexURL);
        $host = $urlInfo['host'];
        if (!(strstr($host, 'www.'))) {
            $host = 'www.' . $host;
            $indexURL = $urlInfo['scheme'] . '://www.' . $urlInfo['host'] . $urlInfo['path'];
            if ($urlInfo['query']) {
                $indexURL .= '?' . $urlInfo['query'];
            }
        }
        //self::$indexURL = $indexURL;
        $className = self::_getSongClass($host);
        $genre = self::_getGenre();
        $country = self::_getCountry();
        return new $className($indexURL, $genre, $country);
    }
    //http://www.nhaccuatui.com/nghe?M=fMAlI445u6
    private static function _getSongClass($host) {
        return str_replace('.', '_', $host);
    }
    private static function _getGenre() {
        //TODO: Need implementation
        return;
    }
    private static function _getCountry() {
        //TODO: Need implementation
        return;
    }
}
?>
```

Cách sử dụng:

```php
$url = 'http://www.nhacso.net/Music/Song/Nhac-Nhe/2007/06/05F62DF7/';
// $url is any link that I complete the site parser.
$objSong = Indexer::factory($url);
//Get info:
$objSong->sname // song name
$objSong->slink // song link
$objSong->... // many other attributes.
```

Nói tạm đến đây đã...
