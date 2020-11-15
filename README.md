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

Lakukan perintah pada uml *MALANG* `nano /etc/bind/named.conf.local` dan isi konfigurasi pada **semeruc12.pw** dengan syntax
```
zone "semeruc12.pw" {
	type master;
	file "/etc/bind/jarkom/semeruc12.pw";
};
```
![1 1](https://user-images.githubusercontent.com/52096462/99184560-532cc800-2776-11eb-930c-ec2b262d8083.PNG)

Buat folder **jarkom** di dalam /etc/bind `mkdir /etc/bind/jarkom`

Copykan file db.local pada path /etc/bind ke dalam folder jarkom yang baru saja dibuat dan ubah namanya menjadi **semeruc12.pw** `cp /etc/bind/db.local /etc/bind/jarkom/semeruc12.pw`

Kemudian buka file `semeruc12.pw` dan edit

![1 2](https://user-images.githubusercontent.com/52096462/99185444-85412880-277c-11eb-8ab1-406afeee6ea8.PNG)

Lalu restart bind9 `service bind9 restart`. Pada client *GRESIK* dan *SIDOARJO* edit file **resolv.conf** dengan mengetikkan perintah `nano /etc/resolv.conf`

![1 3](https://user-images.githubusercontent.com/52096462/99185526-fda7e980-277c-11eb-953f-4a09aa7ea224.PNG)
![1 5](https://user-images.githubusercontent.com/52096462/99185529-ff71ad00-277c-11eb-9f8c-67513e7148ba.PNG)

Lakukan `ping semeruc12.pw`

![1 4](https://user-images.githubusercontent.com/52096462/99185528-fed91680-277c-11eb-84ad-678b4e2afc2f.PNG)
![1 6](https://user-images.githubusercontent.com/52096462/99185530-000a4380-277d-11eb-9f77-1383664e2598.PNG)

### Soal 2

Buka file `semeruc12.pw` pada uml MALANG, dan masukan konfigurasi

![2 1](https://user-images.githubusercontent.com/52096462/99185574-54adbe80-277d-11eb-87ed-f77bb13d9026.PNG)


Lakukan `service bind9 restart` dan cek **ping www.semeruc12.pw** atau **host -t CNAME www.semeruc12.pw** dari uml *GRESIK*

![2 2](https://user-images.githubusercontent.com/52096462/99185576-56778200-277d-11eb-9a43-bfc1ce6debe4.PNG)


### Soal 3

Edit file **/etc/bind/jarkom/semeruc12.pw** dengan
```
nano /etc/bind/jarkom/semeruc12.pw
```
Serta lakukan konfigurasi pada file tersebut

![3 1](https://user-images.githubusercontent.com/52096462/99185661-e87f8a80-277d-11eb-9ca2-0c67a3aaa4db.PNG)

Setelah itu lakukan `service bind9 restart` dan ping dari *GRESIK* yaitu `ping penanjakan.semeruc12.pw` atau `host -t CNAME penanajakan.semeruc12.pw`

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

//Kembalikan nameserver agar tersambung dengan MALANG
host -t PTR 10.151.77.28
```

![4 3](https://user-images.githubusercontent.com/52096462/99185694-195fbf80-277e-11eb-9b5e-17688f7ec049.PNG)

## Soal 5

* Lakukan konfigurasi pada uml *MALANG* dan lakukan edit file **/etc/bind/named.conf.local**, sehingga menjadi

![Img 17](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/5.0.jpg)

Setelah itu dapat melakukan `service bind9 restart`

![Img 18](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/5.1.jpg)

* Berikutnya pada uml *MOJOKERTO* lakukan update package list `apt-get update` dan install aplikasi bind9 `apt-get install bind9 -y`. Berikutnya tambahkan syntax pada file **/etc/bind/named.conf.local**, gambarannya sebagai berikut

![Img 19](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/5.2.jpg)

Lakukan restart bind9 `service bind9 restart`

* Pada uml *MALANG*, masukkan command `service bind9 stop` . Pada client *GRESIK* pastikan pengaturan nameserver mengarah ke IP *MALANG* dan IP *MOJOKERTO*

![Img 20](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/5.5.jpg)

Lakukan ping ke **semeruc12.pw** pada client *GRESIK*

![Img 21](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/5.6.jpg)

## Soal 6

* Pada *MALANG*, edit file **/etc/bind/jarkom/semeruc12.pw**, sehingga menjadi

![Img 22](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/6.1.jpg)

Kemudian edit file **/etc/bind/named.conf.options** pada *MALANG*, dan comment **dnssec-validation auto;** dan tambahkan baris berikut pada **/etc/bind/named.conf.options**
```
allow-query{any;};
```

![Img 23](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/6.2.jpg)

Berikutnya lakukan `service bind9 restart`.

Kemudian edit file **/etc/bind/named.conf.local** menjadi seperti gambar di bawah:

![Img 24](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/6.3.jpg)

* Pada *MOJOKERTO* edit file **/etc/bind/named.conf.options**, comment **dnssec-validation auto;** dan tambahkan baris berikut pada **/etc/bind/named.conf.options**
```
allow-query{any;};
```

![Img 25](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/6.5.jpg)

Lalu edit file **/etc/bind/named.conf.local** menjadi seperti gambar di bawah:

![Img 26](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/6.6.jpg)

Kemudian buat direktori dengan nama delegasi. Copy **db.local** ke direktori pucang dan edit namanya menjadi **gunung.semeruc12.pw**
```
mkdir /etc/bind/delegasi
cp /etc/bind/db.local /etc/bind/delegasi/gunung.semeruc12.pw
```

Kemudian edit file **gunung.semeruc12.pw**, 

![Img 27](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/6.8.jpg)

dan lakukan `service bind9 restart`. Lakukan ping ke domain gunung.semeruc12.pw dari client *GRESIK*

![Img 28](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/6.7.jpg)


## Soal 7

Edit file **gunung.semeruc12.pw** juga termasuk memasukkan subdomain **naik.gunung**, dan lakukan ping ke domain naik.gunung.semeruc12.pw dari *GRESIK*

![Img 29](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/7.0.jpg)

## Web Server (Soal 8 - 17)

## Soal 8

Pada uml *PROBOLINGGO*, lakukan instalasi `apache2` dan `php`. Pada hal ini, php yang terinstal versi `7.0.33`. 

Pindah ke directory `cd /etc/apache2/sites-available`, dan copy file default **000-default.conf** ke **semeruc12.pw.conf**. lakukan edit file shingga menjadi

![Img 30](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/8.0.jpg)

Aktifkan konfigurasi `a2ensite semeruc12.pw` dan restart apache. Setlahnya dapat membuka **semeruc12.pw** di browser

![Img 31](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/8.1.jpg)


## Soal 9

Jalankan perintah `a2enmod rewrite` dan service apache2 dengan `service apache2 restart`. Masih di file yang sama, tambahkan syntax berikut di file **semeruc12.pw.conf**
```
 <Directory /var/www/semeruc12.pw>
     Options +FollowSymLinks -Multiviews
     AllowOverride All
 </Directory>
```

![Img 32](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/9.0.jpg)

Untuk mula-mula, maka akan tampil di browser dengan alamat **semeruc12.pw.con/index.php/home**

![Img 33](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/9.3.jpg)

Pindah ke directory **/var/www/semeruc12.pw** dan buat file .htaccess dengan isi file
```
RewriteEngine On
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule ^home$ /index.php/home [L]
```

![Img 34](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/9.2.jpg)

Lakukan `service apache2 restart` dan kembali buka browser dengan alamat **semeruc12.pw/home**

![Img 35](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/9.1.jpg)


## Soal 10

Pindah ke directory **/etc/apache2/sites-available** kemudian buka file **penanjakan.semeruc12.pw.conf** dan tambahkan syntax
```
 <Directory /var/www/penanjakan.semeruc12.pw>
     Options +FollowSymLinks -Multiviews
     AllowOverride All
 </Directory>
```
hingga menjadi

![Img 36](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/10.3.jpg)

Lakukan `service apache2 restart`, sehingga hasilnya berupa

![Img 37](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/10.0.jpg)
![Img 38](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/10.1.jpg)
![Img 39](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/10.2.jpg)

## Soal 11

Buka file **penanjakan.semeruc12.pw.conf** dengan `cd /etc/apache2/sites-available` dan ketikkan `nano penanjakan.semeruc12.pw.conf` yang dimaksud dengan menambahkan syntax
```
 <Directory /var/www/penanjakan.semeruc12.pw/public>
     Options +Indexes
 </Directory>
 
 <Directory /var/www/penanjakan.semeruc12.pw/public/javascripts>
     Options -Indexes
 </Directory>
 
 <Directory /var/www/penanjakan.semeruc12.pw/public/css>
     Options -Indexes
 </Directory>
 
 <Directory /var/www/penanjakan.semeruc12.pw/public/images>
     Options -Indexes
 </Directory>
```

![Img 40](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/11.6.jpg)

Lakukan `service apache2 restart`, sehingga hasilnya berupa

![Img 41](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/11.0.jpg)
![Img 42](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/11.1.jpg)
![Img 43](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/11.2.jpg)
![Img 44](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/11.3.jpg)

## Soal 12

Disediakan file error **404.html** lain untuk menggantkan file **404.html** sebelumnya. Buka file **penanjakan.semeruc12.pw.conf** dan tambahkan syntax, syntax diambil dari situs lain.
```
ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined

ErrorDocument 404 /errors/404.html

<Files "errors/404.html">
     <If "-z %{ENV:REDIRECT_STATUS}">
            RedirectMatch 404 ^/errors/404.html$
     </If>
</Files>
```

![Img 45](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/12.1.jpg)

Setlah itu, dapat membuka browser untuk melihat perubahan yang ada dengan mengetikkan **penanjakan.semeruc12.pw/errors/404.html**

![Img 46](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/12.0.jpg)

Hal ini juga dapat diterapkan pada alamat lain yang menuju ke halaman 404.

![Img 47](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/12.2.jpg)

## Soal 13

Buka file **penanjakan.semeruc12.pw.conf** dan tambahkan syntax `Alias "/js" "/var/www/penanjakan.semeruc12.pw/public/javascripts"`

![Img 48](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/13.2.jpg)

Setelahnya dapat membuka alamat **penanjakan.semeruc12.pw/public/javascripts/** pada browser

* Gambar berikut merupakan gambar ketika `folder javascripts` masih dapat dibuka

![Img 49](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/13.0.jpg)

* Sedangkan gambar berikut merupakan hasil dari no. 11 di mana `directory listing` tidak diperbolehkan

![Img 50](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/13.4.jpg)

Lalu dapat membuka alamat **penanjakan.semeruc12.pw/js/** pada browser

* Gambar berikut merupakan gambar ketika `folder javascripts` dengan konfigurasi virtual host `/js/` masih dapat dibuka

![Img 51](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/13.1.jpg)

* Sedangkan gambar berikut merupakan gambar ketika `folder javascripts` dengan konfigurasi virtual host `/js/` dengan hasil dari no. 11 di mana `directory listing` tidak diperbolehkan.

![Img 51](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/13.3.jpg)

## Soal 14

Pindah ke *directory* `/etc/apache2/sites-available` menggunakan perintah
```
cd /etc/apache2/sites-available
```

Buka file **naik.gunung.semeruc12.pw.conf** dan ubah port yang awalnya `80` menjadi `8888`, serta ubah *DocumentRoot* yang awalnya `/var/www/html` menjadi `/var/www/naik.gunung.semeruc12.pw`, seperti gambar berikut

![Img 52](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/14.1.jpg)

Tambahkan port 8888 pada file **ports.conf**. File ports.conf berada pada directory `/etc/apache2`. Cara menambahkannya sebagai berikut pada gambar

![Img 53](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/14.2.jpg)

Lalu aktifkan konfigurasi **naik.gunung.semeruc12.pw** dan lakukan `service apache2 restart`. dan buka browser dengan alamat **naik.gunung.semeruc12.pw**

![Img 54](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/14.0.jpg)


## Soal 15

Buka kembali file **naik.gunung.semeruc12.pw.conf** dengan `cd /etc/apache2/sites-aailable/` dan `nano`, dan masukkan syntax berikut sesuai pada gambar. Syntax juga berasal dari situs lain.
```
<Directory "/var/www/naik.gunung.semeruc12.pw">
      AuthType Basic
      AuthName "Restricted Content"
      AuthUserFile /etc/apache2/.htpasswd
      Require valid-user
</Directory>
```

Konfigurasikan username dan password sesuai soal.

![Img 55](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/15.2.jpg)

Lakukan `service apache2 restart`, dan buka broowser dengan memasukkan alamat **naik.gunung.semeruc12.pw:8888**  (:8888 sebagai port).

![Img 56](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/15.0.jpg)

Maka akan diminta username dan password, username berupa **semeru** dan password **kuynaikgunung**, setalhnya maka situs dapat dibuka

![Img 57](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/15.1.jpg)


## Soal 16

Pindah ke direktori `cd /etc/apache2/sites-available` dan buka file 000-default.conf. Ganti *DocumentRoot* menjadi `/var/www/semeruc12.pw` seperti pada gambar

![Img 58](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/16.1.jpg)

Lakukan restart apache2 dan masukkan *IP Probolinggo* pada browser

![Img 59](https://github.com/riclown/Jarkom_modul2_praktikum_C12/blob/main/img/16.0.jpg)


## Soal 17
