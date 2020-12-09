---
layout: post
author: minhquydesign
title: SQLiteCRUD Simplite
categories: [SQLiteCRUD]
tags: [SQLiteCRUD]
excerpt_separator: <!--more-->
---

<!--more-->
- sqlitecrud simplite
# index.php
index all record

```
//<?php

// Database name
$database_name = "csdl_tudien.db";

// Database Connection
$db = new SQLite3($database_name);

// Tạo Bảng "tbl_tudien" vào Cơ sở dữ liệu nếu không tồn tại
$query =
    "CREATE TABLE IF NOT EXISTS tbl_tudien (td_id INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL, td_tv STRING, td_ts STRING, td_mt STRING, td_loai STRING, td_chude STRING, td_creat STRING, td_update STRING, td_ta STRING)";
$db->exec($query);

// Câu truy vấn cho trang index
$query = "SELECT td_id, * FROM tbl_tudien ORDER BY td_tv ASC";

// Tạo truy vấn lưu vào biến $result
$result = $db->query($query);
//?>

<?php while ($row = $result->fetchArray()) {
    ++$soHangDemDuoc; ?>
          
            <tr>
                <td><?php echo $row['td_id']; ?></td>
                <th scope="row"><a href="search.php?s=<?php echo $row[
                    'td_tv'
                ]; ?>"><?php echo $row['td_tv']; ?></a> </th>
                
                <td><?php echo $row['td_ts']; ?></td>
                
                <td><?php if ($row['td_mt']) {
                    echo "<pre class='alert alert-success border-left-primary'>" .
                        $row['td_mt'] .
                        "</pre>";
                } ?></td>
                
                <td ><button class="btn btn-primary" ><?php echo $row[
                    'td_loai'
                ]; ?></button></td>
<td><?php echo $row['td_chude']; ?></td><td><?php echo $row[
    'td_creat'
]; ?></td><td><?php echo $row['td_update']; ?></td><td><?php echo $row[
    'td_ta'
]; ?></td>

                <td>
                    <a href="search.php?s=<?php echo $row[
                        'td_tv'
                    ]; ?>" class="btn btn-success m-1 btn-sm">Search</a> |
                    <a href="update.php?id=<?php echo $row[
                        'td_id'
                    ]; ?>" class="btn btn-primary m-1 btn-sm">Edit</a> | 
                    <a href="view.php?id=<?php echo $row[
                        'td_id'
                    ]; ?>" class="btn btn-success m-1 btn-sm">view</a> |
                    
                    <a href="delete.php?id=<?php echo $row[
                        'td_id'
                    ]; ?>" onclick="return confirm('Are you sure?');" class="btn btn-default m-1 btn-sm">Delete</a>
                </td>
            </tr>
            <?php
} ?>
```

# Insert.php (add)

```
//<?php
$message = ""; // initial message 
if( isset($_POST['submit_data']) ){

    // Includs database connection
    include "db_connect.php";

    // Gets the data from post
    $td_tv = $_POST['td_tv'];
    $td_ts = $_POST['td_ts'];
    $td_mt = $_POST['td_mt'];

    $td_loai = $_POST['td_loai'];
    $td_chude = $_POST['td_chude'];
    $td_creat = $_POST['td_creat'];
    $td_update = $_POST['td_update'];
    $td_ta = $_POST['td_ta'];

    // Makes query with post data
    $query = "INSERT INTO tbl_tudien (td_tv, td_ts, td_mt, td_loai, td_chude, td_creat, td_update, td_ta) VALUES ('$td_tv', '$td_ts', '$td_mt', '$td_loai', '$td_chude', '$td_creat', '$td_update', '$td_ta')";
    
    // Executes the query
    // If data inserted then set success message otherwise set error message
    // Here $db comes from "db_connection.php"
    if( $db->exec($query) ){
        $message = "<div class='alert alert-primary' role='alert'>Data is inserted successfully. <a href='index.php' class='btn btn-primary'>Home Index</a></div>";
        // header("location:index.php");
    }else{
        $message = "Sorry, Data is not inserted.";
    }
}

#+++
if( isset($_POST['submit_data_and_backhome']) ){

    // Includs database connection
    // Database name
$database_name = "csdl_tudien.db";

// Database Connection
$db = new SQLite3($database_name);

// Create Table "bang_tudien" into Database if not exists 
// Tạo Bảng "bang_tudien" vào Cơ sở dữ liệu nếu không tồn tại
$query = "CREATE TABLE IF NOT EXISTS tbl_tudien (td_id INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL, td_tv STRING, td_ts STRING, td_mt STRING, td_loai STRING, td_chude STRING, td_creat STRING, td_update STRING, td_ta STRING)";
$db->exec($query);
   
    $td_tv = $_POST['td_tv'];
    $td_ts = $_POST['td_ts'];
    $td_mt = $_POST['td_mt'];

    $td_loai = $_POST['td_loai'];
    $td_chude = $_POST['td_chude'];
    $td_creat = $_POST['td_creat'];
    $td_update = $_POST['td_update'];
    $td_ta = $_POST['td_ta'];

    // Makes query with post data
    $query = "INSERT INTO tbl_tudien (td_tv, td_ts, td_mt, td_loai, td_chude, td_creat, td_update, td_ta) VALUES ('$td_tv', '$td_ts', '$td_mt', '$td_loai', '$td_chude', '$td_creat', '$td_update', '$td_ta')";
    
    // Executes the query
    // If data inserted then set success message otherwise set error message
    // Here $db comes from "db_connection.php"
    if( $db->exec($query) ){
        $message = "<div class='alert alert-primary' role='alert'>Data is inserted successfully. <a href='index.php' class='btn btn-primary'>Home Index</a></div>";
        header("location:index.php");
    }else{
        $message = "Sorry, Data is not inserted.";
    }
}

?>






                    <!-- showing the message here-->
                    <div><?php echo $message;?></div>

                    <table class="table table-responsive" >
                        <form action="insert.php" method="post">
                            <div class="form-group">
                            <label for="xxx">Tiếng Việt*</label>
                            <input name="td_tv" type="text" class="form-control">
                            <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
                            </div>
                    
                            <div class="form-group">
                            <label for="xxx">Tiếng Sovak*</label>
                            <input name="td_ts" type="text" class="form-control">
                            <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
                            </div>

                            <div class="form-group">
                            <label for="xxx">Mô tả/ ghi chú</label>
                            <textarea name="td_mt"    class="form-control" rows="3"></textarea>
                            <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
                            </div>


                            <!--div class="form-group">
                            <label for="xxx">td_loai*</label>
                            <input name="td_loai" type="text" class="form-control">
                            <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
                            </div-->

                            <div class="form-group">
    <label for="x">Loại</label>
    <select class="form-control"  name="td_loai" id="exampleFormControlSelect1">
    <option  value=""></option>
      <option  value="Từ">Từ</option>
      <option  value="câu">Câu</option>
      <option  value="Cụm từ">Cụm từ</option>
      
    </select>
  </div>


                            <!--div class="form-group">
                            <label for="xxx">td_chude</label>
                            <input name="td_chude" type="text" class="form-control">
                            <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
                            </div-->

                            <div class="form-group">
    <label for="x">td_chude</label>
    <select name="td_chude"  class="form-control" id="exampleFormControlSelect1">
    <option  value=""></option>
      <option  value="1">Nail</option>
      <option  value="Cuộc sống">Cuộc sống</option>
      <option  value="Cơ bản">Cơ bản</option>
      
    </select>
  </div>

                            <div class="form-group">
                            <label for="xxx">td_creat</label>
                            <input name="td_creat" type="text" class="form-control " value="<?php echo date("Y-m-d h:i:s A"); ?>" readonly>
                            <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
                            </div>
                            <div class="form-group">
                            <label for="xxx">td_update</label>
                            <input name="td_update" type="text" class="form-control" readonly>
                            <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
                            </div>
                            <div class="form-group">
                            <label for="xxx">td_ta</label>
                            <input name="td_ta" type="text" class="form-control">
                            <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
                            </div>


                            
                            <button name="submit_data" type="submit" class="btn btn-sm btn-primary text-center">Submit And Return</button>
                        
                            <button name="submit_data_and_backhome" type="submit" class="btn btn-sm btn-primary mx-3">Submit Data And Backhome</button>
                            
                        
                        </form>
                    </table>




                </div>
                <!-- /.container-fluid -->



<div class="container text-center my-3 " >
    <a class="btn btn-light" href="index.php">Back Home</a>
    <button onclick=" window.history.back();" class="btn btn-primary" href="index.php">Back History  window.history.back();</button>


</div>

            </div>
            <!-- End of Main Content -->
```


# Update (edit)
update.php?id=td_id

```
<?php
$message = ""; // initial message 

// Includs database connection
// Database name
$database_name = "csdl_tudien.db";

// Database Connection
$db = new SQLite3($database_name);

// Create Table "bang_tudien" into Database if not exists 
// Tạo Bảng "bang_tudien" vào Cơ sở dữ liệu nếu không tồn tại
$query = "CREATE TABLE IF NOT EXISTS tbl_tudien (td_id INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL, td_tv STRING, td_ts STRING, td_mt STRING, td_loai STRING, td_chude STRING, td_creat STRING, td_update STRING, td_ta STRING)";
$db->exec($query);


// Updating the table row with submited data according to rowid once form is submited 
if (isset($_POST['submit_data'])) {
    
    
    // Gets the data from post
    //$id     = $_POST['id'];
   // $name   = $_POST['name'];
   // $email  = $_POST['email'];
   // $email2 = $_POST['email2'];
    $td_id = $_POST['td_id'];
    $td_tv = $_POST['td_tv'];
    $td_ts = $_POST['td_ts'];
    $td_mt = $_POST['td_mt'];

    $td_loai = $_POST['td_loai'];
    $td_chude = $_POST['td_chude'];
    $td_creat = $_POST['td_creat'];
    $td_update = $_POST['td_update'];
    $td_ta = $_POST['td_ta'];
    // Makes query with post data
    //$query = "UPDATE tbl_tudien set td_tv='$td_tv', td_ts='$td_ts', td_mt='$td_mt',    td_loai='$td_loai' , td_chude='$td_chude', td_creat='$td_creat', td_update='$td_update', td_ta='$td_ta'   WHERE td_id=$td_id";
    $query  = "UPDATE tbl_tudien set td_tv='$td_tv', td_ts='$td_ts', td_mt='$td_mt', td_loai='$td_loai' , td_chude='$td_chude', td_creat='$td_creat', td_update='$td_update', td_ta='$td_ta' WHERE rowid=$td_id";
    

    // Executes the query
    // If data inserted then set success message otherwise set error message
    // Here $db comes from "db_connection.php"
    if ($db->exec($query)) {
        $message = "<div class='alert alert-primary' role='alert'> Data is updated successfully. <a href='index.php' class='btn btn-primary'>Home Index</a></div>";
        //header("location:index.php");
    } else {
        $message = "Sorry, Data is not updated.";
    }
}

// submit_data_and_backhome
if (isset($_POST['submit_data_and_backhome'])) {
    
    // Gets the data from post
    //$id     = $_POST['id'];
   // $name   = $_POST['name'];
   // $email  = $_POST['email'];
   // $email2 = $_POST['email2'];
   $td_id = $_POST['td_id'];
   $td_tv = $_POST['td_tv'];
   $td_ts = $_POST['td_ts'];
   $td_mt = $_POST['td_mt'];

   $td_loai = $_POST['td_loai'];
   $td_chude = $_POST['td_chude'];
   $td_creat = $_POST['td_creat'];
   $td_update = $_POST['td_update'];
   $td_ta = $_POST['td_ta'];
   // Makes query with post data
   //$query = "UPDATE tbl_tudien set td_tv='$td_tv', td_ts='$td_ts', td_mt='$td_mt',    td_loai='$td_loai' , td_chude='$td_chude', td_creat='$td_creat', td_update='$td_update', td_ta='$td_ta'   WHERE td_id=$td_id";
   $query  = "UPDATE tbl_tudien set td_tv='$td_tv', td_ts='$td_ts', td_mt='$td_mt', td_loai='$td_loai' , td_chude='$td_chude', td_creat='$td_creat', td_update='$td_update', td_ta='$td_ta' WHERE rowid=$td_id";
   

   // Executes the query
   // If data inserted then set success message otherwise set error message
   // Here $db comes from "db_connection.php"
   if ($db->exec($query)) {
       $message = "<div class='alert alert-primary' role='alert'> Data is updated successfully. <a href='index.php' class='btn btn-primary'>Home Index</a></div>";
       header("location:index.php");
   } else {
       $message = "Sorry, Data is not updated.";
   }
}

$td_id     = $_GET['id']; // rowid from url
// Prepar the query to get the row data with rowid
$query  = "SELECT td_id, * FROM tbl_tudien WHERE td_id=$td_id";
$result = $db->query($query);
$data   = $result->fetchArray(); // set the row in $data
?>

                <!-- Begin Page Content -->
                <div class="container-fluid">

                    <!-- Page Heading -->
                    <h1 class="h3 mb-4 text-gray-800">edit Page</h1>


				         <table class="table table-responsive table-striped">
							<form action="" method="post">
							<input type="hidden" name="td_id" value="<?php
				echo $td_id;
				?>">
							<div class="form-group">
								<label for="xxx">td_tv</label>
								<input name="td_tv" type="text" value="<?php
				echo $data['td_tv'];
				?>" class="form-control">
							</div>
							<div class="form-group">
								<label for="xxx">td_ts</label>
								<input name="td_ts" type="text" value="<?php
				echo $data['td_ts'];
				?>" class="form-control">
							</div>
							<div class="form-group">
								<label for="xxx">td_mt</label>
								<textarea name="td_mt"   class="form-control alert alert-success" rows="7"><?php
				echo $data['td_mt'];
				?></textarea>
                            </div>

                            

                            <!--div class="form-group">
								<label for="xxx">td_loai</label>
								<textarea name="td_loai"   class="form-control alert alert-success" rows="7"><?php
				echo $data['td_loai'];
				?></textarea>
                            </div-->

                            <div class="form-group">
    <label for="x">Loại</label>
    <select class="form-control"  name="td_loai" id="exampleFormControlSelect1">
    <option  value="<?php echo $data['td_loai']; ?>"><?php echo $data['td_loai']; ?> - curent</option>
      <option  value="Từ">Từ</option>
      <option  value="câu">Câu</option>
      <option  value="Cụm từ">Cụm từ</option>
      
    </select>
  </div>



  <div class="form-group">
    <label for="x">td_chude</label>
    <select name="td_chude"  class="form-control" id="exampleFormControlSelect1">
    <option  value=""></option>
      <option  value="1">Nail</option>
      <option  value="Cuộc sống">Cuộc sống</option>
      <option  value="Cơ bản">Cơ bản</option>
      
    </select>
  </div>

                            </div>
                            <div class="form-group">
								<label for="xxx">td_creat</label>
								<input readonly name="td_creat"  value="<?php echo $data['td_creat']; ?>"  class="form-control alert alert-success">
                            </div>
                            <div class="form-group">
								<label for="xxx">td_update</label>
								<input name="td_update"   class="form-control alert alert-success" value="<?php echo date("Y-m-d h:i:s A"); ?>">
                            </div>
                            <div class="form-group">
								<label for="xxx">td_ta</label>
								<textarea name="td_ta"   class="form-control alert alert-success"><?php
				echo $data['td_ta'];
				?></textarea>
                            </div>



							<div class="form-group">
								
								<button name="submit_data" type="submit" class="btn btn-primary"/>Update data</button>
							</div>

							<div class="form-group">
								
								<button name="submit_data_and_backhome" type="submit" class="btn btn-primary"/>Update data and backhome</button>
							</div>
							</form>
						</table>


                </div>
                <!-- /.container-fluid -->

            
<div class="container text-center my-3 " >
    <a class="btn btn-light" href="index.php">Back Home</a>
    <button onclick=" window.history.back();" class="btn btn-primary" href="index.php">Back History  window.history.back();</button>


</div>
```


# Delete.php
url: delete.php?id=td_id

```
<?php

// Includs database connection
// Database name
$database_name = "csdl_tudien.db";

// Database Connection
$db = new SQLite3($database_name);

// Create Table "bang_tudien" into Database if not exists 
// Tạo Bảng "bang_tudien" vào Cơ sở dữ liệu nếu không tồn tại
$query = "CREATE TABLE IF NOT EXISTS tbl_tudien (td_id INTEGER PRIMARY KEY AUTOINCREMENT NOT NULL, td_tv STRING, td_ts STRING, td_mt STRING, td_loai STRING, td_chude STRING, td_creat STRING, td_update STRING, td_ta STRING)";
$db->exec($query);

//
$id = $_GET['id']; // rowid from url

// Prepar the deleting query according to rowid
$query = "DELETE FROM tbl_tudien WHERE td_id=$id";

// Run the query to delete record
if( $db->query($query) ){
	$message = "Record is deleted successfully.";
    
    header('Location: index.php');
exit;
}else {
	$message = "Sorry, Record is not deleted.";
}

echo $message;
?>



	
<div class="container">
<a href="index.php" class="btn btn-primary aligin-right">Back to Home</a>
</div>

<div class="container">
<a href="list.php" class="btn btn-primary d-flex p-2">Back to List</a>
</div>

?>
```

# List.php
list item


# Datatable.php
using datatablejs datatable.net

# Search.php
search.php?s=
- td_tv
- td_ts

```

```

# View.php
view.php?id=td_id
