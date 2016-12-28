# form-validation-trial-4th-year
<!DOCTYPE HTML>
<html> 
<head>
<style>
.error {color: #FF0000;}
.mid{margin-right: 80px; margin-left: 80px;}
	.small{width:50px;}
	.comp{width:120px;}
</style>
</head>
<body>
<?php
// define variables with empty values

$title = $name = $company = $email = $phone = $customer = "";
$titleErr = $nameErr = $emailErr = "";

//data validation

if ($_SERVER["REQUEST_METHOD"] == "POST") {
  //check title field
  if (empty($_POST["title"])) {
    $titleErr = "This field is required";
  } else {
    $title = test_input($_POST["title"]);
  }
  if (empty($_POST["name"])){
    $nameErr = "This field is required";
  } else {
    $name = test_input($_POST["name"]);
    // check if name only contains letters and whitespace
    if (!preg_match("/^[a-zA-Z ]*$/",$name)) {
      $nameErr = "Only letters and white space allowed";
    }

  }

  if (empty($_POST["email"])) {
    $emailErr = "This field is required";
  } else {
    $email = test_input($_POST["email"]);
    // check if e-mail address is formed properly
    if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
      $emailErr = "Invalid email format"; 
    }
  }

  $company = test_input($_POST["company"]);
  $phone = test_input($_POST["phone"]);
  $customer = test_input($_POST["customer"]);

}
function test_input($data) {
  $data = trim($data);
  $data = stripslashes($data);
  $data = htmlspecialchars($data);
  return $data;
}
?>
<div class="mid"><header><h1>Event Registeration</h1><h5>Fill out the form to register for our event</h5>
</header>
<form method="post" action="<?php echo htmlspecialchars($_SERVER["PHP_SELF"]);?>">
<div class="col-md-12">
Title <span class="error"> * <?php echo $titleErr;?></span>
	<textarea name="title" rows="1" cols="30" style="margin-left:20px"></textarea>
<br><br>
<div class="row">
<label for="name">Name</label> <span class="error"> * <?php echo $nameErr;?></span>
<input type="text" class="comp" id="name"style="margin-left:12px"size="10"></input>
<input type="text" id="name"style="margin-left:2px"size="15"></input>
</div><br>
Company <input type="text" name="company"style="margin-left:2px" size="31"><br><br>
E-mail <span class="error"> * <?php echo $emailErr;?></span>
<input type="text" name="email" placeholder="ex: myname@example.com"style="margin-left:8px" size="31"><br><br>
<div class="row">
<label for="phone">Phone <br> Number</label>
	<input type="tel" id="phone" pattern="[\+]\d{2}]" class="small" size="2" maxlength="2"style="margin-left:11px">
	<b>-</b>
	<input type="tel" id="phone" pattern="\d{10}" class="comp"size="10" maxlength="10">
</div><br>

Are you an existing customer? <br><br>
<input type="radio" name="customer"<?php if(isset($customer) && $customer=="exist")echo "checked";?>  value="exist" > Yes
<input type="radio" name="customer"<?php if(isset($customer) && $customer=="new")echo "checked";?> value="new" > No <br><br>
<input type='submit' name='register' value='Register'/>
</div></form></div>
</body>
</html>
