# Jarkom_Modul2_Lapres_C02
Laporan Resmi Modul 2 Praktikum Jaringan Komputer
## Kelompok C02
* Aulia Ihza Hendradi (05111840000089)
* Excel Deo Cornelius (05111840000117)
## Topologi
![topo](https://user-images.githubusercontent.com/52096462/99184822-57f27b80-2778-11eb-84eb-d6c4fc190a0c.PNG)
## Setting DNS
![setingdns](https://user-images.githubusercontent.com/52096462/99184832-69d41e80-2778-11eb-941b-b2ee4926e8f9.PNG)
### Soal 1
Buka uml *MALANG* dan update package list `apt-get update` dan lakukan proses instalasi bind9 dengan perintah `apt-get install bind9 -y`.

Lakukan perintah pada uml *MALANG* `nano /etc/bind/named.conf.local` dan isi konfigurasi pada **semeruc02.pw** dengan syntax
```
zone "semeruc02.pw" {
	type master;
	file "/etc/bind/jarkom/semeruc02.pw";
};
```
![1 1](https://user-images.githubusercontent.com/52096462/99184560-532cc800-2776-11eb-930c-ec2b262d8083.PNG)

Buat folder **jarkom** di dalam /etc/bind `mkdir /etc/bind/jarkom`

Copykan file db.local pada path /etc/bind ke dalam folder jarkom yang baru saja dibuat dan ubah namanya menjadi **semeruc02.pw** `cp /etc/bind/db.local /etc/bind/jarkom/semeruc02.pw`

Kemudian buka file `semeruc02.pw` dan edit

![1 2](https://user-images.githubusercontent.com/52096462/99185444-85412880-277c-11eb-8ab1-406afeee6ea8.PNG)

Lalu restart bind9 `service bind9 restart`. Pada client *GRESIK* dan *SIDOARJO* edit file **resolv.conf** dengan mengetikkan perintah `nano /etc/resolv.conf`

![1 3](https://user-images.githubusercontent.com/52096462/99185526-fda7e980-277c-11eb-953f-4a09aa7ea224.PNG)
![1 5](https://user-images.githubusercontent.com/52096462/99185529-ff71ad00-277c-11eb-9f8c-67513e7148ba.PNG)

Lakukan `ping semeruc02.pw`

![1 4](https://user-images.githubusercontent.com/52096462/99185528-fed91680-277c-11eb-84ad-678b4e2afc2f.PNG)
![1 6](https://user-images.githubusercontent.com/52096462/99185530-000a4380-277d-11eb-9f77-1383664e2598.PNG)

### Soal 2

Buka file `semeruc02.pw` pada uml MALANG, dan masukan konfigurasi

![2 1](https://user-images.githubusercontent.com/52096462/99185574-54adbe80-277d-11eb-87ed-f77bb13d9026.PNG)


Lakukan `service bind9 restart` dan cek **ping www.semeruc02.pw** atau **host -t CNAME www.semeruc02.pw** dari uml *GRESIK*

![2 2](https://user-images.githubusercontent.com/52096462/99185576-56778200-277d-11eb-9a43-bfc1ce6debe4.PNG)


### Soal 3

Edit file **/etc/bind/jarkom/semeruc02.pw** dengan
```
nano /etc/bind/jarkom/semeruc02.pw
```
Serta lakukan konfigurasi pada file tersebut

![3 1](https://user-images.githubusercontent.com/52096462/99185661-e87f8a80-277d-11eb-9ca2-0c67a3aaa4db.PNG)

Setelah itu lakukan `service bind9 restart` dan ping dari *GRESIK* yaitu `ping penanjakan.semeruc02.pw` atau `host -t CNAME penanajakan.semeruc02.pw`

![3 2](https://user-images.githubusercontent.com/52096462/99185662-ea494e00-277d-11eb-9423-4e8307fe06ba.PNG)

### Soal 4

Edit file `/etc/bind/named.conf.local` pada *MALANG*
```
nano /etc/bind/named.conf.local
```

Lalu tambahkan konfigurasi berikut ke dalam file named.conf.local
```
zone "77.151.10.in-addr.arpa" {
    type master;
    file "/etc/bind/jarkom/77.151.10.in-addr.arpa";
};
```

![4 1](https://user-images.githubusercontent.com/52096462/99185696-1a90ec80-277e-11eb-8624-8946c5fc6969.PNG)

Copy file **db.local** ke **77.151.10.in-addr.arpa** dan lakukan edit file tersebut.

![4 2](https://user-images.githubusercontent.com/52096462/99185697-1b298300-277e-11eb-9012-1acf482ad52a.PNG)

Setelah itu lakukan `service bind9 restart`

Untuk mengecek apakah konfigurasi sudah benar atau belum, lakukan perintah berikut pada client *GRESIK*
```
// Install package dnsutils
// Pastikan nameserver telah dikembalikan ke settingan awal
apt-get update
apt-get install dnsutils

//Kembalikan nameserver agar tersambung dengan PROBOLINGGO
host -t PTR 10.151.77.28
```

![4 3](https://user-images.githubusercontent.com/52096462/99185694-195fbf80-277e-11eb-9b5e-17688f7ec049.PNG)

### Soal 5

* Lakukan konfigurasi pada uml *MALANG* dan lakukan edit file **/etc/bind/named.conf.local**, sehingga menjadi

![5 1](https://user-images.githubusercontent.com/52096462/99185766-9a1ebb80-277e-11eb-866c-66edb70089ec.PNG)

Setelah itu dapat melakukan `service bind9 restart`

* Berikutnya pada uml *MOJOKERTO* lakukan update package list `apt-get update` dan install aplikasi bind9 `apt-get install bind9 -y`. Berikutnya tambahkan syntax pada file **/etc/bind/named.conf.local**, gambarannya sebagai berikut

![5 2](https://user-images.githubusercontent.com/52096462/99185768-9b4fe880-277e-11eb-8e0f-7bdac93f9ec2.PNG)

Lakukan restart bind9 `service bind9 restart`

* Pada uml *MALANG*, masukkan command `service bind9 stop` . Pada client *GRESIK* pastikan pengaturan nameserver mengarah ke IP *MALANG* dan IP *MOJOKERTO*

![5 3](https://user-images.githubusercontent.com/52096462/99186856-b5d99000-2785-11eb-8756-7b173d7a5277.PNG)

Lakukan ping ke **semeruc02.pw** pada client *GRESIK*

![5 4](https://user-images.githubusercontent.com/52096462/99185771-9d19ac00-277e-11eb-833f-697aca8bb9b5.PNG)

### Soal 6

* Pada *MALANG*, edit file **/etc/bind/jarkom/semeruc02.pw**, sehingga menjadi

![6 1](https://user-images.githubusercontent.com/52096462/99185814-dd792a00-277e-11eb-9901-c09484fe041c.PNG)

Kemudian edit file **/etc/bind/named.conf.options** pada *MALANG*, dan comment **dnssec-validation auto;** dan tambahkan baris berikut pada **/etc/bind/named.conf.options**
```
allow-query{any;};
```

![6 2](https://user-images.githubusercontent.com/52096462/99185817-de11c080-277e-11eb-839a-a7deeffe7222.PNG)

Berikutnya lakukan `service bind9 restart`.

Kemudian edit file **/etc/bind/named.conf.local** menjadi seperti gambar di bawah:

![6 3](https://user-images.githubusercontent.com/52096462/99185818-deaa5700-277e-11eb-89ff-fb550f79b0b7.PNG)

* Pada *MOJOKERTO* edit file **/etc/bind/named.conf.options**, comment **dnssec-validation auto;** dan tambahkan baris berikut pada **/etc/bind/named.conf.options**
```
allow-query{any;};
```

![6 4](https://user-images.githubusercontent.com/52096462/99185820-dfdb8400-277e-11eb-96d6-b147cc005c22.PNG)

Lalu edit file **/etc/bind/named.conf.local** menjadi seperti gambar di bawah:

![6 5](https://user-images.githubusercontent.com/52096462/99185822-e0741a80-277e-11eb-8c2b-c827532dbfd3.PNG)

Kemudian buat direktori dengan nama delegasi. Copy **db.local** ke direktori delegasi dan edit namanya menjadi **gunung.semeruc02.pw**
```
mkdir /etc/bind/delegasi
cp /etc/bind/db.local /etc/bind/delegasi/gunung.semeruc02.pw
```

Kemudian edit file **gunung.semeruc02.pw**, 

![6 6](https://user-images.githubusercontent.com/52096462/99185825-e10cb100-277e-11eb-9f7f-b93fdd8476ea.PNG)

dan lakukan `service bind9 restart`. Lakukan ping ke domain gunung.semeruc02.pw dari client *GRESIK*

![6 7](https://user-images.githubusercontent.com/52096462/99185813-dbaf6680-277e-11eb-8b08-ab7bef3c1441.PNG)


### Soal 7

Edit file **gunung.semeruc02.pw** juga termasuk memasukkan subdomain **naik.gunung**

![7 1](https://user-images.githubusercontent.com/52096462/99185898-51b3cd80-277f-11eb-84fe-474829232ee4.PNG)

Dan lakukan ping ke domain naik.gunung.semeruc02.pw dari *GRESIK*

![7 2](https://user-images.githubusercontent.com/52096462/99185900-537d9100-277f-11eb-870d-f79193615b21.PNG)

### Soal 8

Pada uml *PROBOLINGGO*, lakukan instalasi `apache2` dan `php`. Pada hal ini, php yang terinstall versi `7.0.33`. 

Pindah ke directory `cd /etc/apache2/sites-available`, dan copy file default **000-default.conf** ke **semeruc02.pw.conf**. lakukan edit file sehingga menjadi

![8 1](https://user-images.githubusercontent.com/52096462/99185909-5f695300-277f-11eb-86a1-2a460756b540.PNG)

Aktifkan konfigurasi `a2ensite semeruc02.pw` dan restart apache. Setelahnya dapat membuka **semeruc02.pw** di browser

![8 2](https://user-images.githubusercontent.com/52096462/99185912-61cbad00-277f-11eb-87d6-33e34a4bd27b.PNG)


### Soal 9

Jalankan perintah `a2enmod rewrite` dan service apache2 dengan `service apache2 restart`. Masih di file yang sama, tambahkan syntax berikut di file **semeruc02.pw.conf**
```
 <Directory /var/www/semeruc02.pw>
     Options +FollowSymLinks -Multiviews
     AllowOverride All
 </Directory>
```

![9 1](https://user-images.githubusercontent.com/52096462/99185920-6bedab80-277f-11eb-88e7-aad0a8768595.PNG)

Untuk mula-mula, maka akan tampil di browser dengan alamat **semeruc02.pw.con/index.php/home**

![9 2](https://user-images.githubusercontent.com/52096462/99185925-73ad5000-277f-11eb-9151-dfc887a69aa2.PNG)

Pindah ke directory **/var/www/semeruc02.pw** dan buat file .htaccess dengan isi file
```
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^home$ /index.php/home [L]
```

![9 3](https://user-images.githubusercontent.com/52096462/99185930-7a3bc780-277f-11eb-9808-5f3608811b50.PNG)

Lakukan `service apache2 restart` dan kembali buka browser dengan alamat **semeruc02.pw/home**

![9 4](https://user-images.githubusercontent.com/52096462/99186056-3b5a4180-2780-11eb-9048-cdcca33eb1d3.PNG)


### Soal 10

Pindah ke directory **/etc/apache2/sites-available** kemudian buka file **penanjakan.semeruc02.pw.conf** ubah menjadi seperti gambar dan sertakan syntax
```
 <Directory /var/www/penanjakan.semeruc02.pw>
     Options +FollowSymLinks -Multiviews
     AllowOverride All
 </Directory>
```
hingga menjadi

![10 1](https://user-images.githubusercontent.com/52096462/99186061-3eedc880-2780-11eb-824d-66aed3baa5ed.PNG)

Lakukan `service apache2 restart`, sehingga hasilnya berupa

![10 2](https://user-images.githubusercontent.com/52096462/99186063-3f865f00-2780-11eb-9d0e-2a8a0799fdca.PNG)

### Soal 11

Buka file **penanjakan.semeruc02.pw.conf** dengan `cd /etc/apache2/sites-available` dan ketikkan `nano penanjakan.semeruc02.pw.conf` yang dimaksud dengan menambahkan syntax
```
 <Directory /var/www/penanjakan.semeruc02.pw/public>
     Options +Indexes
 </Directory>
 
 <Directory /var/www/penanjakan.semeruc02.pw/public/javascripts>
     Options -Indexes
 </Directory>
 
 <Directory /var/www/penanjakan.semeruc02.pw/public/css>
     Options -Indexes
 </Directory>
 
 <Directory /var/www/penanjakan.semeruc02.pw/public/images>
     Options -Indexes
 </Directory>
```

![11 1](https://user-images.githubusercontent.com/52096462/99186092-7b212900-2780-11eb-857e-c32900a6ff68.PNG)

Lakukan `service apache2 restart`, sehingga hasilnya berupa

![11 2](https://user-images.githubusercontent.com/52096462/99186093-7c525600-2780-11eb-93b6-49f1b25ac758.PNG)
![11 3](https://user-images.githubusercontent.com/52096462/99186094-7ceaec80-2780-11eb-81fd-dbfafad29701.PNG)
![11 4](https://user-images.githubusercontent.com/52096462/99186095-7d838300-2780-11eb-8d8f-91421bde74c2.PNG)
![11 5](https://user-images.githubusercontent.com/52096462/99186096-7e1c1980-2780-11eb-91ab-ba69f556e4c6.PNG)

### Soal 12

Disediakan file error **404.html** lain untuk menggantkan file **404.html** bawaan apache. Buka file **penanjakan.semeruc02.pw.conf** dan tambahkan syntax ini dibawah ErrorLog
```
ErrorDocument 404 /errors/404.html
```

![12 1](https://user-images.githubusercontent.com/52096462/99186098-7eb4b000-2780-11eb-841e-16592f69d71c.PNG)

Setlah itu, dapat membuka browser untuk melihat perubahan yang ada dengan mengetikkan **penanjakan.semeruc02.pw/publico**

![12 2](https://user-images.githubusercontent.com/52096462/99186099-7f4d4680-2780-11eb-8f80-ec38449ff2a5.PNG)

Hal ini dapat dibuktikan dengan mengecek halaman error yang ada pada **penanjakan.semeruc02.pw/public/errors/404.html**

![12 3](https://user-images.githubusercontent.com/52096462/99186100-7fe5dd00-2780-11eb-93dc-623776f1bdc7.PNG)

### Soal 13

Buka file **penanjakan.semeruc02.pw.conf** dan tambahkan syntax `Alias "/js" "/var/www/penanjakan.semeruc02.pw/public/javascripts"`

![13 1](https://user-images.githubusercontent.com/52096462/99186101-7fe5dd00-2780-11eb-9c2a-448bf24b5d00.PNG)

Setelahnya dapat membuka alamat **penanjakan.semeruc02.pw/js/** pada browser

* Seperti yang dilihat hasilnya akan forbidden karena hasil dari no. 11 di mana `directory listing` tidak diperbolehkan

### Soal 14

Pindah ke *directory* `/etc/apache2/sites-available` menggunakan perintah
```
cd /etc/apache2/sites-available
```

Buka file **naik.gunung.semeruc02.pw.conf** dan ubah port yang awalnya `80` menjadi `8888`, serta ubah isinya sesuai gambar dibawah ini

![14 1](https://user-images.githubusercontent.com/52096462/99186243-af491980-2781-11eb-8c8b-db8cc1eb6b15.PNG)

Tambahkan port 8888 pada file **ports.conf**. File ports.conf berada pada directory `/etc/apache2`. Cara menambahkannya sebagai berikut pada gambar

Lalu aktifkan konfigurasi **naik.gunung.semeruc02.pw** dan lakukan `service apache2 restart`. dan buka browser dengan alamat **naik.gunung.semeruc02.pw**

![14 2](https://user-images.githubusercontent.com/52096462/99186244-b07a4680-2781-11eb-82b1-b8fe8fa9251f.PNG)

### Soal 15

Buka kembali file **naik.gunung.semeruc02.pw.conf** dengan `cd /etc/apache2/sites-aailable/` dan `nano`, dan masukkan syntax berikut sesuai pada gambar. Syntax juga berasal dari situs lain.
```
<Directory "/var/www/naik.gunung.semeruc02.pw">
      AuthType Basic
      AuthName "Restricted Content"
      AuthUserFile /etc/apache2/.htpasswd
      Require valid-user
</Directory>
```

Konfigurasikan username dan password sesuai soal.

![15 0](https://user-images.githubusercontent.com/52096462/99186245-b112dd00-2781-11eb-845d-a73ce68ed9e9.PNG)

Lakukan `service apache2 restart`, dan buka broowser dengan memasukkan alamat **naik.gunung.semeruc02.pw:8888**  (:8888 sebagai port).

![15 1](https://user-images.githubusercontent.com/52096462/99186247-b1ab7380-2781-11eb-9054-af7853b33d90.PNG)
![15 2](https://user-images.githubusercontent.com/52096462/99186249-b2440a00-2781-11eb-9c18-f018a0c22892.PNG)

Maka akan diminta username dan password, username berupa **semeru** dan password **kuynaikgunung**, setalhnya maka situs dapat dibuka

![15 3](https://user-images.githubusercontent.com/52096462/99186252-b2dca080-2781-11eb-888a-b0b3eefb7481.PNG)
![15 4](https://user-images.githubusercontent.com/52096462/99186253-b3753700-2781-11eb-81ed-c5067db27233.PNG)

### Soal 16

Pindah ke direktori `cd /etc/apache2/sites-available` dan buka file 000-default.conf. Ganti *DocumentRoot* menjadi `/var/www/semeruc02.pw` seperti pada gambar

![16 1](https://user-images.githubusercontent.com/52096462/99186254-b4a66400-2781-11eb-9f76-466083870e22.PNG)
![16 2](https://user-images.githubusercontent.com/52096462/99186256-b4a66400-2781-11eb-8c42-cb2b6ea06863.PNG)

Lakukan restart apache2 dan masukkan *IP Probolinggo* pada browser

![16 3](https://user-images.githubusercontent.com/52096462/99186405-a3118c00-2782-11eb-8654-382e6e35b3df.PNG)
![16 4](https://user-images.githubusercontent.com/52096462/99186410-a4db4f80-2782-11eb-9410-e37aea86ac84.PNG)


### Soal 17
![17 1](https://user-images.githubusercontent.com/52096462/99186450-f71c7080-2782-11eb-9bae-072993614f2e.PNG)
![17 2](https://user-images.githubusercontent.com/52096462/99186451-f84d9d80-2782-11eb-817d-b661ee65e6a8.PNG)
![17 3](https://user-images.githubusercontent.com/52096462/99186452-f8e63400-2782-11eb-8454-dc32ce50931f.PNG)
![17 4](https://user-images.githubusercontent.com/52096462/99186453-faaff780-2782-11eb-8b14-a319a63ba3ad.PNG)
![17 5kloseme0ru](https://user-images.githubusercontent.com/52096462/99186455-fbe12480-2782-11eb-8da4-8795bf2670f0.PNG)
![17 6Hasil](https://user-images.githubusercontent.com/52096462/99186456-fd125180-2782-11eb-800c-65dec69e626c.PNG)
