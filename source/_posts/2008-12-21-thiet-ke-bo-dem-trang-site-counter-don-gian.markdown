---
layout: post
title: "Thiết kế bộ đếm trang (site-counter) đơn giản"
author: hoatle
date: 2008-12-21 05:38
comments: true
categories:
    - "vi"
tags:
    -
cover:
description: Thiết kế bộ đếm trang (site-counter) đơn giản
keywords:
published: true
---

Lại thêm một thứ đơn giản nữa :). Bộ đếm trang trước đây và cả bây giờ vẫn rất phổ biến. Có một số
nhà cung cấp miễn phí bộ đếm cho bạn, chỉ việc đăng kí một tài khoản + nhúng đoạn code site-counter
vào trang của bạn là xong :). Có bạn lại không thích như thế, muốn tự mình viết một cái site-counter
riêng :). Bài viết này sẽ hướng dẫn + chia sẻ 1 bộ đếm trang đơn giản bằng PHP + MySQL.

<!-- more -->

Vì bảng dữ liệu khá nhỏ nên có thể sử dụng SQLite làm cơ sở dữ liệu, nhưng hiện giờ cái site-counter
này của tớ chỉ đang hỗ trợ MySQL.

Demo: http://d9k50.net/test/term7. Bạn để ý thấy bộ đếm trang nằm ở góc phải phía dưới ngoài cùng,
có thống kê một số thông số nhất định về tình hình truy cập website. Bạn có thể dùng bộ đếm trang
này để theo dõi, tuy nhiên thống kê chỉ có tính chất tương đối vì chả có cái gì là tuyệt đối
(mà nói chung thì thống kê chẳng bao giờ đúng :D).

**1. Cấu trúc file**

```
- config.php // Thông số cài đặt cơ sở dữ liệu: hostname, username, password và dabasename
- install.php // Chạy "1 lần rồi thôi" khi lần đấu bạn cài đặt bộ đếm trang này, sau đó nên xoá luôn đi
- site-counter-block.php // Include file này vào bất kỳ chỗ nào trong site của bạn để hiển thị thống kê
- site-counter-block.tpl.php // Đây là file template
- site-counter-include.php // Nên Include file này vào header để session hoạt động tốt
- SiteCounter.class.php // SiteCounter class - quan trọng nhất
- site-counter-block.css // Để tùy chỉnh style cho site-counter khi hiển thị
- site-counter-test.php // Để test
```

Đấy là các file thiết yếu nhất, còn lại những phụ kiện phụ khác như: CHANGELOG.txt, INSTALL.txt,
LICENSE.txt, README.txt, TODO.txt nữa. Ở đây chỉ bàn đến mấy file quan trọng trên thôi.

*2. Lần lượt phân tích từng file*

2.1 `config.php`

Lưu cấu hình về hostname, username, password và databasename để site-counter chạy được. Khi cài đặt
thì điều đầu tiên là bạn phải điền các thông số vào trong file này.

```php
<?php
// $Id$
/**
 * Config file for SiteCounter to work
 *
 * Edit to match your database, replace your_host by your host name...
 * your_host is the host of your database
 * your_username is the MySQL account of your database
 * your_password is the password for that account
 * your_database is the database name
 */

define('HOST', 'your_host');
define('USERNAME', 'your_username');
define('PASSWD', 'your_password');
define('DBNAME', 'your_databasename');
```

2.2 `install.php`

"Chạy 1 lần rồi thôi" để tạo bảng. Sau khi báo tạo bảng thành công thì bạn nên xóa file này đi
luôn.

```php
<?php
// $Id$
/**
 * @file
 * Install file
 *
 * This enables to create table site_counter in your database to track visitor's information
 */
require_once 'config.php'; // Configuration file
$query = "CREATE TABLE site_counter (
   `ip` varchar(20) NOT NULL,
   `timestamp` int(11) NOT NULL,
   `visits` int(4) DEFAULT '1'
);"; // Query to create table.
mysql_connect(HOST, USERNAME, PASSWD) or die('Could not connect to the host!');
mysql_select_db(DBNAME) or die('Could not select database!');
mysql_query($query) or die('Could not create table!');
echo 'Successful create table for site-counter! Please delete this install.php file by now.';
```

Ở đây sau khi chạy thành công sẽ tạo được bảng `site_counter` với 1 số trường sau: `ip (distinct)`,
`timestamp`, `visits`. Nếu chưa có `ip` trong bảng thì `insert`, nếu có rồi và là `session` mới thì
`update` tăng `visits` lên 1. Chỉ thế thôi.

2.3 `SiteCounter.php`

Quan trọng bậc nhất và là cái đáng bàn nhiều nhất. Tuy nhiên khi nhìn vào source code là bạn có thể
biết được cách hoạt động của nó luôn.

```php
<?php
// $Id$
/**
 * start session handler to avoid repetitive request info (visits) update for each session
 *
 * Is there any other better solution???
 */
session_start();

/**
 * SiteCounter class to track and update basic site's info
 *
 * This is a Singleton Class to track and update basic site's info
 * such as: IP, Visits, Total hits, Online, Unique visitors
 *
 * @copyright  hoatle (hoatle.net)
 * @author     hoatle
 * @license    http://opensource.org/licenses/gpl-license.php GNU Public License
 * @version    1.0
 * @link       http://hoatle.net/Project-Site-Counter
 * @since      Class available since Release 1.0
 */
class SiteCounter
{

    /**
     * static property to hold singleton instance
     * @access private
     * @static
     * @var SiteCounter
     */
    private static $instance = false;

    /**
     * constant duration (in minutes) to get total online users
     */
    const DURATION = 5;

    /**
     * ip addressquery
     * @access private
     * @var string
     */
    private $ip;

    /**
     * number of visitis to your site from  this IP address
     * @access private
     * @var integer
     */
    private $visits;

    /**
     * number of online visitors
     * @access private
     * @var integer
     */
    private $online;

    /**
     * number of total hits since your connter's first operation
     * @access private
     * @var integer
     */
    private $totalHits;

    /**
     * number of unique visitors (ip address) since your counter's first operation
     * @access private
     * @var integer
     */
    private $unique;

    /**
     * database connection id to access
     * @access private
     * @static
     * @var resource
     */
    private static $dbConnectionId;

    /**
     * SiteCounter::__construct()
     *
     * private so only getInstance() method can instantiate
     * @access private
     * @return void
     */
    private function __construct()
    {
        // Get the IP address
        $this->ip = $_SERVER['REMOTE_ADDR'];
        // Get Info from request and insert to the database
        $this->_updateRequestInfo();
        // Get Info from database and update Counter instance
        $this->_updateCounterInfo();
    }

    /**
     * SiteCounter::_updateRequestInfo()
     *
     * Get request info and update database
     * @access private
     * @return void
     */
    private function _updateRequestInfo()
    {
        // Get current timestamp
        $time = time();
        $query = "SELECT * FROM site_counter "
               . "WHERE `ip` = '$this->ip'";
        $res = mysql_query($query, $this->_getDbConnection());
        $row = mysql_fetch_object($res);
        // Check ip existence in the table
        if ($row->ip) {
          // If ip exists, update visits
          $visits = $row->visits; // current on database
          // increase $visits on each session only
          if (!$_SESSION['visitsIncreased']) {
              $visits += 1;
              $_SESSION['visitsIncreased'] = true;
          }
          $query = "UPDATE site_counter "
                 . "SET `timestamp` = $time, `visits` = $visits "
                 . "WHERE `ip` = '$this->ip'";
        } else {
          // Else, insert into database
          $query = "INSERT site_counter(`ip`, `timestamp`, `visits`) "
                 . "VALUES ('$this->ip', $time, 1)";
          $_SESSION['visitsIncreased'] = true;
        }
        mysql_query($query, $this->_getDbConnection()) or die ('Could not query database!');
    }

    /**
     * SiteCounter::_updateCounterInfo()
     *
     * Get database info and update Counter's attributes
     * @access private
     * @return void
     */
    private function _updateCounterInfo()
    {
        // Get online visitors
        // limit time
        $limitTime = time() - (self::DURATION * 60); // Count in senconds
        $query = "SELECT COUNT(*) `online` FROM site_counter "
               . "WHERE `timestamp` > $limitTime";
        $this->online = mysql_fetch_object(mysql_query($query, $this->_getDbConnection()))->online;

        // Get visits
        $query = "SELECT `visits` FROM site_counter "
               . "WHERE `ip` = '$this->ip'";
        $this->visits = mysql_fetch_object(mysql_query($query, $this->_getDbConnection()))->visits;

        // Get total hits
        $query = "SELECT SUM(`visits`) `totalHits` "
               . "FROM site_counter";
        $this->totalHits = mysql_fetch_object(mysql_query($query, $this->_getDbConnection()))->totalHits;

        // Get the number of unique visitors
        $query = "SELECT COUNT(*) `unique` FROM site_counter";


        $this->unique = mysql_fetch_object(mysql_query($query, $this->_getDbConnection()))->unique;
    }

    /**
     * SiteCounter::_getDbConnection()
     *
     * Get database connection resource, this is a singleton pattern. This method get config constant
     * from config.php file: HOST, USERNAME, PASSWD, DBNAME
     * @access private
     * @return resource $dbConnectionId
     */
    private function _getDbConnection() {
       if (!self::$dbConnectionId) {
           self::$dbConnectionId = mysql_connect(HOST, USERNAME, PASSWD) or die('Error connect to host: ' . HOST);
           mysql_select_db(DBNAME, self::$dbConnectionId) or die('Error connect to database: ' . DBNAME);
       }
       return self::$dbConnectionId;
    }

    /**
     * SiteCounter::getInstance()
     *
     * factory method to return the singleton instance
     * @access public
     * @static
     * @return Counter $instance
     */
    public static function getInstance()
    {
        if (!self::$instance) {
            // If no instance, just create one
            self::$instance = new SiteCounter();
        }
        return self::$instance;
    }

    /**
     * SiteCounter::__clone()
     *
     * Prevent from object clonning
     * @access public
     * @return Exception
     */
    final public function __clone()
    {
        return new Exception('This Counter object can not be cloned!');
    }

    /*
     * Getter method
     *
     * This magic getter method will return Counter's attributes if any
     * @acess public
     * @return mixed
     */
    public function __get($property) {
        $methodName = "get{$property}";
        if (method_exists($this, $methodName)) {
            return $this->$methodName();
        }
    }

    /**
     * SiteCounter::getIp()
     *
     * Get Ip address from the current request
     * @access public
     * @return string $ip
     */
    public function getIp()
    {
        return $this->ip;
    }

    /**
     * SiteCounter::getVisits()
     *
     * Get number of visits from the current request
     * @access public
     * @return integer $visits
     */
    public function getVisits()
    {
        return $this->visits;
    }

    /**
     * SiteCounter::getOnline()
     *
     * Get number of online user at the time of request
     * @access public
     * @return integer $online
     */
    public function getOnline()
    {
        return $this->online;
    }

    /**
     * SiteCounter::getTotalHits()
     *
     * Get total hits from the day of site-counter's operation
     * @access public
     * @return integer $totalHits
     */
    public function getTotalHits()
    {
        return $this->totalHits;
    }

    /**
     * SiteCounter::getUnique()
     *
     * Get the total number of unique visitor (ip address)
     * @access public
     * @return integer $unique
     */
    public function getUnique()
    {
        return $this->unique;
    }
}
```

Ý tưởng cho class SiteCounter: Singleton vì có thể được gọi 2 lần trong 1 file, nhưng chỉ được phép
có 1 instance trong 1 lần request. Đầu tiên là lấy ip của người dùng. Bước 1 là cập nhật cơ sở dữ
liệu (`_updateRequestInfo`): kiểm tra ip có tồn tại hay chưa, nếu chưa thì thêm 1 record vào bảng,
nếu rồi thì update visits tăng lên 1. Bước 2 là cập nhật đối tượng SiteCounter để sau đó lấy thông
tin về $ip, $visits, $online, $totalHits, $unique thông qua đối tượng được khởi tạo từ class
SiteCounter. Ví dụ:

```php
$counter = SiteCounter::getInstance();
$counter->getIp(); // = $counter->Ip;
$counter->Online; // = $counter->getOnline();
```

Có thể thấy có 2 cách lấy thuộc tính như vậy là do magic method __get() được implement. Khi bạn truy
cập thuộc tính của 1 object mà không public thì hàm __get() này sẽ được gọi và tham số được truyền
vào chính là property bạn gọi thông qua object. Tất nhiên là bạn cũng phải implement các hàm Getter
trước rồi đã, đây coi như chỉ là helper method mà thôi.

```php
    /*
     * Getter method
     *
     * This magic getter method will return Counter's attributes if any
     * @acess public
     * @return mixed
     */
    public function __get($property) {
        $methodName = "get{$property}";
        if (method_exists($this, $methodName)) {
            return $this->$methodName();
        }
    }
```

2.4 Bây giờ đến phần sử dụng class SiteCounter trên.

Đầu tiên là sẽ có 2 file được include vào trang theo dõi của bạn: site-counter-include.php và
site-counter-block.php để hiển thị. site-counter-include.php luôn phải được include vào header của
trang vì sử dụng session, nếu include sau 1 vài file thì rất có thể session sẽ không được tạo vì
header đã được gửi lại cho phía client => Warning.

File site-counter-include.php

```php
<?php
// $Id$
/**
 * @file tracking visitor's information
 *
 * To track every visitor's information on every request to any page on your website,
 * include this file on your header or footer part or any that that is represented on
 * every page of your site.
 */
require_once 'config.php';
require_once 'SiteCounter.class.php';
$counter = SiteCounter::getInstance();
```

File site-conter-block.php, site-counter-block.tpl.php và site-counter-block.css để hiển thị:

File site-counter-block.php

```php
<?php
// $Id$
/**
 * @file display visitor's information
 *
 * To display visitor's information, include this file on any part of your page.
 * Refer to README.txt on HOW TO USE part for more information.
 */
$counter = SiteCounter::getInstance();
// Get information
$ip        = $counter->Ip;
$online    = $counter->Online;
$visits    = $counter->Visits;
$totalHits = $counter->TotalHits;
$unique    = $counter->Unique;
// display it
include_once 'site-counter-block.tpl.php
```

File site-counter-block.tpl.php:

```php
<?php
// $Id$
/**
 * @file template file to display site-counter information
 * Availabe variables:
 * - $ip
 * - $visits
 * - $online
 * - $totalHits
 * - $unique
 */
?>
<div id="site-counter"><fieldset><legend>Site-Counter</legend>
<div>Your IP: <span id="ip"><?php print $ip;?></span></div>
<div>Your visits: <span id="visits"><?php print $visits;?></span></div>
<div>Online: <span id="online"><?php print $online;?></span></div>
<div>Total Hits: <span id="total-hits"><?php print $totalHits;?></span></div>
<div>Unique visitors: <span id="unique"><?php print $unique; ?></span></div>
</fieldset>
</div>
```

File site-counter-block.css:

```css
/**
 * $Id$
 * Styles site-counter
 * author: hoatle
 * website: hoatle.net
 */

 #site-counter {
    width: 220px;
    font-size: 12px;
    color: gray;
    text-align: left;
    background-color: white;
    border: 1px black dotted;
    filter: alpha(opacity=90);
    -moz-opacity: 0.09;
    opacity: 0.90;
    -khtml-opacity: 0.90;
    margin: 2em 0 0;
 }

 #site-counter div {
    text-align: left;
 }

 #site-counter div #ip {

 }

 #site-counter div #visits {

 }

 #site-counter div #online {

 }

 #site-couner div #total-hits {

 }

 #site-counter p #unique {

 }
```

2.5 Xong

Cuối cùng là test nó với trang site-counter-test.php.

```html
<?php
// $Id$
include_once 'site-counter-include.php';
?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
<meta http-equiv="Content-Type" content="text/html; charset=utf-8" />
<title>Site-Counter Test Page</title>
<link rel="stylesheet" href="site-counter-block.css" type="text/css" media="screen" />
</head>
<body>
<?php include_once 'site-counter-block.php'; ?>
</body>
</html>
```

Chúc vui :).
