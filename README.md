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

    <img src="https://user-images.githubusercontent.com/37539546/145604545-0d982687-d091-4332-af24-f384dda6c876.JPG" width="600">
    
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

- Pertama membagi *subnet* (*subnetting*) terhadap topologi. Di sini kelompok kami menggunakan teknik **VLSM** (*Variable Length Subnet Masking*) dalam pembagiannya.

  <img src="https://user-images.githubusercontent.com/37539546/145599487-17bb884c-838c-4d7d-8ab4-e5e3f35180b9.jpg" width="600">

- Penentuan jumlah alamat IP yang dibutuhkan tiap *subnet* dan ***labelling netmask*** berdasarkan jumlah IP. Berdasarkan hasil perhitungan, maka menggunakan *length* **/21** untuk *netmask*-nya.

  <img src="https://user-images.githubusercontent.com/37539546/145600244-c5ec8984-69e2-4f5a-b08d-75e316fc5a6d.png" width="600">

- Pembuatan ***tree subnet*** untuk nantinya membagi IP berdasarkan **NID** dan ***netmask***-nya.

  <img src="https://user-images.githubusercontent.com/37539546/145600501-c342578e-0110-44b5-87e5-52a821f02820.jpg" width=600>

- Pembagian IP dan *netmask* dengan tabel berdasarkan ***tree subnet*** yang sudah dibuat.

  <img src="https://user-images.githubusercontent.com/37539546/145600741-5c76168b-751a-4241-a0e0-eb78cf81f98c.png" width=550>

Kemudian, pada **GNS3** membuat topologi sesuai permintaan soal. *Setting network* masing-masing *node* dengan fitur `Edit network configuration` yang ada di menu `Configure` sesuai pembagian IP menggunanakan VLSM sebelumnya. Berikut konfigurasinya:

- Foosha (Router)
  ```
  auto eth0
  iface eth0 inet dhcp

  auto eth1
  iface eth1 inet static
      address 10.3.7.146
      netmask 255.255.255.252

  auto eth2
  iface eth2 inet static
      address 10.3.7.149
      netmask 255.255.255.252
  ```
  
- Water7 (Router & DHCP Relay)
  ```
  auto eth0
  iface eth0 inet static
  address 10.3.7.145
      netmask 255.255.255.252
      gateway 10.3.7.146

  auto eth1
  iface eth1 inet static
      address 10.3.7.1
      netmask 255.255.255.128

  auto eth2
  iface eth2 inet static
      address 10.3.7.129
      netmask 255.255.255.248

  auto eth3
  iface eth3 inet static
      address 10.3.0.1
      netmask 255.255.252.0
  ```
  
- Guanhao (Router & DHCP Relay)
  ```
  auto eth0
  iface eth0 inet static
      address 10.3.7.150
      netmask 255.255.255.252
      gateway 10.3.7.149

  auto eth1
  iface eth1 inet static
      address 10.3.4.1
      netmask 255.255.254.0

  auto eth2
  iface eth2 inet static
      address 10.3.7.137
      netmask 255.255.255.248

  auto eth3
  iface eth3 inet static
      address 10.3.6.1
      netmask 255.255.255.0
  ```
  
- Doriki (DNS Server)
  ```
  auto eth0
  iface eth0 inet static
      address 10.3.7.130
      netmask 255.255.255.248
      gateway 10.3.7.129
  ```
  
- Jipangu (DHCP Server)
  ```
  auto eth0
  iface eth0 inet static
      address 10.3.7.131
      netmask 255.255.255.248
      gateway 10.3.7.129
  ```
  
- Maingate (Web Server)
  ```
  auto eth0
  iface eth0 inet static
      address 10.3.7.139
      netmask 255.255.255.248
      gateway 10.3.7.137
  ```
  
- Jorge (Web Server)
  ```
  auto eth0
  iface eth0 inet static
      address 10.3.7.138
      netmask 255.255.255.248
      gateway 10.3.7.137
  ```
  
- Blueno (Client)
  ```
  auto eth0
  iface eth0 inet dhcp
  ```
  
- Cipher (Client)
  ```
  auto eth0
  iface eth0 inet dhcp
  ```
  
- Elena (Client)
  ```
  auto eth0
  iface eth0 inet dhcp
  ```
  
- Fukurou (Client)
  ```
  auto eth0
  iface eth0 inet dhcp
  ```

### Foosha

Setelah selesai mengonfigurasi *node*, jalankan *command* berikut pada *router* `Foosha` untuk pengaturan lalu lintas komputer.
```
iptables -t nat -A POSTROUTING -s 10.3.0.0/21 -o eth0 -j SNAT --to-source [IP Foosha]
```

Sebagai catatan, karena IP Foosha akan berubah-ubah, dapat menggunakan *command* `ip a` untuk mendapatkan IP Foosha, contohnya seperti gambar di bawah.

<img src="https://user-images.githubusercontent.com/37539546/145622800-29445b68-e3e7-4f7c-973b-d0493ba505bc.JPG" width="600">

Lalu, lakukan *routing* pada **Foosha** seperti berikut:
```
#NODE KIRI
route add -net 10.3.7.128 netmask 255.255.255.248 gw 10.3.7.145
route add -net 10.3.7.0 netmask 255.255.255.128 gw 10.3.7.145
route add -net 10.3.0.0 netmask 255.255.252.0 gw 10.3.7.145
#NODE KANAN
route add -net 10.3.4.0 netmask 255.255.255.0 gw 10.3.7.150
route add -net 10.3.6.0 netmask 255.255.254.0 gw 10.3.7.150
route add -net 10.3.7.136 netmask 255.255.255.248 gw 10.3.7.150
```

*Testing* pada **Foosha** dengan `ping` ke [**google.com**](https://www.google.com).

<img src="https://user-images.githubusercontent.com/37539546/145623774-ca9ca28e-c8b2-4819-b040-bbb2424c9601.JPG" width="600">

### Semua node (kecuali Foosha)

Agar *node*-*node* lainnya dapat mengakses internet, jalankan *command* berikut dan gunakan IP DNS dari `Foosha`.
```
echo nameserver 192.168.122.1 > /etc/resolv.conf
```

### Water7 dan Guanhao

Lakukan *setting* **DHCP Relay** dengan *install* terlebih dahulu. *Command* yang dijalankan adalah sebagai berikut.
```
apt-get update
apt-get install isc-dhcp-relay -y
```

Buka *file* **/etc/default/isc-dhcp-relay** dan edit seperti konfigurasi berikut.

<img src="https://user-images.githubusercontent.com/37539546/145618270-3426a8ba-aff3-45e4-b7cb-fa0ed8136870.JPG" width="600">

*Restart* **DHCP Relay**.
```
service isc-dhcp-relay restart
```

Untuk memastikan apakah DHCP Relay berjalan, dapat menggunakan *command* berikut.
```
service isc-dhcp-relay status
```

### Jipangu

Lakukan *setting* **DHCP Server** dengan *install* terlebih dahulu. *Command* yang dijalankan adalah sebagai berikut.
```
apt-get update
apt-get install isc-dhcp-server -y
```

Buka *file* **/etc/default/isc-dhcp-server** dan edit bagian paling bawah seperti konfigurasi berikut.

<img src="https://user-images.githubusercontent.com/37539546/145621170-16dc55d9-c641-4c81-b1de-749a3777769f.JPG" width="500">

Buka *file* lagi, yaitu **/etc/dhcp/dhcpd.conf** dan edit seperti konfigurasi berikut.
```
subnet 10.3.7.0 netmask 255.255.255.128 {
    range 10.3.7.2 10.3.7.126;
    option routers 10.3.7.1;
    option broadcast-address 10.3.7.127;
    option domain-name-servers 10.3.7.130;
    default-lease-time 600;
    max-lease-time 7200;
}

# Cipher (A3)
subnet 10.3.0.0 netmask 255.255.252.0 {
    range 10.3.0.2 10.3.3.254;
    option routers 10.3.0.1;
    option broadcast-address 10.3.3.255;
    option domain-name-servers 10.3.7.130;
    default-lease-time 600;
    max-lease-time 7200;
}

# Elena (A6)
subnet 10.3.4.0 netmask 10.3.254.0 {
    range 10.3.4.2 10.3.5.254;
    option routers 10.3.4.1;
    option broadcast-address 10.3.5.255;
    option domain-name-servers 10.3.7.130;
    default-lease-time 600;
    max-lease-time 7200;
}

# Fukurou (A7)
subnet 10.3.6.0 netmask 255.255.255.0 {
    range 10.3.6.2 10.3.6.254;
    option routers 10.3.6.1;
    option broadcast-address 10.3.6.255;
    option domain-name-servers 10.3.7.130;
    default-lease-time 600;
    max-lease-time 7200;
}

# Doriki & Jipangu (A1)
subnet 10.3.7.136 netmask 255.255.255.248 {
}

# Jorge & Maingate (A8)
subnet 10.3.7.128 netmask 255.255.255.248 {
}
```

*Restart* **DHCP Server**.
```
service isc-dhcp-server restart
```

Perlu diketahui, apabila muncul *fail* seperti di bawah, dapat melakukan *restart* DHCP Server kembali.

<img src="https://user-images.githubusercontent.com/37539546/141606738-ea9007d7-d26e-4f15-ac6a-8246d6fa7df7.JPG" width="600">

Untuk memastikan apakah DHCP Server berjalan, dapat menggunakan *command* berikut.
```
service isc-dhcp-server status
```

### Semua *Client*

Sehabis mengonfigurasi **DHCP Server** dan **DHCP Relay**, *restart* semua *node client* agar *service* DHCP dapat berjalan. 

## Soal 2

### Kalian diminta untuk men-*drop* semua akses HTTP dari luar topologi kalian pada *server* yang merupakan DHCP Server dan DNS Server demi menjaga keamanan.

### Jawaban:

### Foosha

Masukkan *command* berikut pada node **Foosha**:
```
iptables -A FORWARD -p tcp --dport 80 -d 10.3.7.128/29 -i eth0 -j DROP
```
- `-A FORWARD` digunakan untuk mendefinisikan *chain* **FORWARD**.
- `-p tcp` digunakan untuk mendefinisikan protokol **TCP**.
-  `80` digunakan untuk mendefinisikan *port* **80**.
-  `d 10.3.7.128/29` digunakan untuk mendefinisikan alamat tujuan dari paket (dalam hal ini DHCP Server dan DNS Server) yang berada pada **10.3.7.128/29**.
-  `i eth0` digunakan untuk memasukkan paket dari **eth0 Foosha**.
-  `-j DROP` digunakan untuk men-*drop* paket.

### Foosha atau Jipangu & Doriki

Kita bisa melakukan *testing* dengan 2 cara, yaitu dengan *ping* website yang berprotokol HTTP pada **Jipangu**/**Doriki** ataupun dengan `nmap -p 80 10.3.7.128` pada **Foosha** (dalam hal ini perlu meng-*install* **netcat** pada *node* **Jipangu**/**Doriki**).

- Menggunakan *ping*

  <img src="https://user-images.githubusercontent.com/37539546/145627329-568b8b04-c912-43c7-a312-bf9cd9ada01a.JPG" width="600">
  
  <img src="https://user-images.githubusercontent.com/37539546/145627654-f409a53b-0472-42bb-a51c-99fd110ddc1b.JPG" width="600">

- Menggunakan `nmap` (sebelumnya pada **Jipangu**/**Doriki** telah menjalankan *command* `nc -l -p 80`)

  <img src="https://user-images.githubusercontent.com/37539546/145668984-93580d2c-1ba6-4a12-bcd6-8623412364f9.JPG" width="500">
  
  <img src="https://user-images.githubusercontent.com/37539546/145669001-1f981a77-a47c-462f-a219-15ea0326c7c0.JPG" width="500">

## Soal 3

### Karena kelompok kalian maksimal terdiri dari 3 orang, Luffy meminta kalian untuk membatasi DHCP dan DNS Server hanya boleh menerima maksimal 3 koneksi ICMP secara bersamaan menggunakan iptables, selebihnya di-*drop*.

### Jawaban:

### Jipangu dan Doriki

Pada kedua *node*, masukkan *command* berikut:
```
iptables -A INPUT -p icmp -m connlimit --connlimit-above 3 --connlimit-mask 0 -j DROP
```
- `-A INPUT` digunakan untuk mendefinisikan *chain* **INPUT**.
- `-p icmp` digunakan untuk mendefinisikan protokol **ICMP**.
-  `-m connlimit` digunakan untuk mendefinisikan *rule connection limit*.
-  `--connlimit-above 3` digunakan untuk *limit* yang ditangkap paket sebanyak > 3.
-  `--connlimit-mask 0` digunakan untuk mengizinkan hanya 3 koneksi untuk tiap *subnet* dalam satu waktu.
-  `-j DROP` digunakan untuk men-*drop* paket.

### 4 *Node* Berbeda (Bebas)

Kita bisa melakukan *testing* dengan *ping* ke arah **Jipangu** atau **Doriki** secara bersamaan pada 4 *node* yang berbeda. Sebagai contoh, kita lakukan *ping* yang mengarah ke **Jipangu** pada *node* **Blueno**, **Cipher**, **Elena**, dan **Fukurou**.

<img src="https://user-images.githubusercontent.com/37539546/145670019-acf3031a-33cd-4f08-b14b-da58dde765cc.gif" width="500">

## Soal 4

### Kemudian kalian diminta untuk membatasi akses ke Doriki yang berasal dari *subnet* Blueno, Cipher, Elena, dan Fukuro dengan beraturan sebagai berikut:
1. Akses dari *subnet* **Blueno** dan **Cipher** hanya diperbolehkan pada pukul 07.00 - 15.00 pada hari Senin sampai Kamis.

### Jawaban:

### Doriki

Masukkan *command* berikut pada node **Doriki**:
```
# BLUENO
iptables -A INPUT -s 10.3.7.0/25 -m time --timestart 07:00 --timestop 15:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -s 10.3.7.0/25 -j REJECT
# CIPHER
iptables -A INPUT -s 10.3.0.0/22 -m time --timestart 07:00 --timestop 15:00 --weekdays Mon,Tue,Wed,Thu -j ACCEPT
iptables -A INPUT -s 10.3.0.0/22 -j REJECT
```
- `-A INPUT` digunakan untuk mendefinisikan *chain* **INPUT**.
- `-s [IP Blueno/Cipher]` digunakan untuk mendefinisikan protokol alamat asal paket dari **Blueno**/**Cipher**.
-  `-m time` digunakan untuk mendefinisikan *rule time*.
-  `--timestart-xx:xx --timestop xx:xx` digunakan untuk mendefinisikan waktu mulai dan berhenti.
-  `--weekdays xxx,xxx,xxx` digunakan untuk mendefinisikan hari.
-  `-j ACCEPT` digunakan untuk menerima paket.
-  `-j REJECT` digunakan untuk menolak paket.

### Blueno atau Cipher

Kita bisa melakukan *testing* dengan mengatur ke waktu tertentu menggunakan *command* `date -s "dd/MMM/yyyy hh:mm:ss"` dan *ping* ke arah **Doriki** pada *node* **Blueno** atau **Cipher**.

- Tanggal: **Kamis, 9 Desember 2021 pukul 13.00** (bisa diakses)

  <img src="https://user-images.githubusercontent.com/37539546/145637065-6a49ae6f-a8ea-497b-9f76-db2171b66e5f.JPG" width="500">
  
- Tanggal: **Sabtu, 4 Desember 2021 pukul 07.00** (tidak bisa diakses)

  <img src="https://user-images.githubusercontent.com/37539546/145637331-2c0ad4f1-4d8c-4621-a8c5-203e2bcc7c00.JPG" width="500">

## Soal 5

### (Lanjutan) 2. Akses dari *subnet* Elena dan Fukurou hanya diperbolehkan pada pukul 15.01 hingga pukul 06.59 setiap harinya. Selain itu di-*reject*.

### Jawaban:

### Doriki

Masukkan *command* berikut pada node **Doriki**:
```
# ELENA
iptables -A INPUT -s 10.3.4.0/23 -m time --timestart 07:00 --timestop 15:00 -j REJECT
# FUKUROU
iptables -A INPUT -s 10.3.6.0/24 -m time --timestart 07:00 --timestop 15:00 -j REJECT
```
- `-A INPUT` digunakan untuk mendefinisikan *chain* **INPUT**.
- `-s [IP Elena/Fukurou]` digunakan untuk mendefinisikan protokol alamat asal paket dari **Elena**/**Fukurou**.
-  `-m time` digunakan untuk mendefinisikan *rule time*.
-  `--timestart-xx:xx --timestop xx:xx` digunakan untuk mendefinisikan waktu mulai dan berhenti.
-  `-j REJECT` digunakan untuk menolak paket.

### Elena atau Fukurou

Kita bisa melakukan *testing* dengan mengatur ke waktu tertentu menggunakan *command* `date -s "dd/MMM/yyyy hh:mm:ss"` dan *ping* ke arah **Doriki** pada *node* **Elena** atau **Fukurou**.

- Tanggal: **Minggu, 6 Desember 2021 pukul 17.00** (bisa diakses)

  <img src="https://user-images.githubusercontent.com/37539546/145638317-73bcfe25-1659-4c57-9c0d-ed188f6c2453.JPG" width="500">
  
- Tanggal: **Jumat, 10 Desember 2021 pukul 10.00** (tidak bisa diakses)

  <img src="https://user-images.githubusercontent.com/37539546/145638096-df458dce-244e-460c-a7ef-de31b3f386c8.JPG" width="500">

## Soal 6

### Karena kita memiliki 2 Web Server, Luffy ingin Guanhao di-*setting* sehingga setiap *request* dari *client* yang mengakses DNS Server akan didistribusikan secara bergantian pada Jorge dan Maingate. Luffy berterima kasih pada kalian karena telah membantunya. Luffy juga mengingatkan agar semua aturan iptables harus disimpan pada sistem atau paling tidak kalian menyediakan *script* sebagai *backup*.

### Jawaban:

### Guanhao

Masukkan *command* berikut pada node **Guanhao**:
```
iptables -t nat -A PREROUTING -d 10.3.7.136 -p tcp --dport 80 -m statistic --mode nth --every 2 --packet 0 -j DNAT --to-destination 10.3.7.138
iptables -t nat -A PREROUTING -d 10.3.7.136 -p tcp --dport 80 -j DNAT --to-destination 10.3.7.139
```

### Maingate dan Jorge

Melakukan instalasi **Apache2** pada **Maingate** dan **Jorge** dengan *update package list*. *Command* yang dijalankan adalah sebagai berikut.
```
apt-get update
apt-get install apache2 -y
```

### Maingate/Jorge dan *Client* (Bebas)

Kita bisa melakukan *testing* dengan menginputkan sembarang kata pada *client*. Sebelumnya *install* **netcat** pada *node* **Maingate** dan **Jorge** terlebih dahulu.
```
apt-get update
apt-get install netcat -y
```

Setelah itu, masukkan perintah `nc -l -p 80` pada **Maingate** dan **Jorge**, dan pada *client* masukkan perintah `nc 10.3.7.136 80`. Terakhir inputkan sembarang kata pada *client*. Pada contoh di bawah menggunakan *client* **Elena** dan **Cipher**.

<img src="https://user-images.githubusercontent.com/37539546/145670056-022d2c73-b108-4a7f-a7fb-b21d472570fd.gif" width="500">

## Kendala
