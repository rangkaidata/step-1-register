# Step-1-register
source code untuk membuat akun baru atau register akun.

![Register-User](https://github.com/rangkaidata/step-1-register/blob/master/register.png)
*Gambar 1. Register User.*

Langkah pertama dalam membuat aplikasi apapun yang menggunakan banyak user adalah dengan membuat register user. Dengan tujuan agar setiap user memiliki ruang tersendiri dalam worksheet masing-masing dan tidak tercampur dengan data worksheet user lain. Register User menggunakan User Name, Full Name, dan Password untuk ID di server dan membuat folder baru untuk User Baru. 

Langkah pertama untuk membuat form Register User adalah membuat script htmlnya.
1. Buatlah file baru dengan text editor seperti Notepad di windows atau Nano di Linux.
2. Kopi script berikut, kemudian simpan dengan nama register.html.
3. Kemudian bukalah file tersebut denga Browser seperti Chrome, Firefox atau Internet Explorer.

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="description" content="Software Akuntansi Online">
    <meta name="keywords" content="HTML, CSS, JavaScript, Accounting, Akuntansi, Tutorial, Online, Software, Aplikasi, Web">
    <meta name="author" content="Budiono">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Akuntansi Online - Rangkaidata.com</title>
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
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="description" content="Software Akuntansi Online">
    <meta name="keywords" content="HTML, CSS, JavaScript, Accounting, Akuntansi, Tutorial, Online, Software, Aplikasi, Web">
    <meta name="author" content="Budiono">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Akuntansi Online - Rangkaidata.com</title>
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
Refresh browser dengan tombol F5. Akan tampil form seperti gambar diatas.

Langkah selanjutnya adalah memasukkan kode javascript di dalam sintax <script></script>.

### Step 1.1. Deklarasi Variable.

```javascript
<script>
	var msg=document.getElementById("msg");
	var user_name=document.getElementById("user_name");
	var user_fullname=document.getElementById("user_fullname");
	var user_password=document.getElementById("user_password");
	var confirm_password=document.getElementById("confirm_password");
	var passcode_image=document.getElementById("passcode_image");
	var user_passcode=document.getElementById("user_passcode");
	var button_register=document.getElementById("button_register");

</script>
```

### Step 1.2. Fokus di Input Text User Name.
```javascript
	user_name.focus();
```

### Step 1.3. Fungsi Ketika Tombol Register di Klik.
```javascript
	button_register.onclick=function(){
		// kode ketika diklik.
	}
```
### Step 1.3.1. Membaca Nilai Tombol.
Bila nilai tombol adalah Reset, maka program akan memanggil ulang halaman untuk refresh. Bila nilai tombol adalah Register, maka lanjutkan baris berikutnya.
```javascript
	if (button_register.innerHTML === "Reset"){
		location.replace(location.href);
	}
```
### Step 1.3.2. Masukkan Nilai Input ke Dalam Variabel obj.
Masukkan semua variable yang telah diinput dilayar kedalam variable obj. 
```javascript
	const obj = {
		"home_folder":null,
		"user_name":user_name.value,
		"user_fullname":user_fullname.value,
		"user_password":user_password.value,
		"confirm_password":confirm_password.value,
		"user_passcode":user_passcode.value
	};
```
### Step 1.3.3. Deklarasi XHR.
XHR adalah XML HTTP Request, yaitu fungsi yang telah disediakan oleh javascript untuk mengirim data dan permintaan ke server sekaligus memberikan umpan balik atau respon balik ke client user. Disini fungsi XHR diinstansikan dengan nama request, sedangkan data inputan di format konversi ke bentuk JSON lalu dimasukan ke variabel dbParam.
```javascript		
	var request = new XMLHttpRequest();
	var dbParam = JSON.stringify(obj);
```
### Step 1.3.4. Onload Adalah Fungsi Ketika XHR Mengirim ke Server
Ketika XHR dikirim keserver, dengan segera klien bisa memeriksa status pengiriman di onload.
```javascript
	request.onload = function() {
	}
```
### Step 1.3.4.1. Memeriksa Data Masuk.
Bila data dari server telah siap, yaitu dengan nilai readyState=4
```javascript
	if (request.readyState===4){
		...
	} 
```
### Step 1.3.4.1.1. Deklarasi Variabel Untuk Data.
Selanjutnya memasukkan paket data yang telah diterima kedalam variable. Dimana data tersebut dikonversi ke array javascript.
```javascript
	var paket = JSON.parse(request.responseText);
```
### Step 1.3.4.1.2. Kirim ke Fungsi.
Paket data yang telah diterima, dan sudah dikonversi ke javascript selanjutnya dikirim ke fungsi terimaData, untuk diproses di klien.
```javascript
	terimaData(paket);
```
### Step 1.3.4.2. Bila Terjadi Error.
Bila terjadi error saat kirim data ke server, tampilkan dikonsol browser untuk diperiksa.
```javascript
	else {
		console.log('Network request failed with response ' + request.status + ': ' + request.statusText)
	}
```
### Step 1.3.5. Mengirim Data Ke Server.
Data dikirim ke server dengan link https://datablok.id/v0/register/create.php, dan juga parameternya seperti dbParam.
```javascript
	request.open('POST', 'https://datablok.id/v0/register/create.php');
	request.setRequestHeader('Content-type', 'application/x-www-form-urlencoded');
	request.send(dbParam);
```
### Step 1.4. Fungsi Untuk Membaca Paket Data.
Paket Data dari server telah siap, dan diolah di sisi klien. Yaitu memeriksa apakah responnya baik atau tidak. bila nilai responnya 0, proses data tersebut telah berhasil membuat user baru diserver. Namun bila bukan 0, maka terjadi kesalahan. Untuk menampilkan pesan kesalahan atau keberhasilan maka paket.msg ditampilkan ke layar.
```javascript
	function terimaData(paket){
		if (paket.err==0){
			button_register.innerHTML = "Reset";
		}
		msg.innerHTML = "Message: "+paket.msg;
	}
```

Setelah script javascript dimasukkan, maka form pertama untuk Register User telah selesai. Dengan Form tersebut user bisa membuat User Baru dan mendaftarkan user tersebut di server datablok.id, dimana server tersebut akan membuat ruang baru untuk user yang digunakan untuk memasukkan data data, mengedit data, dan menghapus data. User tersebut akan menjadi administrator, dan bisa koneksi (Join) ke folder user lain, dengan modul Join User yang akan dijelaskan di step-13. 


Selamat Mencoba.

