
---

# Mikhmon-PPPoE-Ros.7

[![License](https://img.shields.io/github/license/heruhendri/Mikhmon-PPPoE-Ros.7.svg)](LICENSE)
[![Stars](https://img.shields.io/github/stars/heruhendri/Mikhmon-PPPoE-Ros.7.svg)](https://github.com/heruhendri/Mikhmon-PPPoE-Ros.7/stargazers)
[![Forks](https://img.shields.io/github/forks/heruhendri/Mikhmon-PPPoE-Ros.7.svg)](https://github.com/heruhendri/Mikhmon-PPPoE-Ros.7/network/members)
![PHP](https://img.shields.io/badge/PHP-7.x-blue.svg)
![License](https://img.shields.io/badge/license-Personal%20Use%20Only-orange)
![Status](https://img.shields.io/badge/status-active-brightgreen)

## 📌 Deskripsi

**Mikhmon-PPPoE-Ros.7** adalah aplikasi berbasis web yang dikembangkan untuk memudahkan manajemen user PPPoE pada Mikrotik RouterOS versi 7.x. Dengan antarmuka sederhana dan fitur yang lengkap, aplikasi ini membantu admin jaringan dalam mengelola, monitoring, dan mengotomatisasi tugas-tugas terkait PPPoE user secara efisien.

---

## ✨ Fitur Utama

- **Manajemen User PPPoE**  
  Tambah, edit, hapus, dan monitoring user PPPoE dengan mudah.

- **Dashboard Interaktif**  
  Menampilkan data statistik user aktif, penggunaan bandwidth, dan performa router.

- **Otomatisasi Voucher**  
  Generate dan cetak voucher internet dengan cepat.

- **Backup & Restore**  
  Fitur backup/restore konfigurasi user PPPoE.

- **Keamanan**  
  Akses login untuk admin, serta log aktivitas.

---


## 🖥️ Screenshot

> 
![Screenshot](https://raw.githubusercontent.com/heruhendri/Mikhmon-PPPoE-Ros.7/refs/heads/master/ss.png)

---

## ⚙️ Penggunaan

1. Login menggunakan akun admin.
2. Atur koneksi ke Router Mikrotik pada menu **Pengaturan**.
3. Kelola user PPPoE, monitoring, dan cetak voucher sesuai kebutuhan Anda.

---

## 📌 Instalasi dengan Simple bisa menggunakan script [Script Auto Instaler Mikhmon](https://github.com/heruhendri/Mikhmon-PPPoE-Ros.7/tree/installer)

```bash
wget -O installer-mikhmon.sh hhttps://raw.githubusercontent.com/heruhendri/Mikhmon-PPPoE-Ros.7/refs/heads/installer/installer-mikhmon-sh
chmod +x installer-mikhmon.sh
./installer-mikhmon.sh
```
---

## ⚙️ Opsi Instalasi 2 (Menggunakan Domain Https Cloudflare)
**multi-instal Mikhmon HTTPS di NAT VPS**
By Hendri 👍
Berikut langkah **lengkap & aman** untuk **install Mikhmon Multi (multi user)** di **NAT VPS** (misalnya dari NATVPS) dan menambahkan **HTTPS (SSL)**.

---

## 🧩 Persiapan Awal

Pastikan kamu sudah punya:

* VPS NAT (misalnya NATVPS)
* Akses SSH (dari panel NATVPS Bisa Menggunakan Putty Atau Terminal Yanglain)
* Subdomain (misalnya `mikhmon.hendri.site`)
* Token Cloudflare (opsional, untuk SSL otomatis)

---

## ⚙️ 1. Update & Install Dependensi

Masuk SSH sebagai root:

```bash
apt update && apt upgrade -y
apt install nginx php php-fpm php-cli php-curl php-zip php-xml php-mbstring unzip curl git -y
```

Pastikan PHP aktif:

```bash
php -v
```

---

## 📦 2. Install Mikhmon Multi

Masuk ke folder web:

```bash
cd /var/www/
```

Clone repo Mikhmon Multi (versi asli):

```bash
git clone https://github.com/laksa19/mikhmonv3.git mikhmon
```

Atau jika kamu mau versi **multi user modifikasi**, pakai:

```bash
git clone https://github.com/heruhendri/Mikhmon-PPPoE-Ros.7.git mikhmon
```

---

## 🧰 3. Konfigurasi Nginx

Buat file konfigurasi baru (Buat Format Seperti dibawah dan masukan satu persatu jika anda ingin menginstal mikhmon lebih dari satu): 

```bash
nano /etc/nginx/sites-available/mikhmon1.conf
nano /etc/nginx/sites-available/mikhmon2.conf
nano /etc/nginx/sites-available/mikhmon3.conf
```

Isi dengan konfigurasi ini (ganti domain kamu):

```nginx
server {
    listen 80;
    server_name mikhmon.hendri.site;

    root /var/www/html/mikhmon1;
    index index.php index.html;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php-fpm.sock;
    }

    location ~ /\.ht {
        deny all;
    }
}
```

Simpan & keluar (`CTRL + X`, `Y`, `Enter`).

Aktifkan site:

```bash
ln -s /etc/nginx/sites-available/mikhmon1.conf /etc/nginx/sites-enabled/
ln -s /etc/nginx/sites-available/mikhmon2.conf /etc/nginx/sites-enabled/
ln -s /etc/nginx/sites-available/mikhmon3.conf /etc/nginx/sites-enabled/
ln -s /etc/nginx/sites-available/mikhmon4.conf /etc/nginx/sites-enabled/
```

Uji konfigurasi:

```bash
nginx -t
```

Reload Nginx:

```bash
systemctl reload nginx
```

---

## 🔒 4. Tambahkan HTTPS (SSL)

### Opsi 1 – Jika pakai domain Cloudflare:

* Aktifkan mode SSL → **Full (strict)** di Cloudflare.
* Arahkan subdomain ke IP publik NAT VPS (gunakan port NAT, misalnya `x.x.x.x:12345`).
* Cloudflare akan otomatis memberikan HTTPS.

### Opsi 2 – Install Let’s Encrypt (langsung di VPS):

Gunakan **Certbot**:

```bash
apt install certbot python3-certbot-nginx -y
certbot --nginx -d mikhmon.hendri.site
```

Ikuti petunjuk dan pilih opsi “Redirect HTTP to HTTPS”.

---

## 🧱 5. Akses Mikhmon

Sekarang buka di browser:

```
https://mikhmon.hendri.site
```

Login default (jika ada) biasanya:

```
User: admin
Pass: 1234
```

---

## ⚡ 6. Tips Tambahan

| Tujuan         | Perintah                                      |
| -------------- | --------------------------------------------- |
| Restart Nginx  | `systemctl restart nginx`                     |
| Cek status PHP | `systemctl status php-fpm`                    |
| Lokasi web     | `/var/www/mikhmon/`                           |
| Backup         | `zip -r mikhmon-backup.zip /var/www/mikhmon/` |

---



## ⚙️ Opsi Instalasi 3 (Menggunakan IP VPS Dan Port)
 **multi-instal Mikhmon di NAT VPS** (misalnya 2–3 instance sekaligus, beda port).

---

### 1. **Siapkan VPS**

Pastikan VPS kamu sudah:

* OS: Ubuntu/Debian (lebih stabil buat Mikhmon)
* Sudah ada akses root
* Sudah install web server (nginx/apache) + PHP

Kalau belum, install dulu (contoh pakai nginx + php):

```bash
apt update && apt upgrade -y
apt install nginx php php-cli php-fpm unzip wget -y
```

---

### 2. **Download Mikhmon**

Masuk ke folder web (default di nginx biasanya `/var/www/html/`):

```bash
cd /var/www/html/
wget git clone https://github.com/heruhendri/Mikhmon-PPPoE-Ros.6.git mikhmon -O mikhmon.zip
unzip mikhmon.zip
mv mikhmonv3-master mikhmon1
```

Instance pertama sudah ada di `/var/www/html/mikhmon1`

---

### 3. **Tambah Instance Lain**

Kalau mau multi-instal (misalnya `mikhmon2`, `mikhmon3`):

```bash
cp -r /var/www/html/mikhmon1 /var/www/html/mikhmon2
cp -r /var/www/html/mikhmon1 /var/www/html/mikhmon3
```

Jadi ada:

* `/var/www/html/mikhmon1`
* `/var/www/html/mikhmon2`
* `/var/www/html/mikhmon3`

---

### 4. **Atur Virtual Host / Port**

#### Opsi A: Pakai **subfolder**

Kalau langsung akses via domain/IP:

* `http://IP-VPS/mikhmon1`
* `http://IP-VPS/mikhmon2`
* `http://IP-VPS/mikhmon3`

#### Opsi B: Pakai **port berbeda**

Bikin config nginx baru:

```bash
nano /etc/nginx/sites-available/mikhmon1.conf
```

Isi:

```nginx
server {
    listen 8081;
    root /var/www/html/mikhmon1;
    index index.php;
    server_name _;

    location / {
        try_files $uri $uri/ /index.php?$args;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php7.4-fpm.sock; # sesuaikan versi PHP
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }
}
```

Simpan, lalu copy untuk instance lain (`8082` → `/var/www/html/mikhmon2`, dst).

Aktifkan site:

```bash
ln -s /etc/nginx/sites-available/mikhmon1.conf /etc/nginx/sites-enabled/
ln -s /etc/nginx/sites-available/mikhmon2.conf /etc/nginx/sites-enabled/
```

Reload nginx:

```bash
systemctl reload nginx
```

Sekarang bisa diakses via:

* `http://IP-VPS:8081` → mikhmon1
* `http://IP-VPS:8082` → mikhmon2
* `http://IP-VPS:8083` → mikhmon3

---

### 5. **(Opsional) Pakai Subdomain**

Kalau punya domain, bisa arahkan:

* `mikhmon1.domain.com`
* `mikhmon2.domain.com`

Cukup ubah `server_name` di config nginx.

---

⚡ Jadi intinya ada 3 cara akses multi Mikhmon:

1. **Subfolder** → `IP/mikhmon1`, `IP/mikhmon2` (paling gampang).
2. **Multi-port** → `IP:8081`, `IP:8082`.
3. **Subdomain** → `mikhmon1.domain.com`, `mikhmon2.domain.com`.

---

## ❗ Lisensi

Perangkat lunak ini hanya diperbolehkan untuk penggunaan pribadi.  
**Dilarang keras** menggandakan, mendistribusikan, memodifikasi, atau menggunakan untuk tujuan komersial tanpa izin tertulis dari pemilik.

Copyright © 2025 heruhendri

---

## 🤝 Kontribusi

Kontribusi sangat terbatas karena lisensi penggunaan pribadi. Untuk pertanyaan, silakan hubungi saya melalui:

- [GitHub Issues](https://github.com/heruhendri/Mikhmon-PPPoE-Ros.7/issues)
- Email: heruu2004@gmail.com

---

## 📢 Catatan

- Pastikan RouterOS sudah update ke versi 7.x.
- Selalu backup data sebelum melakukan perubahan besar.

---

Terima kasih telah menggunakan **Mikhmon-PPPoE-Ros.7**!  
Dukung terus pengembangan tools open-source dengan tetap menghormati lisensi penggunaan.

---

