# Jarkom Modul 5 A08 2021

Anggota:
-   05111940000030 - Bunga Fairuz Wijdan
-   05111940000062 - Thomas Felix Brilliant
-   05111940000145 - Ikhlasul Amal Rivel

**Daftar Soal:**

* [Soal 1](https://github.com/ThomasFel/Jarkom-Modul-5-A08-2021#Soal-1)
* [Soal 2](https://github.com/ThomasFel/Jarkom-Modul-5-A08-2021#Soal-2)
* [Soal 3](https://github.com/ThomasFel/Jarkom-Modul-5-A08-2021#Soal-3)
* [Soal 4](https://github.com/ThomasFel/Jarkom-Modul-5-A08-2021#Soal-4)
* [Soal 5](https://github.com/ThomasFel/Jarkom-Modul-5-A08-2021#Soal-5)
* [Soal 6](https://github.com/ThomasFel/Jarkom-Modul-5-A08-2021#Soal-6)

## Narasi Pendahuluan

Setelah kalian mempelajari semua modul yang telah diberikan, Luffy ingin meminta bantuan untuk terakhir kalinya kepada kalian. Dan kalian dengan senang hati mau membantu Luffy.

-   Tugas pertama kalian yaitu membuat topologi jaringan sesuai dengan rancangan yang diberikan Luffy di bawah ini:
    
    <img src="https://lh4.googleusercontent.com/ty6LE-eYo6B_En_g88XeLYHxGuZ7WyNTGKJPyNGk5pg7dq1dkiAZUDRNZCa_IPc454HQcbMKtwqACJ6UcWcSoO4pE7Mmx4TRkEPRvQc1n5ypBQezF-rpLlHdESEu6xc_2-w7gPz4" width="600">
    
    **Keterangan:**
    - **Doriki** adalah **DNS Server**
    - **Jipangu** adalah **DHCP Server**
    - **Maingate** dan **Jorge** adalah **Web Server**
    - Jumlah *host* pada **Blueno** adalah 100 *host*
    - Jumlah *host* pada **Cipher** adalah 700 *host*
    - Jumlah *host* pada **Elena** adalah 300 *host*
    - Jumlah *host* pada **Fukurou** adalah 200 *host*
    
-   Karena kalian telah belajar *subnetting* dan *routing*, Luffy ingin meminta kalian untuk membuat topologi tersebut menggunakan teknik **CIDR** atau **VLSM**.
-   Setelah melakukan *subnetting*, kalian juga diharuskan melakukan *routing* agar setiap perangkat pada jaringan tersebut dapat terhubung.
-   Tugas berikutnya adalah memberikan IP pada *subnet* **Blueno**, **Cipher**, **Fukurou**, dan **Elena** secara dinamis menggunakan bantuan **DHCP Server**. Kemudian kalian ingat bahwa kalian harus setting **DHCP Relay** pada *router* yang menghubungkannya.

## Soal 1

### Agar topologi yang kalian buat dapat mengakses keluar, kalian diminta untuk mengkonfigurasi Foosha menggunakan iptables, tetapi Luffy tidak ingin menggunakan MASQUERADE.

### Jawaban:

## Soal 2

### Kalian diminta untuk men-*drop* semua akses HTTP dari luar topologi kalian pada *server* yang merupakan DHCP Server dan DNS Server demi menjaga keamanan.

### Jawaban:

## Soal 3

### Karena kelompok kalian maksimal terdiri dari 3 orang, Luffy meminta kalian untuk membatasi DHCP dan DNS Server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya di-*drop*.

### Jawaban:

## Soal 4

### Kemudian kalian diminta untuk membatasi akses ke Doriki yang berasal dari *subnet* Blueno, Cipher, Elena, dan Fukuro dengan beraturan sebagai berikut:
1. Akses dari *subnet* **Blueno** dan **Cipher** hanya diperbolehkan pada pukul 07.00 - 15.00 pada hari Senin sampai Kamis.

### Jawaban:

## Soal 5

### (Lanjutan) 2. Akses dari *subnet* Elena dan Fukuro hanya diperbolehkan pada pukul 15.01 hingga pukul 06.59 setiap harinya. Selain itu di-*reject*.

### Jawaban:

## Soal 6

### Karena kita memiliki 2 Web Server, Luffy ingin Guanhao di-*setting* sehingga setiap *request* dari *client* yang mengakses DNS Server akan didistribusikan secara bergantian pada Jorge dan Maingate. Luffy berterima kasih pada kalian karena telah membantunya. Luffy juga mengingatkan agar semua aturan iptables harus disimpan pada sistem atau paling tidak kalian menyediakan *script* sebagai *backup*.

### Jawaban:
