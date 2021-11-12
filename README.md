# Jarkom-Modul-3-E03-2021

Daftar Kelompok:

1. Reyhan Naufal Rahman - 05111940000171
2. Vicky Thirdian - 05111940000211
3. Fiodhy Ardito Narawangsa - 05111940000218

## Soal dan Pembahasan

![image](https://user-images.githubusercontent.com/59334824/141429556-461d16e3-cb19-4477-b707-2118657ebaf6.png)

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

```

host Skypie {
    hardware ethernet d2:2c:c8:91:59:81;
    fixed-address 192.201.3.69;
}

```

7.  Loguetown digunakan sebagai client Proxy agar transaksi jual beli dapat terjamin keamanannya, juga untuk mencegah kebocoran data transaksi.

```
base
```

8. Pada Loguetown, proxy harus bisa diakses dengan nama jualbelikapal.yyy.com dengan port yang digunakan adalah 5000

```
base
```

9. Agar transaksi jual beli lebih aman dan pengguna website ada dua orang, proxy dipasang autentikasi user proxy dengan enkripsi MD5 dengan dua username, yaitu luffybelikapalyyy dengan password luffy_yyy dan zorobelikapalyyy dengan password zoro_yyy

```
base
```

10. Transaksi jual beli tidak dilakukan setiap hari, oleh karena itu akses internet dibatasi hanya dapat diakses setiap hari Senin-Kamis pukul 07.00-11.00 dan setiap hari Selasa-Jum’at pukul 17.00-03.00 keesokan harinya (sampai Sabtu pukul 03.00) (10).

```
base
```

11. Agar transaksi bisa lebih fokus berjalan, maka dilakukan redirect website agar mudah mengingat website transaksi jual beli kapal. Setiap mengakses google.com, akan diredirect menuju super.franky.yyy.com dengan website yang sama pada soal shift modul 2. Web server super.franky.yyy.com berada pada node Skypie

```
base
```

12. Saatnya berlayar! Luffy dan Zoro akhirnya memutuskan untuk berlayar untuk mencari harta karun di super.franky.yyy.com. Tugas pencarian dibagi menjadi dua misi, Luffy bertugas untuk mendapatkan gambar (.png, .jpg), sedangkan Zoro mendapatkan sisanya. Karena Luffy orangnya sangat teliti untuk mencari harta karun, ketika ia berhasil mendapatkan gambar, ia mendapatkan gambar dan melihatnya dengan kecepatan 10 kbps

```
base
```

13. Sedangkan, Zoro yang sangat bersemangat untuk mencari harta karun, sehingga kecepatan kapal Zoro tidak dibatasi ketika sudah mendapatkan harta yang diinginkannya

```
base
```
