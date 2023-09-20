Link Adaptable [Adaptable](https://xpnse.adaptable.app/ "Tugas 2 PBP"). 

# TUGAS 2
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

![bagan](image.png)

<h3>C.</h3> 

Virtual environment digunakan untuk mengisolasi lingkungan proyek agar tidak bertabrakan dengan proyek lain yang berbeda versi. Jika kita tidak menggunakan virtual environment kita masih tetap dapat membuat aplikasi web berbasis Django. Namun, kemungkinan error akan besar karena versi paket atau dependensi antar proyek belum tentu sama meskipun modulnya sama. 

sumber: https://stackoverflow.com/a/44392668

<h3>D.</h3> 

MVT, MVC, dan MVVM ketiganya merupakan pola desain arsitektur untuk pengembangan aplikasi. MVC atau model view controller merupakan pola desain. MVC terbagi menjadi tiga yaitu Model untuk mengatur logika bisnis, View untuk menampilkan data, dan Controller untuk menghubungkan model dan view. MVT atau model view template merupakan variasi dari pola desain MVC yang digunakan dalam framework Django. Perlu diketahui bahwa view di MVT dan di MVC berbeda. View pada MVT ekuivalen dengan controller pada MVC. MVVM atau Model View View Model adalah pengembangan dari MVC. Model MVC ini menyelesaikan kekurangan pada model MVC yaitu dengan membuat separasi jelas antara business logic dan data presentation logic. 

Sumber:
https://www.geeksforgeeks.org/difference-between-mvc-mvp-and-mvvm-architecture-pattern-in-android/


# TUGAS 3
###	 Apa perbedaan antara form POST dan form GET dalam Django?
Form post lebih secure daripada form get. Ketika menggunakan method get, request parameter di append ke URL. Hal ini membuat data sensitive terekspos, dan penyerang dapat dengan mudah mendapatkan data sensitif tersebut. Sedangkan ketika kita menggunakan method POST, request parameter tidak di append ke URL melainkan disimpan pada body HTTP request. Selain itu, parameter yang dapat dikirm method GET terbatas karena request parameter di append ke URL. Namun, method GET masih sering digunakan karena lebih cepat dan lebih simple daripada POST. Secara konvensi, method GET digunakan ketika meminta request sedangkan POST digunakan ketika mengirim request.
Sumber: https://www.geeksforgeeks.org/difference-between-http-get-and-post-methods/

###	 Apa perbedaan utama antara XML, JSON, dan HTML dalam konteks pengiriman data?
XML dan HTML keduanya merupakan markup language, perbedaannya XML didesain untuk pegiriman data sedangkan HTML digunakan untuk memformat dan menampilkan data. JSON dan XML keduanya digunakan untuk pengiriman data, perbedaannya XML menggunakan struktur tag untuk merepresentasikan data, sedangkan JSON menggunakan key value pair.

###	Mengapa JSON sering digunakan dalam pertukaran data antara aplikasi web modern?
JSON sering digunakan karena human dan machine readable. untuk informasi yang sama JSON mengirimkan data yang lebih sedikit dibandingkan dengan XML, karena JSON tidak menggunakan struktur tag. selain itu mayoritas bahasa pemrograman saat ini sudah menyediakan dukungan bawaan untuk mengurai dan menghasilkan data dalam format JSON. JavaScript, yang digunakan dalam sebagian besar aplikasi web, memiliki kemampuan yang mudah untuk mengurai data JSON serta menghasilkannya kembali.
###	 Jelaskan bagaimana cara kamu mengimplementasikan checklist di atas secara step-by-step (bukan hanya sekadar mengikuti tutorial).
1.	 **Membuat input form untuk menambahkan objek model pada app sebelumnya**.
-	Sebelum membuat file form.py saya menambahkan item baru yaitu item date_added. Kemudian Saya melakukan migrasi model.
-	Pertama saya membuat file form.py, fields pada form.py diisi dengan item yang dideklarasikan pada class product model.
-	Kemudian saya membuat fungsi create_item pada file views.py di main. Fungsi ini digunakan untuk menangani permintaan pembuatan item baru dan memvalidasi form.
-	Buat file create_item.html untuk dirender oleh fungsi create_item
-	Setelah itu, tambahkan button create_item pada file main.html untuk menampilkan file create_item.html dengan cara melakukan routing URL
2.	 **Tambahkan 5 fungsi views untuk melihat objek yang sudah ditambahkan dalam format HTML, XML, JSON, XML by ID, dan JSON by ID.**
-	Untuk HTML disini saya membuat halaman page baru yaitu show-detail. Pertama saya membuat file HTML, data yang disimpan diperlihatkan dalam bentuk table pada kolom yang sesuai yaitu name, amount, price, description, dan date added.
-	Setelah membuat HTML show-detail saya membuat fungsi show detail di views.py dengan menambahkan context item yang didapatkan dari Item.objects.all()
-	Setelah itu saya menambahkan button detail pada file main.html dan melakukan routing URL untuk show-detail.
-	kemudian, saya membuat Fungsi XML, JSON, XML by ID, dan JSON by ID. Untuk membuat fungsi-fungsi ini saya menggunakan serializer untuk menerjemahkan data pada database ke format XML dan JSON, untuk XML by ID dan JSON by ID kita perlu menerapkan filter mengambil data yang memiliki nilai id yang sama dengan primary key.
3.	 **Membuat routing URL untuk masing-masing views yang telah ditambahkan pada poin 2.**
-	Routing dilakukan dengan menambahkan path pada file url.py, path tersebut adalah sebagai berikut:
```
    path('xml/', show_xml, name='show_xml'), 
    path('json/', show_json, name='show_json'),
    path('xml/<int:id>/', show_xml_by_id, name='show_xml_by_id'),
    path('json/<int:id>/', show_json_by_id, name='show_json_by_id'),

```
ketika URL cocok dengan pola maka akan memanggil fungsi yang sesuai.

### Mengakses kelima URL di poin 2 menggunakan Postman
* **JSON**
![JSON postman](JSON_postman.png)

* **XML**
![XML postman](XML_postman.png)

* **JSON by ID**
![JSON by ID postman](JSON_byID_postman.png)

* **XML by ID**
![XML by ID postman](XML_byID_postman.png)





