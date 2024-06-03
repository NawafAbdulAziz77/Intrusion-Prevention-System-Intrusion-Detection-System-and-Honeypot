# Intrusion-Prevention-System-Intrusion-Detection-System-and-Honeypot

## Apa itu IDS, Port Sentry, IPS
Intrusion Detection System (IDS) adalah sistem yang mengawasi traffic jaringan dan kegiatan mencurigakan dalam sebuah jaringan. IDS memberikan peringatan kepada sistem atau administrator jaringan jika mendeteksi aktivitas mencurigakan dan dapat merespons traffic yang tidak normal dengan tindakan seperti penolakan pengguna atau IP address. IDS membantu dalam pertahanan jaringan dengan memonitor fungsi jaringan internal.

Ada dua jenis IDS:
Network-based Intrusion Detection System (NIDS): Menganalisis semua traffic yang mengalir ke jaringan untuk mendeteksi serangan.
Host-based Intrusion Detection System (HIDS): Memantau aktivitas host individual untuk mendeteksi serangan atau penyusupan.
Cara kerja IDS terbagi menjadi dua:
1. Knowledge-based (Misuse Detection): Mengenali penyusupan dengan membandingkan paket data dengan database rule IDS.
2. Behavior-based (Anomaly Based): Mendeteksi keanehan dalam sistem yang dapat dianggap sebagai serangan.

### PortSentry
PortSentry adalah perangkat lunak yang mendeteksi port scanning dan merespons secara aktif dengan memblokir penyerang. PortSentry bekerja di atas soket TCP dan UDP, mendeteksi stealth scan, dan memblokir IP penyerang menggunakan ipchains/ipfwadm dan memasukkan IP tersebut ke dalam file /etc/host.deny. PortSentry juga melaporkan pelanggaran melalui syslog dan dapat diintegrasikan dengan Logcheck untuk laporan email.

## Intrusion Prevention System (IPS)
IPS adalah pengembangan dari IDS yang tidak hanya mendeteksi tetapi juga mencegah serangan. IPS memonitor kegiatan jaringan untuk aktivitas yang mengancam dan mampu menghalangi serangan dengan minimal intervensi administrator. IPS menggunakan banyak filter untuk mencegah serangan seperti worm, virus, dan DoS.

Jenis-jenis IPS:
Network-based Intrusion Prevention System: Memantau seluruh jaringan dari traffic mencurigakan.
Wireless Intrusion Prevention System: Memantau jaringan nirkabel dari traffic mencurigakan.
Network Behavior Analysis (NBA): Memeriksa traffic untuk mengidentifikasi ancaman seperti DDoS.
Host-based Intrusion Prevention System: Memantau aktivitas host individual untuk kegiatan mencurigakan.
Perbedaan IDS dan IPS adalah IDS bersifat pasif sedangkan IPS bersifat aktif dalam memblokir serangan.

## Honeypot
Honeypot adalah sistem informasi yang terbuka yang fokus pada pengumpulan informasi tentang aktivitas ilegal dari attacker. Honeypot melindungi server asli dengan mendirikan server palsu untuk menarik serangan. Ada dua jenis honeypot:
1. High Interaction Honeypot: Mengoperasikan sistem operasi penuh sehingga penyerang melihatnya sebagai target nyata.
2. Low Interaction Honeypot: Mensimulasikan layanan tertentu tanpa memberikan akses penuh kepada penyerang.

Dengan honeypot, administrator dapat menganalisis perilaku penyerang dan melindungi sistem sebenarnya dari serangan.

## Hasil Pengujian
### 1. Pengujian Port Scanning
Pada pengujian port scanning, hasil yang diperoleh menunjukkan bahwa ketika penyerang mencoba melakukan scanning pada server, daftar port yang terbuka tidak akan terlihat karena telah diblokir oleh sistem IPS pada PC penyerang.

Host details juga tidak muncul karena koneksi jaringan ke PC penyerang sudah diblokir (Gambar 1). 
<figure>
    <img src="https://blogger.googleusercontent.com/img/a/AVvXsEgWKpF5HI4vABQsik3LNVfeYSkwg8-v1cRlJlAQM8TsLAZSWkfsFJs9HD2XPfDRCLOxzElpDqRRYQPlq3HwMpyUDRhZsPa9GKGep29-SEETS0K96Ft4srzX4W2EXNVfy9TcEwXc7XTcSbVFgvRrlDyN8O5ACa5yLJEqrmq5aHABBpVb4yruH1jj6KUV7rg" alt="Profile Picture">
</figure>

Pada PC IPS, terdapat log dan status IP penyerang yang mencoba melakukan scanning (Gambar 2). 
<figure>
    <img src="https://blogger.googleusercontent.com/img/a/AVvXsEiemyAjfFwAkElAsa95Pr4v1hz9Ej7lJSq34kTqhI9iF8O4wbAyfWIhoznDwjUcICIlTtF3OPUP5aZeSnHzRmiZ4O_0vy41i0NHSxnaVJBkTObxOFAAwXdH37LFSZbUa5iz6mHGJEtyoVjJjx6FGLGZPdUecRRijkJPESCTlTQE9AbEQHx2cvBbOedf89M" alt="Profile Picture">
</figure>

Pada PC honeypot, juga terlihat log koneksi yang mencoba memasuki alamat IP aktif dalam jaringan (Gambar 3).
<figure>
    <img src="https://blogger.googleusercontent.com/img/a/AVvXsEjfubO8Cqly1ViEIxWM2Q7cygdN5OdXIyzaUrywNS6sygJJCTtDt4uHnU5KkA8Gzvz1pZSCcHVcE_hMYKNuqRQsXB9DpvbiB4gTEyzEb9mEBnjNw9cB4ltn8-hRzkdaS3WQCl3oS-XEwcME9j6fH5HxtuL--2l9erDrI23eSQxuXk-yTcb7w_Q3x8lZuXg" alt="Profile Picture">
</figure>
Dari hasil ini dapat disimpulkan bahwa PSAD mendeteksi dan memblokir usaha scanning dengan bantuan iptables, sementara honeypot mengecoh penyerang dengan informasi palsu jika sistem IPS tidak dapat menangani serangan tersebut.


### 2. Pengujian DoS atau DDoS
Pengujian DoS atau DDoS dilakukan menggunakan tools Hping3 dan Torshammer.

Setelah serangan dilancarkan, website pada PC server masih dapat diakses, menunjukkan bahwa serangan berhasil ditangani (Gambar 4).
<figure>
    <img src="https://blogger.googleusercontent.com/img/a/AVvXsEiiNbK-AHzcJpf1dFruomxGYSq13jOGYfetowxIEtfxPj62f3OkIiVNK3QGYSigde-Ir2vCO90EQ9886I7QmlnxIY73EfhuAdPgNZbbfRYT3T4i8DcFJHSKg8MM09EB3CxeJjaQSM9-MqUFTFOL2eNqY5mGRNGVd3qIG14oxvYjlFtN8xVlrHVAgBa4SYg" alt="Profile Picture">
</figure>

Pada PC IPS, terekam data serangan yang terjadi (Gambar 5), 
<figure>
    <img src="https://blogger.googleusercontent.com/img/a/AVvXsEjqFJGjb3DdybSW2M5wiFNg8lr2VWjUg5vafWHtm0RfDzBhx139TvVSgaXKJPTiIEyhQXP7fLaC47fP9P6oyK62TajrtsmpcpRf46rb_wCGEoeMcDV5yi12cXWUKQpksjJHzF9LDmu_k052QLAs9crzYBbQ_ezAKcSOxxd5kzU03RBEHYpBUgKXKrowdpw" alt="Profile Picture">
</figure>


dan pada PC honeypot terlihat aktivitas jaringan yang menunjukkan pemutusan koneksi karena usaha penyerangan (Gambar 6).
<figure>
    <img src="https://blogger.googleusercontent.com/img/a/AVvXsEjel9AuVAclpwjuIhHpdKeO8BglsZHOVRZ7QSLANwdpGDe2zgirIX2U3W1s-j7-yI28EBK8iCMlV0cg7ZXvf56Bw1Hb9ZCFFhZMTmZ9kBtmmba8cwENWRc3BeXfhWzFFYm-ev6Q6t12EodGb9u0mwACZcAA8YWRBwIjAs0Odex1_j4qN1bf5jR8-euzZuM" alt="Profile Picture">
</figure>
Kesimpulannya, sistem IPS berhasil memblokir penyerang yang mencoba mengirimkan paket dalam jumlah besar. PSAD mendeteksi dan memblokir alamat IP yang mencurigakan sesuai dengan konfigurasi danger level.

### 3. Pengujian SQL Injection
Pengujian SQL Injection menggunakan tools sqlmap menunjukkan bahwa penyerang masih dapat melakukan scanning database pada server dan memperoleh data (Gambar 7). 
<figure>
    <img src="https://blogger.googleusercontent.com/img/a/AVvXsEiC8lhcXSgFzdNnwjmiDagVMZL8ITQYhq0uXfCnklzhunQXPzHv0vtv9_YtMtu51y8MRLgwfZA3-fHhQEGtX-69noj5mheZzR3feujWcPoumRERa9peaEp47y6jFP-VGS9WsXl9XoQVLG_YxsbdgC5MYM64dzG5_G7XtUGsjYDh7ndm6R9iyD9CKzTiyhA" alt="Profile Picture">
</figure>


Namun, ketika mencoba melakukan koneksi ke MySQL pada PC server, koneksi penyerang sudah terputus karena indikasi mencurigakan yang terdeteksi oleh PC IPS (Gambar 8). 
<figure>
    <img src="https://blogger.googleusercontent.com/img/a/AVvXsEgN45IVl4Nxhxc8vpJ7d_dlAvB0OUFFLgIoLzGv9933ep0RL9znO64P63TsHky0mzLzR0epNWy_Nrta616b9mjvREIt_Dzyp-zBW5e8rCt-tHbT7RNmk7rmJ7PZv8-SgozMUzFKNyFSXqjn9R7S-qPGlx4yxU1yvRn1hpdATPF8tzf2kJVyKW0k9FS7oHY" alt="Profile Picture">
</figure>

Status PSAD pada PC IPS menunjukkan deteksi dan pemblokiran usaha penyerangan (Gambar 9).
<figure>
    <img src="https://blogger.googleusercontent.com/img/a/AVvXsEi6eE6wpDYVTijL1nv52fnawIgJ2E6kS-bL0H7vCNN0AXDQerhG4aNJtbq3c8zQko5upzhNLOYg-DtHrm1HzItxSr4q8kA1XPE7KrQdSdR7B0ezMlfm2WYYdlBY9T9Ei2pxLin0iBnbRPO2kTXnhsD5lCoAqPyzofz4jDQxw0IbiCjAJ9Ni8-WCljhY8mQ" alt="Profile Picture">
</figure>


Dari hasil ini, dapat disimpulkan bahwa honeypot tidak dapat sepenuhnya mengatasi serangan SQL Injection, tetapi PSAD efektif dalam mendeteksi dan memblokir usaha penyerangan serta memasukkan alamat IP penyerang dalam daftar blokir.
