link Adaptable: 

pertanyaan:
A. Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step (bukan hanya sekadar mengikuti tutorial).

B. Buatlah bagan yang berisi request client ke web aplikasi berbasis Django beserta responnya dan jelaskan pada bagan tersebut kaitan antara urls.py, views.py, models.py, dan berkas html.

C. Jelaskan mengapa kita menggunakan virtual environment? Apakah kita tetap dapat membuat aplikasi web berbasis Django tanpa menggunakan virtual environment?

D. Jelaskan apakah itu MVC, MVT, MVVM dan perbedaan dari ketiganya.

Jawab:

<h3>A.</h3> 

1. **Membuat sebuah proyek Django baru.**

Sebelumnya saya buat terlebih dahulu direktori untuk proyek baru Bernama Tugas2PBP. Kemudian saya inisiasi git dan menghubungkannya ke github dengan add, commit, dan push. lalu membuat file .gitignore. kemudian membuat dan mengkatifkan virtual environment menggunakan command:

`python -m venv env`

`env\Scripts\activate.bat`

virtual environment memungkinkan suatu mesin untuk memiliki versi python yang berbeda untuk tiap proyek tanpa menimbulkan error. Dengan virtual environment tiap proyek dapat menginstall dependensi dengan versi yang berbeda-beda.  
selanjutnya saya menginstall dependencies yang dibutuhkan untuk proyek ini menggunakan command:

`pip install -r requirements.txt`

pip merupakan sistem manajemen paket yang berfungsi untuk meng-install dan mengelola paket dalam proyek python. Disini saya menginstall dependencies yang tertera pada file requirements.txt
Kemudian saya membuat project Django baru menggunakan command:

`django-admin startproject Inventory .`


2. **Membuat aplikasi dengan nama main pada proyek tersebut.**

Aplikasi dengan nama main saya buat dengan menjalankan command berikut:
python manage.py startapp main
aplikasi main kemudian saya daftarkan ke list INSTALLED_APPS di file settings.py. ini dilakukan agar proyek Django dapat mengenali app main.

3. **Melakukan routing pada proyek agar dapat menjalankan aplikasi main.**

file urls.py yang berada di direktori Inventory (proyek) saya ubah isinya menjadi sebagai berikut:

```
urlpatterns = [
    path('', include('main.urls')),
]
```

Disini rute fungsi path adalah  ‘ ’ yang berarti direktori saat ini. Sehingga direktori root akan menampilkan app main.

4. **Membuat model pada aplikasi main dengan nama Item dan memiliki atribut wajib sebagai berikut.**
•	name sebagai nama item dengan tipe CharField.
•	amount sebagai jumlah item dengan tipe IntegerField.
•	description sebagai deskripsi item dengan tipe TextField.
Model dibuat dengan mengakses ke file models.py di direktori main, di file models.py saya buat Model dengan nama Item dan memberikan atribut sebagai berikut:
```
class Item(models.Model):
    name = models.CharField(max_length=255)
    amount = models.IntegerField()
    description = models.TextField()
    price = models.IntegerField()
```
Terdapat atribut baru yang saya tambahkan yaitu price. Atribut ini akan digunakan nanti untuk tema kecil saya.

5. **Membuat sebuah fungsi pada views.py untuk dikembalikan ke dalam sebuah template HTML yang menampilkan nama aplikasi serta nama dan kelas kamu.**

Pada file views.py saya membuat fungsi show_main dengan paramenter request. Lalu saya  menambahkan context yaitu name dan class dengan value nama saya (Muhammad Iqbal) dan kelas saya (PBP A). kemudian saya return render(request, "main.html", context). 
Fungsi render disini adalah fungsi yang digunakan untuk merender sebuah halaman HTML yang akan dikirmkan ke website pengguna. Argumen request adalah permintaan yang diterima oleh server. “main.html” adalah nama template yang digunakan untuk menghasilkan halaman HTML. Dictionary context adlaah data yang akan dikirimkan ke tampilan.
Setelah itu , di files main.html pada subdirektori templates saya menuliskan kode HTML sebagai berikut:
```
<h1>Pengelolaan Pengeluaran Keuangan</h1>
<h5>Name: </h5>
<p>{{ name }}<p>
<h5>Class: </h5>
<p>{{ class }}<p>
```
“ {{ }} “ merupakan syntax HTML untuk variabel. Variabel ini didapatkan dari context yang berada di file views.py.

6. **Membuat sebuah routing pada urls.py aplikasi main untuk memetakan fungsi yang telah dibuat pada views.py.**
```
urlpatterns = [
    path('', show_main, name='show_main'),
]
```

7. **Melakukan deployment ke Adaptable terhadap aplikasi yang sudah dibuat sehingga nantinya dapat diakses oleh teman-temanmu melalui Internet.**

Deployment ke adaptable dilakukan sama seperti pada tutorial 0. 

8. **Membuat sebuah README.md yang berisi tautan menuju aplikasi Adaptable yang sudah di-deploy, serta jawaban dari beberapa pertanyaan berikut.**

Referensi:
https://stackoverflow.com/questions/39055728/importance-of-virtual-environment-setup-for-django-with-python


<h3>B.</h3> 

<h3>C.</h3> 

<h3>D.</h3> 