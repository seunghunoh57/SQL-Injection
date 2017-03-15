# SQL-Injection

This program will generate a password that bypasses a PHP script using raw md5 encryption for its password.


#### DO NOT THIS PROGRAM IN ANY MALICIOUS INTENT OR IN ANY REAL-LIFE SITUATIONS.


## How it works
Below is a sample PHP script that this program takes advantage of:

```php
if (isset($_POST['username']) and isset($_POST['password']))
{
	$username = mysql_real_escape_string($_POST['username']);
	$password = md5($_POST['password'], true);
	$sql_s = "SELECT * FROM users WHERE username='$username' and pw='$password'";
	$rs = mysql_query($sql_s);
	if (mysql_num_rows($rs) > 0) {
		echo "Login successful!";
	} else {
		echo "Incorrect username or password";
	}
}
```

This type of PHP script uses an MD5 hash to encrypt the password before inputting it into the SQL query. Note we can take advantage of the fact that the MD5 hash is done like so: ```php $password = md5($_POST['password'], true);```. This hash inputs a raw binary input into the password query, implying there is a possibility of special characters that can be interpreted as SQL commands, i.e. ```=```, ```'```. Also, note that in MySQL, when two binary inputs are compared against each other, it returns ```TRUE```, since ```FALSE = FALSE``` is ```TRUE```.

Knowing all this means that all we have to do is create a random input into the MD5 hash such that it returns a raw binary input that includes ``` '=' ```.

The Python script generates such a random input by putting together a randomly generated integer and finding its hash, repeating this process until its MD5 hash includes ```'='```


## Note
On average, the program should take anywhere from a few seconds to a couple minutes.
For more information, feel free to contact me!




###### This program is written in Python and takes use of the PyMD5 library (included in the file).
