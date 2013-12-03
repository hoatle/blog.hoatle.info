---
layout: post
title: "Bài tập tách chuỗi PHP"
author: hoatle
date: 2008-12-17 03:14
comments: true
categories:
    - "vi"
tags:
    - "PHP"
cover:
description: Bài tập tách chuỗi PHP
keywords: Bài tập tách chuỗi PHP
published: true
---

**Bài toán**: Cho một chuỗi như sau:
`http://210.245.126.171/Music/NhacTre/TinhYeu_LyMaiTrang/wma32/06_BienTham_TinhYeu_LyMaiTrang.wma`
(Đây là một link bài hát trên NhacSo.net. Nhìn vào tên file ta có thể biết nhiều thông tin về bài
hát này. Có thể thấy đây là bài số 06 mang tên Biển Thắm trong album Tình Yêu của ca sĩ Lý Mai Trang.
Bạn hãy trích thành một mảng `$info` như sau:

<!-- more -->

```php
$info = array (
  'no' => '06',
  'name' => 'Bien Tham',
  'album' => 'Tinh Yeu',
  'singer' => 'Ly Mai Trang',
  'link' => 'http://210.245.126.171/Music/NhacTre/TinhYeu_LyMaiTrang/wma32/06_BienTham_TinhYeu_LyMaiTrang.wma'
);
```

**Hướng giải quyết:**

1. Tách tên file ra để phân tích => 06_BienTham_TinhYeu_LyMaiTrang
2. Tách chuỗi thành mảng từ dấu phân cách "_" => ("06", "BienTham", "TinhYeu", "LyMaiTrang")
3. Xử lý nốt dấu cách trong từ => ("06", "Bien Tham", "Tinh Yeu", "Ly Mai Trang")
4. Done

**Bước 1:**

```php
$httpHref  = 'http://210.245.126.171/Music/NhacTre/TinhYeu_LyMaiTrang/wma32/06_BienTham_TinhYeu_LyMaiTrang.wma';
$slashPos  = strrpos($httpHref, '/');
$fileName  = substr($httpHref, $slashPos+1, strlen($httpHref) - $slashPos);
$dotPos    = strrpos($fileName, '.');
$extension = substr($fileName, $dotPos, strlen($fileName)-$dotPos);
$fileName  = str_replace($extension, '', $fileName);
```

**Bước 2:**

```php
list($no, $name, $album, $singer) = explode('_', $fileName);
```

**Bước 3:**
(Có vẻ như khó nhất, làm sao tách: BienTham => Bien Tham; LyMaiTrang => Ly Mai Trang??? Sau một hồi
loay hoay cuối cùng cũng viết xong cái hàm biến đối nảy: input là một chuỗi có các ký tự liên tiếp
nhau kiểu LyMaiTrang và output phải là Ly Mai Trang.

```php
function correct_string($str) {
    $strLen = strlen($str);
    $arrStack = array();
    array_push($arrStack, substr($str, 0, 1));
    for ($i = 1; $i < $strLen; $i++) {
        $currentChar =  substr($str, $i, 1);
        if (ctype_upper($currentChar)) {
            $currentChar = ' ' . $currentChar;
        }
        array_push($arrStack, $currentChar);
    }
    return implode('', $arrStack);
}
```

**Phù!!! Thế là xong:**

```php
$httpHref = 'http://210.245.126.171/Music/NhacTre/TinhYeu_LyMaiTrang/wma32/06_BienTham_TinhYeu_LyMaiTrang.wma';
$slashPos = strrpos($httpHref, '/');
$fileName = substr($httpHref, $slashPos+1, strlen($httpHref) - $slashPos);
$dotPos = strrpos($fileName, '.');
$extension = substr($fileName, $dotPos, strlen($fileName)-$dotPos);
$fileName = str_replace($extension, '', $fileName);
list($no, $name, $album, $singer) = explode('_', $fileName);
$name = correct_string($name);
$album = correct_string($album);
$singer = correct_string($singer);
$info = array(
    'no' => $no,
    'name' => $name,
    'album' => $album,
    'singer' => $singer,
    'link'    => $httpHref
);

function correct_string($str) {
    $strLen = strlen($str);
    $arrStack = array();
    array_push($arrStack, substr($str, 0, 1));
    for ($i = 1; $i < $strLen; $i++) {
        $currentChar =  substr($str, $i, 1);
        if (ctype_upper($currentChar)) {
            $currentChar = ' ' . $currentChar;
        }
        array_push($arrStack, $currentChar);
    }
    return implode('', $arrStack);
}
```


