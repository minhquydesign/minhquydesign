---
layout: post
author: minhquy
title: Phân trang dữ liệu trong PHP code
categories: [PHP]
tags: [PHP, SQL, MySQL, Phân Trang]
excerpt_separator: <!--more-->
---

Dưới đây là Thuật toán phân trang, hướng dẫn làm chức năng phân trang trong PHP.

Phân trang cơ bản là quá trình lấy một tập hợp các kết quả và phân chia thành các trang để dễ xem hơn.Với những trang Web có dữ liệu lớn, việc phân trang là rất quan trọng, nó giúp trang web sẽ load nhanh hơn , giúp người dùng dễ dàng nhấn chọn trang mà mình mong muốn, đến được trang có nội dung mà mình cần, rất nhanh chóng, dễ dàng và chính xác.
<!--more-->
# Tạo database
Tạo một Cơ sở dữ liệu ví dụ `demo_phantrang`.
Thực hiện truy vấn SQL trong PHPMyadmin trong DATABASENAME `demo_phantrang` như sau:
```
CREATE TABLE IF NOT EXISTS `news` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `title` varchar(255) COLLATE utf8_unicode_ci DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB  DEFAULT CHARSET=utf8 COLLATE=utf8_unicode_ci AUTO_INCREMENT=18 ;
```
SQL là một ngôn ngữ khá đơn giản và dễ học.
Nếu bạn chưa học về SQL thì có thể xem đoạn mô tả thêm của chúng tôi.
Trong đó:
- ` CREATE TABLE IF NOT EXISTS `news` ` tạo bảng news nếu bảng không tồn tại.
- ` CHARSET=utf8 COLLATE=utf8_unicode_ci ` hỗ trợ lưu trữ những đoạn text tiếng việt có dấu.
- ` DEFAULT NULL ` mặc định sẽ là giá trị NULL.
- `` `id` int(11) NOT NULL AUTO_INCREMENT ` khai báo cột id với giá trị là integer độ dài 11, không null, tự độnng tăng dần giá trị.
# Tiếp tục thực hiện truy vấn SQL chèn dữ liệu vào bảng `test_phantrang`
 ```
 INSERT INTO `news` (`id`, `title`) VALUES
(1, 'Title 1'),
(2, 'Title 2'),
(3, 'Title 3'),
(4, 'Title 4'),
(5, 'Title 5'),
(6, 'Title 6'),
(7, 'Title 7'),
(8, 'Title 8'),
(9, 'Title 9'),
(10, 'Title 10'),
(11, 'Title 11'),
(12, 'Title 12'),
(13, 'Title 13'),
(14, 'Title 14'),
(15, 'Title 15'),
(16, 'Title 16'),
(17, 'Title 17');
```

# Tạo trang index.php

Đây là toàn bộ nội dung file `index.php` của chúng tôi, trang hiển thị đoạn phân trang của bạn.
bạn có thể thay đổi tên file  `index.php` thành ví dụ `tenfile.php` và thay thế `index.php` thành `tenfile.php` trong file.
```
<!DOCTYPE html>
<html>
    <head>
        <title>Ví dụ phân trang trong PHP và MySQL</title>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
    </head>
    <body>
        <?php 
        // PHẦN XỬ LÝ PHP
        // BƯỚC 1: KẾT NỐI CSDL
        $conn = mysqli_connect('localhost', 'root', 'vertrigo', 'demo_phantrang');
 
        // BƯỚC 2: TÌM TỔNG SỐ RECORDS
        $result = mysqli_query($conn, 'select count(id) as total from news');
        $row = mysqli_fetch_assoc($result);
        $total_records = $row['total'];
 
        // BƯỚC 3: TÌM LIMIT VÀ CURRENT_PAGE
        $current_page = isset($_GET['page']) ? $_GET['page'] : 1;
        $limit = 10;
 
        // BƯỚC 4: TÍNH TOÁN TOTAL_PAGE VÀ START
        // tổng số trang
        $total_page = ceil($total_records / $limit);
 
        // Giới hạn current_page trong khoảng 1 đến total_page
        if ($current_page > $total_page){
            $current_page = $total_page;
        }
        else if ($current_page < 1){
            $current_page = 1;
        }
 
        // Tìm Start
        $start = ($current_page - 1) * $limit;
 
        // BƯỚC 5: TRUY VẤN LẤY DANH SÁCH TIN TỨC
        // Có limit và start rồi thì truy vấn CSDL lấy danh sách tin tức
        $result = mysqli_query($conn, "SELECT * FROM news LIMIT $start, $limit");
 
        ?>
        <div>
            <?php 
            // PHẦN HIỂN THỊ TIN TỨC
            // BƯỚC 6: HIỂN THỊ DANH SÁCH TIN TỨC
            while ($row = mysqli_fetch_assoc($result)){
                echo '<li>' . $row['title'] . '</li>';
            }
            ?>
        </div>
        <div class="pagination">
           <?php 
            // PHẦN HIỂN THỊ PHÂN TRANG
            // BƯỚC 7: HIỂN THỊ PHÂN TRANG
 
            // nếu current_page > 1 và total_page > 1 mới hiển thị nút prev
            if ($current_page > 1 && $total_page > 1){
                echo '<a href="index.php?page='.($current_page-1).'">Prev</a> | ';
            }
 
            // Lặp khoảng giữa
            for ($i = 1; $i <= $total_page; $i++){
                // Nếu là trang hiện tại thì hiển thị thẻ span
                // ngược lại hiển thị thẻ a
                if ($i == $current_page){
                    echo '<span>'.$i.'</span> | ';
                }
                else{
                    echo '<a href="index.php?page='.$i.'">'.$i.'</a> | ';
                }
            }
 
            // nếu current_page < $total_page và total_page > 1 mới hiển thị nút prev
            if ($current_page < $total_page && $total_page > 1){
                echo '<a href="index.php?page='.($current_page+1).'">Next</a> | ';
            }
           ?>
        </div>
    </body>
</html>
```
Trong đó:
- `$total_records` tổng số hàng đã lấy được từ csdl dạng number.
- `$total_page` tổng số trong tính được sau khi chia `$limit`.
- `$current_page` trang hiện tại.
- `$limit` đặt số hàng hiển thị mỗi trang có thể thay đổi.

Thế là xong.
