# step-1-register
source code untuk membuat akun baru atau register akun.

![Register-User](https://github.com/rangkaidata/step-1-register/blob/master/register.png)
*Gambar 1. Register User.*

Langkah pertama dalam membuat aplikasi apapun yang menggunakan banyak user adalah dengan membuat register user. Dengan tujuan agar setiap user memiliki ruang tersendiri dalam worksheet masing-masing dan tidak tercampur dengan data worksheet user lain. Register User menggunakan User Name, Full Name, dan Password untuk ID di server dan membuat folder baru untuk User Baru. 

Langkah pertama untuk membuat form Register User adalah membuat script htmlnya.
1. Buatlah file di text editor seperti Notepad di windows atau Nano di Linux.
2. Kopi script berikut, kemudian simpan dengan nama register.html.
3. Kemudian bukalah file tersebut denga Browser seperti Chrome, Firefox atau Internet Explorer.

```
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Page Title</title>
</head>
<body>

</body>
</html> 
```
Setelah membuat script HTMLnya, langkah selanjutnya adalah membentuk form sesuai dengan format input data yang diminta oleh server. Tambahlah kode HTML diatas dengan form menjadi seperti berikut:

```
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Page Title</title>
</head>
<body>

<form>
	<h1>Register Akun Baru</h1>
	<ul>
	<li><h4 id="msg"></h4></li>
	<li>
		<label for="user_name">User Name:</label>
		<input type="text" id="user_name">
	</li>
	<li>
		<label for="user_fullname">Full Name:</label>
		<input type="text" id="user_fullname">
	</li>
	<li>
		<label for="user_password">Password:</label>
		<input type="password" id="user_password">
	</li>
	<li>
		<label for="confirm_password">Confirm Password:</label>
		<input type="password" id="confirm_password">
	</li>
	<li>
		<label for="passcode_image">Passcode:</label>
		<img src="https:\\datablok.id\v0\passcode\xyzimg.php" id="passcode_image" border=1>
	</li>
	<li>	
		<label for="user_passcode">Retype Passcode:</label>
		<input type="text" id="user_passcode">
	</li>
	<li>
		<button type="button" id="button_register">Register</button>
	</li>
	</ul>
</form>

</body>
</html> 
```
Refresh browser dengan tmbol F5. Akan tampil form seperti gambar diatas.

Langkah selanjutnya adalah memasukkan kode javascript di dalam sintax <script></script>
