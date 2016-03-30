# Ins-Del-Up-Email


Add
<?php
$host = mysql_connect('localhost','root','');
$db = mysql_select_db('reg');

if(isset($_REQUEST['submit'])){
	$name = $_POST['name'];
	$mob = $_POST['mob'];
	$uname = $_POST['uname'];
	$pass = $_POST['pass'];
	
	$query = 'insert into registration (name,mob,uname,pass) values("'.$name.'","'.$mob.'","'.$uname.'","'.$pass.'")';
	if(mysql_query($query))
	{
		header('location:login.php'); }
		else{
		header('location:add.php');	
			}
	}

?>
<script>
  
  // When the browser is ready...
  $(function() {
  
    // Setup form validation on the #register-form element
    $("#register-form").validate({
    
        // Specify the validation rules
        rules: {
            name: "required",
            mob: "required",
            uname: "required",
            pass: {
                required: true,
                minlength: 5
            }
        },
        
        // Specify the validation error messages
        messages: {
            name: "Please enter your name",
            mob: "Please enter your mob no",
            uname: "Please enter a valid username",
            pass: {
                required: "Please provide a password",
                minlength: "Your password must be at least 5 characters long"
            }
        },
        
        submitHandler: function(form) {
            form.submit();
        }
    });

  });
  
  </script>
Login
<?php
$host = mysql_connect('localhost','root','');
$db = mysql_select_db('reg');
 
 if(isset($_REQUEST['submit'])){
	 $uname = $_POST['uname'];
	 $pass = $_POST['pass'];

 $query = mysql_query("select * from registration where uname='$uname' and pass='$pass'");
 $row = mysql_num_rows($query);
 
 if($row > 0){
	 session_start();
	 $_SESSION['uname'] =$uname;
	 header('location:view.php');
	 }else{
	 echo "<script> alert('plz currect username & password');</script>";	 
		 }	 
	 }
?>

View

<?php
session_start();

if ($_SESSION["uname"]) {
    echo "";
} else {
    header('location:login.php');
}
?>
<?php
$host = mysql_connect('localhost','root','');
$db = mysql_select_db('reg');

$uname = $_SESSION['uname'];
$query = "select * from registration"; 
$q= mysql_query($query) or die("Query problem");

echo "<table align=center border=15>
	<tr>
	<td>Name</td>
	<td>Mob</td>
	<td>Uname</td>
	<td>Pass</td>
	<td>Delete</td>
	<td>Edit</td>
	</tr>";

 while($data = mysql_fetch_array($q)) {
	
	//extract($data);
	echo "<tr>";
	echo "<td>" .$data['name']. "</td>";
	echo "<td>" .$data['mob']. "</td>";
	echo "<td>" .$data['uname']."</td>";
	echo "<td>" .$data['pass']. "</td>";
	
	?>
	<td><a href="delete.php?id=<?php echo $data['id']; ?>"> Delete </a></td>
    <td><a href="edit.php?id=<?php echo $data['id']; ?>"> Edit </a></td>

    <?php
}
?>	

Edit

<?php
	session_start();
	if ($_SESSION["uname"]) {
		echo "";
	} else {
		header('location:login.php');
	}
	?>



<?php
	$host = mysql_connect('localhost', 'root', '') or die("Connection error");
	$db = mysql_select_db('reg') or die('database error');
	$id = $_REQUEST['id'];


	$query = "select * from registration where id=" . $id;
	$res = mysql_query($query);
	$row = mysql_fetch_assoc($res);
	



		if (isset($_REQUEST['submit'])) {
			$id = $_POST['id'];
			$name = $_POST['name'];
			$mob = $_POST['mob'];
			$uname = $_POST['uname'];
			$pass = $_POST['pass'];
			
		
	
		$query = 'update registration set name="' . $name . '",mob="' . $mob . '",uname="' . $uname . '",pass="' . $pass . '" where id=' . $id;
	
		if (mysql_query($query)) {
			header("Location:view.php");
		}
	}
?>

Delete

<?php

if($_SESSION['uname']){
	echo "";
	}else{
	header('location:login.php');	
		}
?>

<?php
    
	$host=mysql_connect('localhost','root','') or die ("Connection error");
	$db=mysql_select_db('reg') or die ('database error');
	
	$id=$_REQUEST['id'];
	
	$query="delete from registration where id='".$id."'";
	$q=mysql_query($query) or die ("Query problem");
	
	if($q==1)
	{
			header("Location:view.php");
	}
	
?>
$(document).ready(function(){
    $("p").click(function(){
        $(this).hide();
    });
});

document.getElementById("demo").innerHTML = "Hello Dolly.";
