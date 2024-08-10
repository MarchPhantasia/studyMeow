# upload - easy

## 源码

``` php
<?php

error_reporting(0);

header("Content-type: text/html;charset=utf-8");
//设置上传目录
define("UPLOAD_PATH", dirname(__FILE__) . "/upload/");
define("UPLOAD_URL_PATH", str_replace($_SERVER['DOCUMENT_ROOT'], "", UPLOAD_PATH));

if (!file_exists(UPLOAD_PATH)) {
    mkdir(UPLOAD_PATH, 0755);
}


?>
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>文件上传 - 无限制</title>
    <script src="https://cdn.jsdelivr.net/npm/jquery@3.7.1/dist/jquery.min.js"></script>
    <link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/npm/fomantic-ui@2.9.3/dist/semantic.min.css">
    <script src="https://cdn.jsdelivr.net/npm/fomantic-ui@2.9.3/dist/semantic.min.js"></script>
</head>
<body>
    <div class="ui center aligned container" style="position:relative;top:50px">
    <h1 class="ui header">文件上传 - 无限制</h1>
    <form class="ui success form" action="" method="post" enctype="multipart/form-data">
    <div class="ui file input" style="width: 45%;margin: 0 auto">
        <input type="file" name="file" id="file" />
    </div>
    <?php
        if (!empty($_POST['submit'])) {
            if (!$_FILES['file']['size']) {
                echo "<script>alert('请添加上传文件')</script>";
            } else {
                $name = basename($_FILES['file']['name']);
                if (move_uploaded_file($_FILES['file']['tmp_name'], UPLOAD_PATH . $name)) {
                    echo '<div class="ui success message" style="width: 45%;margin: 10px auto;margin-bottom: 0">';
                    echo '<div class="header">上传成功</div>';
                    echo "<p>上传文件相对路径:" . UPLOAD_URL_PATH . $name . "</p>";
                    echo "</div>";
                } else {
                    echo "<script>alert('上传失败')</script>";
                }
            }
        }
    ?>
    <div>
    <input class="ui button" type="submit" name="submit" value="Submit" style="margin-top: 10px;"/>
    </div>
    </form>

    </div>
</body>
</html>

```
