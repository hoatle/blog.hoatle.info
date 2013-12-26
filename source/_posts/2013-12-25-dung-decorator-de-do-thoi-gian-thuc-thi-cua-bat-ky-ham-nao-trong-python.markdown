---
layout: post
title: 'Dùng "decorator" để đo thời gian thực thi của bất kỳ hàm nào trong Python'
author: hoatle
date: 2013-12-25 20:09
comments: true
categories:
    - "vi"
tags:
    - "python"
    - "decorator"
cover: /images/2013/12/python-logo-master.png
description: Dùng "decorator" để đo thời gian thực thi của bất kỳ hàm nào trong Python
keywords: python, decorator, timeout, hàm, đo thời gian
published: true
---

{% img center /images/2013/12/python-logo-master.png Python Logo %}

Python có cú pháp cho "decorator" rất linh hoạt, nó được sử dụng khá rộng rãi.
Bài viết này tôi giới thiệu cách sử dụng "decorator" cho một ví dụ khá hay:
dùng "decorator" để đo đếm thời gian thực thi của bất kỳ hàm nào.

<!-- more -->

"decorator" là gì?
------------------

Bạn đừng nhầm lẫn "decorator" trong Python với "decorator design pattern"[^1]
vì nó còn làm được nhiều hơn thế, nó nghiêng về "AOP (Aspect Oriented
Programming)"[^2] hơn.

Để tìm hiểu nhiều hơn về "decorator" trong Python, bạn có thể xem các bài viết
trong phần đọc thêm bên dưới.

Yêu Cầu
-------

Đo thời gian thực thi của hàm sau (theo mili-giây):

```python
def add(x, y):
    return x + y
```

Lưu tệp tin là: "add.py".

Đo Thời Gian Theo Cách Đơn Giản Nhất
------------------------------------

Để đo thời gian thực thi, cách đơn giản nhất là đếm thời gian trước lúc chạy và
sau khi chạy xong hàm, rồi lấy thời gian sau trừ thời gian trước cho khoảng
thời gian thực thi.

Có thể viết như sau:

```python
import time


def add(x, y):
    return x + y

# test
start_time = time.time()
add(3, 4)
end_time = time.time()
print 'total run-time: %f ms' % ((end_time - start_time) * 1000)
```

Sau khi chạy `$ python add.py` có kết quả tương tự như sau:

```bash
$ python add.py
total run-time: 0.007153 ms
```

Đấy là cách đo đơn giản nhất mà có thể làm được với bất kỳ ngôn ngữ nào, nhưng
cách đo đếm này không hiệu quả khi cần đo đếm hàng nghìn hàm, code sẽ bị trùng
lặp nhiều ("boiler plate").


Đo Thời Gian Dùng "decorator design pattern"
--------------------------------------------

Trong Python, có thể làm như sau:

```python
import time


def timer(fn):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = fn(*args, **kwargs)
        end_time = time.time()
        print 'total run-time of %r: %f ms' % (fn.__name__, (end_time - start_time) * 1000)
        return result
    return wrapper


def add(x, y):
    return x + y

add = timer(add)

def sub(x, y):
    return x - y

sub = timer(sub)

# test
add(3, 4)
sub(3, 4)
```

Kết quả chạy có thể như sau:

```bash
$ python add.py
total run-time of 'add': 0.143051 ms
total run-time of 'sub': 3.393173 ms
```

Đây là cách làm thường thấy trước khi cú pháp "decorator" được giới thiệu, có
thể dùng `timer` để đo đếm các hàm, ví dụ `add` và `sub` như trên.


Dùng Cú Pháp Của "decorator"
----------------------------

Rất đơn giản, thay vì dùng `add = timer(add)` thì dùng `@timer`:

```python
import time


def timer(fn):
    def wrapper(*args, **kwargs):
        start_time = time.time()
        result = fn(*args, **kwargs)
        end_time = time.time()
        print 'total run-time of %r: %f ms' % (fn.__name__, (end_time - start_time) * 1000)
        return result
    return wrapper

@timer
def add(x, y):
    return x + y

@timer
def sub(x, y):
    return x - y

# test
add(3, 4)
sub(3, 4)
```

Như vậy bằng việc dùng "decorator", code Python dễ đọc hơn, lưu ý bạn có thể
thêm nhiều "decorator" cho 1 hàm.


Ứng Dụng `timer`
---------------

Đo đếm thời gian liên quan đến "performance-tuning" và "timeout" - giới hạn
thời gian thực thi của hàm, nếu lâu quá thì thông báo lỗi và phải xử lý. Ví dụ
chỉ cho hàm `add` trên được thực thi trong khoảng `0.007 ms` thì làm như sau:

```python
import sys
import time


class TimeoutException(Exception):
    pass


def timeout(val=sys.maxsize, info=False):
    def wrapper(fn):
        def wrapper_fn(*args, **kwargs):
            start_time = time.time()
            result = fn(*args, **kwargs)
            end_time = time.time()
            run_time = (end_time - start_time) * 1000 # miliseconds
            if val < run_time:
                raise TimeoutException('%r run-time: expected: %f ms, but actual: %f ms' % (fn.__name__, val, run_time))
            if info:
                print '%r run-time: %f ms' % (fn.__name__, run_time)
            return result
        return wrapper_fn
    return wrapper


@timeout(0.007)
def add(x, y):
    return x + y

@timeout(info=True)
def sub(x, y):
    return x - y

# Test

add(3, 4)

sub(3, 4)
```


`timeout` nhận 2 tham số là `val` - giá trị "timeout" và in ra thông tin thời
gian chạy với tham số `info`.

Khi thời gian thực thi của `add` quá 0.007 mili-giây sẽ xảy ra
`TimeoutException` tương tự như lần chạy sau:

```bash
$ python add.py
Traceback (most recent call last):
  File "add.py", line 35, in <module>
    add(3, 4)
  File "add.py", line 17, in wrapper_fn
    raise TimeoutException('%r run-time: expected: %f ms, but actual: %f ms' % (fn.__name__, val, run_time))
__main__.TimeoutException: 'add' run-time: expected: 0.007000 ms, but actual: 0.137091 ms
```

Tổng Kết
--------

Như vậy bạn có thể quản lý và đưa giới hạn thời gian thực thi cho bất kỳ hàm
nào, điều này khá quan trọng với vấn đề "performance" cũng như "security" nhờ
cách dùng "decorator" rất linh hoạt trong Python. Đây chỉ là một ứng dụng nho
nhỏ của "decorator", chúc bạn có thể áp dụng "decorator" trong nhiều bài
toán thực tế hơn.


Đọc Thêm
--------

- http://www.artima.com/weblogs/viewpost.jsp?thread=240808
- http://www.artima.com/weblogs/viewpost.jsp?thread=240845
- http://en.wikipedia.org/wiki/Python_syntax_and_semantics#Decorators


Hình Ảnh
--------

- http://www.vizteams.com/blog/why-python-as-programming-language-past-present-future

[^1]: http://en.wikipedia.org/wiki/Decorator_pattern
[^2]: http://en.wikipedia.org/wiki/Aspect-oriented_programming
