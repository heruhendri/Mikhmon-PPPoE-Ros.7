
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

## 🚀 Instalasi

**cara install Mikhmon di VPS Ubuntu** (misalnya Ubuntu 20.04 atau 22.04):

---

### ✅ **1. Update Sistem**

```bash
sudo apt update && sudo apt upgrade -y
```

---

### ✅ **2. Install Apache, PHP, dan Modul Pendukung**

```bash
sudo apt install apache2 php php-curl php-cli php-xml php-mbstring unzip git -y
```

---

### ✅ **3. Download Mikhmon**

Kita akan clone versi **Mikhmon-mod** (lebih stabil dan aktif di-maintain):

```bash
cd /var/www/
sudo git clone https://github.com/heruhendri/Mikhmon-PPPoE-Ros.7.git mikhmon
```

> Atau jika mau versi original:
>
> ```bash
> sudo git clone https://github.com/laksa19/mikhmon.git mikhmon
> ```

---

### ✅ **4. Ubah Hak Akses Folder**

```bash
sudo chown -R www-data:www-data /var/www/mikhmon
sudo chmod -R 755 /var/www/mikhmon
```

---

### ✅ **5. Konfigurasi Apache**

Buat virtual host:

```bash
sudo nano /etc/apache2/sites-available/mikhmon.conf
```

Isi dengan:

```apache
<VirtualHost *:80>
    ServerAdmin admin@yourdomain.com
    DocumentRoot /var/www/mikhmon
    ServerName yourdomain.com

    <Directory /var/www/mikhmon>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/mikhmon_error.log
    CustomLog ${APACHE_LOG_DIR}/mikhmon_access.log combined
</VirtualHost>
```

> Ganti `yourdomain.com` dengan domain kamu, atau hapus `ServerName` jika hanya pakai IP VPS.

---

### ✅ **6. Aktifkan Site dan Restart Apache**

```bash
sudo a2ensite mikhmon
sudo a2enmod rewrite
sudo systemctl restart apache2
```

---

### ✅ **7. Akses Mikhmon**

Buka browser dan akses:

* Jika pakai domain: `http://yourdomain.com`
* Jika pakai IP VPS: `http://IP-VPS-ANDA`

---

### ✅ (Opsional) **Pasang SSL (HTTPS)**

Jika kamu menggunakan domain:

```bash
sudo apt install certbot python3-certbot-apache -y
sudo certbot --apache
```

---

### ✅ **8. Login Mikhmon**

Default login:

* **Username:** `admin`
* **Password:** `admin`

Langsung bisa mulai tambahkan Router Mikrotik kamu dari halaman dashboard.

---

Kalau kamu ingin auto-start dan tanpa terminal, bisa juga pakai versi **Mikhmon Desktop atau Docker**, tinggal disesuaikan saja.



### Prasyarat

- Webserver (Apache/Nginx)
- PHP 7.x
- Ekstensi PHP: cURL, OpenSSL, JSON
- Mikrotik RouterOS v7.x

### Cara Instalasi

1. **Clone repositori**
   ```bash
   git clone https://github.com/heruhendri/Mikhmon-PPPoE-Ros.7.git
   ```

2. **Pindahkan ke folder webserver**
   ```bash
   mv Mikhmon-PPPoE-Ros.7 /var/www/html/
   ```

3. **Konfigurasi**
   - Edit file `config.php` sesuai kredensial Mikrotik dan kebutuhan Anda.

4. **Akses melalui browser**
   ```
   http://localhost/Mikhmon-PPPoE-Ros.7
   ```

---

## 🖥️ Screenshot

> 
![Screenshot](https://github.com/heruhendri/Mikhmon-PPPoE-Ros.7/blob/master/mikhmon/ss.png?raw=true)

---

## ⚙️ Penggunaan

1. Login menggunakan akun admin.
2. Atur koneksi ke Router Mikrotik pada menu **Pengaturan**.
3. Kelola user PPPoE, monitoring, dan cetak voucher sesuai kebutuhan Anda.

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

