---
layout: post
author: minhquydesign
title: Các kiểu dữ liệu trong PHP
categories: [PHP Data Types]
tags: [PHP, Data, Type]
excerpt_separator: <!--more-->
---




Các biến có thể lưu trữ dữ liệu thuộc các kiểu khác nhau và các kiểu dữ liệu khác nhau có thể làm những việc khác nhau.
<!--more-->

# PHP hỗ trợ các kiểu dữ liệu sau:

- String  là một chuỗi các ký tự, như "Hello world!". Một chuỗi có thể là bất kỳ văn bản nào bên trong dấu ngoặc kép. Bạn có thể sử dụng dấu ngoặc kép hoặc đơn:
- Integer - Kiểu dữ liệu số nguyên là một số không thập phân từ -2,147,483,648 đến 2,147,483,647.
+ Quy tắc cho số nguyên: 
	- Một số nguyên phải có ít nhất một chữ số 
	- Một số nguyên không được có dấu thập phân 
	- Một số nguyên có thể là số dương hoặc số âm 
	- Số nguyên có thể được chỉ định trong ký hiệu: thập phân (cơ số 10), thập lục phân (cơ số 16), bát phân (cơ số 8) hoặc ký hiệu nhị phân (cơ số 2)
Trong ví dụ sau, $ x là một số nguyên. Hàm var_dump () trong PHP trả về kiểu dữ liệu và giá trị:

### Example
```
<?php
$x = 5985;
var_dump($x);
?>
```

- Float (floating point numbers - also called double)
- Boolean
- Array
- Object
- NULL
- Resource