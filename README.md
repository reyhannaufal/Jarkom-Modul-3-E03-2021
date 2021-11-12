# Jarkom Modul 3 E03 2021

Daftar Kelompok:

1. Reyhan Naufal Rahman - 05111940000171
2. Vicky Thirdian - 05111940000211
3. Fiodhy Ardito Narawangsa - 05111940000218

---
### Buatlah topologi sebagai berikut. Dengan penjelasan bahwa `eth1` dan `eth3` merupakan server client sedangkan `eth2` merupakan server.
![image](https://user-images.githubusercontent.com/59334824/141429556-461d16e3-cb19-4477-b707-2118657ebaf6.png)

## Soal dan Pembahasan


1. Semua client yang ada HARUS menggunakan konfigurasi IP dari DHCP Server.

![image](https://user-images.githubusercontent.com/59334824/141429489-59f055cb-c5e7-4867-a13c-9feef28c4bfe.png)

```
base
```

2. Client yang melalui Switch1 mendapatkan range IP dari [prefix IP].1.20 - [prefix IP].1.99 dan [prefix IP].1.150 - [prefix IP].1.169

![image](https://user-images.githubusercontent.com/59334824/141429711-ccb0e48a-19a7-459d-9a42-e562750168fc.png)
![image](https://user-images.githubusercontent.com/59334824/141429920-58d908fc-d753-4f80-969b-84b9cb1a1233.png)

```
base
```

3. Client yang melalui Switch1 mendapatkan range IP dari [prefix IP].1.20 - [prefix IP].1.99 dan [prefix IP].1.150 - [prefix IP].1.169

```
subnet 192.201.2.0 netmask 255.255.255.248 {
    option routers 192.201.2.1;
    option broadcast-address 192.201.0.255;
    option domain-name-servers 192.201.2.4, 192.168.122.1;
}


subnet 192.201.1.0 netmask 255.255.255.0 {
    range 192.201.1.20 192.201.1.99;
    range 192.201.1.150 192.201.1.169;
    option routers 192.201.1.1;
    option broadcast-address 192.201.0.255;
    option domain-name-servers 192.201.2.4, 192.168.122.1;
    default-lease-time 360;
    max-lease-time 7200;
}

subnet 192.201.3.0 netmask 255.255.255.0 {
    range 192.201.3.30 192.201.3.50;
    option routers 192.201.3.1;
    option broadcast-address 192.201.0.255;
    option domain-name-servers 192.201.2.4, 192.168.122.1;
    default-lease-time 720;
    max-lease-time 7200;
}
```

4. Client mendapatkan DNS dari EniesLobby dan client dapat terhubung dengan internet melalui DNS tersebut.

```
subnet 192.201.2.0 netmask 255.255.255.248 {
    option routers 192.201.2.1;
    option broadcast-address 192.201.0.255;
    option domain-name-servers 192.201.2.4, 192.168.122.1;
}


subnet 192.201.1.0 netmask 255.255.255.0 {
    range 192.201.1.20 192.201.1.99;
    range 192.201.1.150 192.201.1.169;
    option routers 192.201.1.1;
    option broadcast-address 192.201.0.255;
    option domain-name-servers 192.201.2.4, 192.168.122.1;
    default-lease-time 360;
    max-lease-time 7200;
}

subnet 192.201.3.0 netmask 255.255.255.0 {
    range 192.201.3.30 192.201.3.50;
    option routers 192.201.3.1;
    option broadcast-address 192.201.0.255;
    option domain-name-servers 192.201.2.4, 192.168.122.1;
    default-lease-time 720;
    max-lease-time 7200;
}
```

5. Lama waktu DHCP server meminjamkan alamat IP kepada Client yang melalui Switch1 selama 6 menit sedangkan pada client yang melalui Switch3 selama 12 menit. Dengan waktu maksimal yang dialokasikan untuk peminjaman alamat IP selama 120 menit.

```
subnet 192.201.2.0 netmask 255.255.255.248 {
    option routers 192.201.2.1;
    option broadcast-address 192.201.0.255;
    option domain-name-servers 192.201.2.4, 192.168.122.1;
}


subnet 192.201.1.0 netmask 255.255.255.0 {
    range 192.201.1.20 192.201.1.99;
    range 192.201.1.150 192.201.1.169;
    option routers 192.201.1.1;
    option broadcast-address 192.201.0.255;
    option domain-name-servers 192.201.2.4, 192.168.122.1;
    default-lease-time 360;
    max-lease-time 7200;
}

subnet 192.201.3.0 netmask 255.255.255.0 {
    range 192.201.3.30 192.201.3.50;
    option routers 192.201.3.1;
    option broadcast-address 192.201.0.255;
    option domain-name-servers 192.201.2.4, 192.168.122.1;
    default-lease-time 720;
    max-lease-time 7200;
}
```

6. Luffy dan Zoro berencana menjadikan Skypie sebagai server untuk jual beli kapal yang dimilikinya dengan alamat IP yang tetap dengan IP [prefix IP].3.69

Untuk menjadikan skypie sebagai fixed ip, pertama-tama pastikan ip `dhcp.conf` sudah benar. Setelah itu masukan kode dibawah, hardware ethernet didapatkan dengan melihat outut dari

```
ip a

```
Masukan pada config `dhcp` dan set fixed-address `fixed-address 192.201.3.69`
```
host Skypie {
    hardware ethernet d2:2c:c8:91:59:81;
    fixed-address 192.201.3.69;
}

```

7.  Loguetown digunakan sebagai client Proxy agar transaksi jual beli dapat terjamin keamanannya, juga untuk mencegah kebocoran data transaksi.

Jika ingin membuat logutown sebagai client proxy maka pertama

Untuk menambahkan proxy pada client `loguetown` lakukanlah command dibawah. Maka akan terset proxy pada client tersebut

```
export http_proxy='jualbelikapal.e03.com:5000'
```

8. Pada Loguetown, proxy harus bisa diakses dengan nama jualbelikapal.yyy.com dengan port yang digunakan adalah 5000

Script untuk webserver
```
apt-get install php -y
apt-get install libapache2-mod-php7.0 -y

git clone https://github.com/FeinardSlim/Praktikum-Modul-2-Jarkom.git

apt-get install unzip
mv super.franky.zip /var/www/

unzip /var/www/super.franky.zip

mv /var/www/super.franky /var/www/super.franky.e03.com
```

Buatlah sebuah dns server dengan `jualbelikapal.e03.com` dengan config sebagai berikut

```
zone "jualbelikapal.e03.com" {
        type master;
        file "/etc/bind/jarkom/jualbelikapal.e03.com";
};
```

Lalu pada config `/etc/bind/jarkom/jualbelikapal.e03.com` aturlah config seperti yang ada dibawah dan arahkan ke pada server Water7 sebagi server proxy
```
;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     jualbelikapal.e03.com. root.jualbelikapal.e03.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      jualbelikapal.e03.com.
@       IN      A       192.201.2.3
```

Pada sisi server proxy tambahkan config dibawah. http_port merupakan port yang akan di set pada sisi client
```
http_port 5000
visible_hostname Water7

dns_nameserver 192.201.2.4 //server dns
```


Untuk menambahkan proxy pada client `loguetown` lakukanlah command dibawah

```
export http_proxy='jualbelikapal.e03.com:5000'
```

9. Agar transaksi jual beli lebih aman dan pengguna website ada dua orang, proxy dipasang autentikasi user proxy dengan enkripsi MD5 dengan dua username, yaitu luffybelikapalyyy dengan password luffy_yyy dan zorobelikapalyyy dengan password zoro_yyy

Jika ingin memasukan password untuk autentikasi maka lakukanlah command dibawah, selanjutkan akan terdapat prompt memasukan nilai password.

```
htpasswd -c -m /etc/squid/passwd zorobelikapale03
```

Pada `squid.conf` tambahkan config dibawah

```
auth_param basic program /usr/lib/squid/basic_ncsa_auth /etc/squid/passwd
auth_param basic children 5
auth_param basic realm Proxy
auth_param basic credentialsttl 2 hours
auth_param basic casesensitive on
acl USERS proxy_auth REQUIRED
http_access allow USERS
```

![image](https://user-images.githubusercontent.com/59334824/141435249-e0ffae63-5510-4b1b-8afd-2cdc0d1fb962.png)


10. Transaksi jual beli tidak dilakukan setiap hari, oleh karena itu akses internet dibatasi hanya dapat diakses setiap hari Senin-Kamis pukul 07.00-11.00 dan setiap hari Selasa-Jum’at pukul 17.00-03.00 keesokan harinya (sampai Sabtu pukul 03.00) (10).

- Config pertama adalah untuk menghandle case hari senin-kamis pukuk 07:00-11:00 (case pagi)
- Config kedua adalah untuk menghandle case dari hari selasa-jumat pukul 17:00-23:59 (case sore-malan)
- Config ketiga adalah untuk menghandle case dari rabu-sabtu pukul 00:00-03:00 (case malam-pagi)

```
acl SATU time MTWH 07:00-11:00
acl DUA  time TWHF 17:00-23:59
acl TIGA time WHFA 00:00-03:00
```

11. Agar transaksi bisa lebih fokus berjalan, maka dilakukan redirect website agar mudah mengingat website transaksi jual beli kapal. Setiap mengakses google.com, akan diredirect menuju super.franky.yyy.com dengan website yang sama pada soal shift modul 2. Web server super.franky.yyy.com berada pada node Skypie

```
zone "super.franky.e03.com" {
        type master;
        file "/etc/bind/jarkom/super.franky.e03.com";
};
```

```

;
; BIND data file for local loopback interface
;
$TTL    604800
@       IN      SOA     super.franky.e03.com. root.super.franky.e03.com. (
                              2         ; Serial
                         604800         ; Refresh
                          86400         ; Retry
                        2419200         ; Expire
                         604800 )       ; Negative Cache TTL
;
@       IN      NS      super.franky.e03.com.
@       IN      A       192.201.3.69
www     IN      CNAME   super.franky.e03.com.

```

```
<VirtualHost *:80>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/super.franky.e03.com
        #Redirect / http://www.super.franky.e03.com

        ServerName super.franky.e03.com
        ServerAlias www.super.franky.e03.com

        <Directory /var/www/super.franky.e03.com>
                Options +Indexes
                AllowOverride All
        </Directory>

        <Directory /var/www/super.franky.e03.com/public>
                Options +Indexes
        </Directory>
        
         Alias "/js" "/var/www/super.franky.e03.com/public/js"
</VirtualHost>

```

Lalu pada setting server squi lakukanlah config seperti dibawah
```
acl awas url_regex "/etc/squid/ban.acl"
deny info http://super.franky.e03.com awas
http_access deny awas
```

lalu pada file `etc/squid/ban.acl` isi dengan `google.com`



12. Saatnya berlayar! Luffy dan Zoro akhirnya memutuskan untuk berlayar untuk mencari harta karun di super.franky.yyy.com. Tugas pencarian dibagi menjadi dua misi, Luffy bertugas untuk mendapatkan gambar (.png, .jpg), sedangkan Zoro mendapatkan sisanya. Karena Luffy orangnya sangat teliti untuk mencari harta karun, ketika ia berhasil mendapatkan gambar, ia mendapatkan gambar dan melihatnya dengan kecepatan 10 kbps

Masukan config dibawah pada `squid.conf`. Lakukan sorting file untuk `jpg` dan `png`, lalu buatlah 2 pools untuk membedakan 2 tipe pencarian internet
- satu untuk kecepatan normal
- dua untuk kecepatan internet yang dibatasi 10kbps

```
acl download url_regex -i ftp \.jpg$ \.png$

delay_pools 2

delay_class 1 1
delay_parameters 1 -1/-1
delay_access 1 deny all

delay_class 2 1
delay_access 2 allow download
delay_access 2 deny all
delay_parameters 2 10000/10000

```

![image](https://user-images.githubusercontent.com/59334824/141442239-c82ad962-8dda-4af8-854b-fcb93d139353.png)


13. Sedangkan, Zoro yang sangat bersemangat untuk mencari harta karun, sehingga kecepatan kapal Zoro tidak dibatasi ketika sudah mendapatkan harta yang diinginkannya

Pada dasarnya by default untuk case pada soal ini sudah terpenuhi. Ketika berselancar ataupun download file selain bertipe `png` dan `jpg` maka speed internet tidak akan dilimit.

![image](https://user-images.githubusercontent.com/59334824/141442297-cdc4fd25-f348-45d2-90c1-0b50e186f571.png)
