---
layout: post
author: minhquy
title: Codeiginer - Xóa index.php khỏi URL
categories: [Codeiginer]
tags: [Codeiginer, index.php]
excerpt_separator: <!--more-->
---
Codeigniter là một khung công tác php hỗ trợ các URL sạch.

Bằng cách đó, bạn có thể tạo một URL dễ đọc và thân thiện với SEO.
<!--more-->
Trong URL ứng dụng "Hello World" ở trên, có thể thấy rằng index.php trong url trông rất khó chịu.

Có cách nào để xóa `index.php` khỏi URL không?

Tất nhiên, bạn có thể sử dụng tệp **.htaccess** để xóa nó.

Làm thế nào để tạo tệp **.htaccess** ?

Hãy bắt đầu nào.

Tạo một tệp có tên **.htaccess** trên thư mục gốc của bạn và nhập mã bên dưới:

```
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^(.*)$ index.php?/$1 [L]
```
Giống như hình dưới đây:

...


Sau đó, mở thư mục `application / config / config.php` bằng trình soạn thảo văn bản.

Và sau đó tìm mã bên dưới:

```
$config['index_page'] = 'index.php';
```
Và thiết lập như thế này:

```
$config['index_page'] = '';
```
Bây giờ, vui lòng truy cập url sau để thử nghiệm:
ví dụ

``http: // localhost / myproject /``
Chúc các bạn thành công