# Arsitektur database Main-Replica RW dan RO dengan failover

---

# Requirements

Pastikan sistem Anda telah menginstall:

- **Docker**
- **Docker Compose**

Cek instalasi dengan perintah berikut:

```bash
docker --version
docker compose version
```

---

# Installation Guide

Ikuti langkah-langkah berikut untuk menjalankan project ini di lingkungan lokal Anda.

---

## 1. Clone Repository

Clone repository ini ke komputer Anda.

```bash
git clone https://github.com/geraldiadityo/postgresql-main-replica-HA.git
```

Masuk ke dalam folder project.

```bash
cd repository-name
```

---

## 2. Konfigurasi Environment

Ubah semua file `.env.example` menjadi `.env.name`, kemudian sesuaikan konfigurasi environment sesuai kebutuhan Anda.

Contoh:

```bash
cp .env.example.name .env.name
```

Setelah itu edit file `.env.name` sesuai dengan konfigurasi yang Anda inginkan.

---

## 3. Pull Docker Images

Download semua image yang dibutuhkan oleh project menggunakan perintah berikut:

```bash
docker compose pull
```

Perintah ini akan mengambil semua image yang didefinisikan pada file `docker-compose.yml`.

---

## 4. Menjalankan Container

Setelah proses pull selesai, jalankan seluruh service dengan perintah berikut:

```bash
docker compose up -d
```

Flag `-d` digunakan untuk menjalankan container dalam mode **detached (background)**.

---

## 5. Verifikasi Container

Pastikan seluruh container telah berjalan dengan baik:

```bash
docker compose ps
```

Jika berhasil, status container akan terlihat sebagai **Up**.

---

## 6. Akses Aplikasi

Buka browser Anda dan akses aplikasi melalui URL berikut:

```
http://localhost:7000
```

Jika semua langkah berhasil dilakukan, maka aplikasi akan berjalan dengan normal.

---

# Database Access

Repository ini menyediakan dua jenis koneksi database:

| Type            | Description                                        | Port     |
| --------------- | -------------------------------------------------- | -------- |
| RW (Read-Write) | Digunakan untuk operasi **insert, update, delete** | **5050** |
| RO (Read-Only)  | Digunakan untuk operasi **read/query saja**        | **5001** |

### Read-Write Database

Gunakan port berikut untuk koneksi database dengan hak akses penuh:

```
localhost:5050
```

Koneksi ini biasanya digunakan oleh:

- Service backend utama
- Migration
- Seeder
- Administrative task

---

### Read-Only Database

Gunakan port berikut untuk koneksi database yang hanya dapat melakukan **read/query**:

```
localhost:5001
```

Koneksi ini biasanya digunakan oleh:

- Reporting service
- Analytics
- Background jobs
- Service yang hanya membutuhkan data tanpa melakukan perubahan

---

# Useful Commands

Beberapa perintah yang sering digunakan selama development:

### Melihat Logs

```bash
docker compose logs -f
```

---

### Menghentikan Container

```bash
docker compose down
```

---

### Restart Container

```bash
docker compose restart
```

---

# Troubleshooting

Jika container tidak berjalan dengan baik:

1. Periksa logs container

```bash
docker compose logs
```

2. Pastikan port yang digunakan tidak bentrok dengan aplikasi lain.

3. Pastikan konfigurasi pada file `.env.name` sudah benar.
