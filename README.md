<?php
    $email = @$_POST['email'];
    $pass = @$_POST['pass'];
    $login = @$_POST['login'];

    if ($login) {
      if($email == "" || $pass == ""){
            ?> <script type="text/javascript">alert("Email / Password tidak boleh kosong");</script> <?php
        } else {
          $sql = mysql_query("select * from user where email = '$email' and password = md5('$pass')") or die (mysql_error());
          $data = mysql_fetch_array($sql);
          $cek = mysql_num_rows($sql);
        if($cek >= 1) {
        } else {
            ?> <script type="text/javascript">alert("Email / Password Belum Terdaftar");</script> <?php
        }
            if($data['level'] == "Investor") {
                @$_SESSION['investor'] = $data['id'];
            header('location: marketin.php');
            } else if($data['level'] == "Admin") {
                @$_SESSION['admin'] = $data['id'];
            header('location: user/admin.html');
             } else if($data['level'] == "Peternak") {
                @$_SESSION['admin'] = $data['id'];
            header('location: datap.php');
             }
          }
        }
  ?>  
