---
layout: post
author: minhquy
title: Các loại vòng lặp trong PHP
categories: [học php, học code]
tags: [php, loop]
excerpt_separator: <!--more-->
---
<!--more-->
## Các vòng lặp Php
+ Các vòng lặp được sử dụng nhằm mục đích thi khối lệnh nào đó nhiều lần. Trong Php cung cấp một số loại vòng lặp:

- Vòng lặp `for` lặp lại một khối lệnh một số lần.
- Vòng lặp while lặp lại khối lệnh nếu điều kiện kiểm tra là đúng.
- Vòng lặp `do` ... `while` đầu tiên thi hành khối lệnh, đến cuối khối lệnh kiểm tra điều kiện, nếu điều kiện đúng thì lặp lại khối lệnh.
- Vòng lặp `foreach` lặp lại khối lệnh cho từng phần tử của một mảng, một interial
Sử dụng trong vòng lặp có hai loại từ khóa hay sử dụng là `break` và `continue`, để điều hướng lại vòng lặp.

# Các ví dụ 
đang cập nhật thêm...
## Vòng lặp for
Thường bạn sử dụng vòng lặp này khi đã biết rõ số lần cần lặp lại.

Cú pháp vòng lặp for:
```
for (khởi_tạo; điều_kiện; tăng_giảm)
{
    Code thi hành;
}
```
Như vậy vòng lặp for có ba tham số điều khiển lặp cách nhau bởi dấu ; là khởi tạo, điều_kiện, tăng_giảm. Sự làm việc như sau:

Khởi đầu thi hành lệnh tại khởi tạo
Kiểm tra biểu thức điều_kiện, nếu là true thi hành khối lệnh rồi sang bước 3, nếu `false` kết thúc lặp.
Kết thúc khối lệnh, thi hành biểu thức tăng_giảm, lặp lại bước 2
Lưu ý việc viết ba tham số của for, không cận thận có thể dẫn đền vòng lặp vô tận.

Ví dụ lặp lại khối lệnh 10 lần:

```
for ($i = 1; $i<=10; $i++) {
    echo "Vòng lặp thứ $i <br>";
}
```