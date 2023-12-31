# Jarkom-Modul-1-E06-2023
Berikut adalah repository dari kelompok E06 untuk pengerjaan Praktikum Modul 1 Jaringan Komputer. Repository ini akan berisikan dokumentasi cara pengerjaan tiap soal, screenshot output, dan kendala yang dialami.

# Anggota Kelompok
| Nama | NRP | 
| --- | --- |
| Muhammad Hafidh Rosyadi | 5025211013 |
| Kartika Diva Asmara Gita | 5025211039 |

# Dokumentasi Pengerjaan Soal
## Nomor 1
### Soal
User melakukan berbagai aktivitas dengan menggunakan protokol FTP. Salah satunya adalah mengunggah suatu file.
- Berapakah sequence number (raw) pada packet yang menunjukkan aktivitas tersebut?
- Berapakah acknowledge number (raw) pada packet yang menunjukkan aktivitas tersebut? 
- Berapakah sequence number (raw) pada packet yang menunjukkan response dari aktivitas tersebut?
- Berapakah acknowledge number (raw) pada packet yang menunjukkan response dari aktivitas tersebut?

### Jawaban
- Karena aktivitas menggunakan protocol FTP dan salah satunya adalah mengunggah file maka dapat digunakan filter `ftp.request.command == STOR` dimana STOR merupakan aktivitas untuk mengunggah suatu file.
- Pada bagian Transmission Protocol Control, dapat dilihat nilai sequence number (raw) dan juga acknowledge number (raw).

![image](src/1ab.png)

- Karena Response dari request pasti berdekatan, maka dapat dilakukan filter protocol 'ftp' dan dapat dicari paket setelah paket 147 (paket request). Paket 149 adalah paket setelah 147 dan berisi response, maka itu pasti reponse dari aktivitas mengunggah file.
- Dapat dilihat nilai sequence number (raw) dan juga acknowledge number (raw) dari paket reponse.

![image](src/1cd.png)

- Berikut jawaban dan flag:
  
![image](src/1flag.png)

## Nomor 2
### Soal
Sebutkan web server yang digunakan pada portal praktikum Jaringan Komputer!

### Jawaban
- Karena ip pada platform jarkom adalah 10.21.78.111, maka dilakukan filter `ip.src == 10.21.78.111` untuk mengambil paket yang berasal dari ip tersebut.
  
![image](src/2a.png)

Selanjutnya klik kanan, follow, dan TCP Stream untuk melihat web server yang digunakan yaitu gunicorn.

![image](src/2b.png)

Berikut jawaban dan flag:

![image](src/2flag.png)

## Nomor 3
### Soal
Dapin sedang belajar analisis jaringan. Bantulah Dapin untuk mengerjakan soal berikut:
- Berapa banyak paket yang tercapture dengan IP source maupun destination address adalah 239.255.255.250 dengan port 3702?
- Protokol layer transport apa yang digunakan?

### Jawaban
- Dilakukan filter `ip.addr == 239.255.255.250 && (udp.port == 3702 || tcp.port == 3702)` untuk melihat paket ip 239.255.255.250 dan paket dengan port 3702.

![image](src/3.png)

- Pada detail bagian diatas, dapat dilihat bawah terdapat 21 paket dengan protokol layer yang digunakan hanya UDP saja.
- Berikut jawaban dan flag:

![image](src/3flag.png)

## Nomor 4
### Soal 
Berapa nilai checksum yang didapat dari header pada paket nomor 130?

### Jawaban
- Mencari paket dengan nomor 130, kemudian lihat detail paket pada bagian Transmission Protocol Control.

![image](src/4.png)

Didapatkan nilai Checksum adalah 0x18e5.
Berikut jawaban dan flag:

![image](src/4flag.png)

## Nomor 5
### Soal
Elshe menemukan suatu file packet capture yang menarik. Bantulah Elshe untuk menganalisis file packet capture tersebut.
- Berapa banyak packet yang berhasil di capture dari file pcap tersebut?
- Port berapakah pada server yang digunakan untuk service SMTP?
- Dari semua alamat IP yang tercapture, IP berapakah yang merupakan public IP?

### Jawaban
- Untuk membuka file zip yang diberikan dibutuhkan password, sehingga perlu untuk mencari password dari satu persatu detail paket yang diberikan.

![image](src/5a.png)

- klik kanan, follow, dan TCP Stream untuk mencari password.
- Dalam pengecekan TCP stream di dalam paket, ditemukan password yaitu NWltcGxlUGFzNXdvcmQ= pada paket nomor 3

![image](src/5b.png)

- Decode password dengan base64 sesuai dengan arahan.
- Didapatkan password yaitu 5implePas5word untuk mengekstrak zip file.

![image](src/5c.png)

- Pada zip file terdapat port netcat nc 10.21.78.111 11111.

![image](src/5d.png)

#### poin 1 (Berapa banyak packet yang berhasil di capture dari file pcap tersebut?)

![image](src/5e.png)

#### poin 2 (Port berapakah pada server yang digunakan untuk service SMTP?)

![image](src/5f.png)

#### poin 3 (Dari semua alamat IP yang tercapture, IP berapakah yang merupakan public IP?)
`ip :74.53.140.153`

![image](src/5flag.png)

### Kendala
- Agak kebingungan untuk pertama kali, karena pertama kali menghadapi tipe soal seperti ini

## Nomor 6
### Soal
Seorang anak bernama Udin Berteman dengan SlameT yang merupakan seorang penggemar film detektif. sebagai teman yang baik, Ia selalu mengajak slamet untuk bermain valoranT bersama. suatu malam, terjadi sebuah hal yang tak terdUga. ketika udin mereka membuka game tersebut, laptop udin menunjukkan sebuah field text dan Sebuah kode Invalid bertuliskan "**server SOURCE ADDRESS 7812 is invalid**". ketika ditelusuri di google, hasil pencarian hanya menampilkan a1 e5 u21. jiwa detektif slamet pun bergejolak. bantulah udin dan slamet untuk menemukan solusi kode error tersebut.

### Jawaban

![image](src/6.png)

- IP pada paket no 7812 adalah `104.18.14.101`.
- sesuai dengan petunjuk soal a1 e5 u21 berarti IP diubah dari bilangan 1-26 yang merupakan angka ke alphabet, sehingga menjadi 10 4 18 14 10 1 = JDRNJA

![image](src/6flag)

### Kendala
- Butuh waktu untuk memahami apa yang diminta soal.

## Nomor 7
### Soal
Berapa jumlah packet yang menuju IP 184.87.193.88?

### Jawaban
Melakukan filter terhadap paket yang menuju ip 184.87.193.88 dengan filter `ip.dst == 184.87.193.88`

![image](src/7.png)

Dapat dilihat displayed sebanyak 6.

![image](src/7flag.png)

## Nomor 8
### Soal
Berikan kueri filter sehingga wireshark hanya mengambil semua protokol paket yang menuju port 80! (Jika terdapat lebih dari 1 port, maka urutkan sesuai dengan abjad)

### Jawaban
Melakukan filter `tcp.dstport == 80 || udp.dstport == 80`
untuk menampilkan seluruh paket yang menuju port 80 dan secara default terurut.

![image](src/8.png)

![image](src/8flag.png)


## Nomor 9
### Soal
Berikan kueri filter sehingga wireshark hanya mengambil paket yang berasal dari alamat 10.51.40.1 tetapi tidak menuju ke alamat 10.39.55.34!

### Jawaban
untuk melakukan filter tersebut memiliki lebih dari satu kemungkinan (variasi && dan and) namun hanya
`ip.src == 10.51.40.1 && ip.dst != 10.39.55.34` yang memunculkan flag.

![image](src/9flag.png)

### Kendala
- Ada lebih dari 1 kueri yang menampilkan apa yang diminta oleh soal, sehingga harus melakukan trial and error.

## Nomor 10
### Soal
Sebutkan kredensial yang benar ketika user mencoba login menggunakan Telnet

### Jawaban
dengan filter `telnet` untuk menampilkan seluruh protokol yang menggunakan telnet. 

![image](src/10a.png)

dan dicari yang memiliki format username:password pada tcp streamnya. 

![image](src/10b.png)

dari username dan password yang ada, hanya `dhafin:kesayangannyak0k0`yang memunculkan flag.

![image](src/10flag.png)
