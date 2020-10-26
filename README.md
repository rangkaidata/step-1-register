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
<form> ... disini form inputan ... </form>
<script> /* disini script javascript */ </script>

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

Langkah selanjutnya adalah memasukkan kode javascript di dalam sintax <script></script>.

```javascript
	<script>
	// step-1: register
	// step-1: 1. deklarasi tiap element html untuk diambil isi dari object tersebut.
	var msg=document.getElementById("msg");
	var user_name=document.getElementById("user_name");
	var user_fullname=document.getElementById("user_fullname");
	var user_password=document.getElementById("user_password");
	var confirm_password=document.getElementById("confirm_password");
	var passcode_image=document.getElementById("passcode_image");
	var user_passcode=document.getElementById("user_passcode");
	var button_register=document.getElementById("button_register");
	
	// step-1: 2. fokus ditext user_name 
	user_name.focus();
	
	// step-1: 3. fungsi untuk tombol register, ketika di klik.
	button_register.onclick=function(){
		
		// step-1: 3.1. bila tombol adalah reset, maka panggil ulang halaman
		if (button_register.innerHTML === "Reset"){
			location.replace(location.href);
		}
		
		// step-1: 3.2. variable untuk data input
		const obj = {
			"home_folder":null,
			"user_name":user_name.value,
			"user_fullname":user_fullname.value,
			"user_password":user_password.value,
			"confirm_password":confirm_password.value,
			"user_passcode":user_passcode.value
		};
		
		// step-1: 3.3. deklarasi XHR untuk mengambil data dari server. 
		//    deklarasi dbParam untuk menyimpan nilai input dan konversi ke format JSON
		var request = new XMLHttpRequest();
		var dbParam = JSON.stringify(obj);

		// step-1: 3.4. fungsi ketika XHR di dimulai, atau terima respon server.
		request.onload = function() {
			
			// step-1: 3.4.1. bila data dari server telah siap, yaitu dengan readyState=4
			if (request.readyState===4){
				
				// step-1: 3.4.1.1. deklarasi variable paket, untuk tempat dari yang diterima dari server
				var paket = JSON.parse(request.responseText);
				
				// step-1: 3.4.1.2. kirim paket data ke fungsi terimaData, untuk diproses selanjutnya
				terimaData(paket);
			} 
			
			// step-1: 3.4.2. bila terjadi error saat kirim data ke server
			else {
				console.log('Network request failed with response ' + request.status + ': ' + request.statusText)
			}
		};
		
		// step-1: 3.5. kirim data register user administrator ke server.
		request.open('POST', 'https://datablok.id/v0/register/create.php');
		request.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
		request.send(dbParam);
	}
	
	// step-1: 4. fungsi untuk merangkai data dari server.
	function terimaData(paket){
		
		// step-1: 4.1. bila error tidak ada atau 0, ganti tombol menjadi reset.
		if (paket.err==0){
			button_register.innerHTML = "Reset";
		}
		
		// step-1: 4.2. tampilkan pesan yang diterima dari server ke user.
		msg.innerHTML = "Message: "+paket.msg;
	}
	
	// step-1: 5. selesai
	</script>
```
Setelah script javascript dimasukkan, maka form pertama untuk Register User telah selesai. Dengan Form tersebut user bisa membuat User Baru dan mendaftarkan user tersebut di server datablok.id, dimana server tersebut akan membuat ruang baru untuk user yang digunakan untuk memasukkan data data, mengedit data, dan menghapus data. User tersebut akan menjadi administrator, dan bisa koneksi (Join) ke folder user lain, dengan modul Join User yang akan dijelaskan di step-13. 

Penjelasan Javascriptnya adalah sebagai berikut:

