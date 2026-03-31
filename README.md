# 🗄️ Basis Data — Kumpulan Tugas & Dokumentasi SQL

Repository ini berisi dokumentasi lengkap tugas-tugas mata kuliah **Basis Data**, mencakup praktik SQL dari dasar hingga tingkat lanjut menggunakan MySQL. Setiap part menampilkan query beserta hasil eksekusinya sebagai bukti kerja dan bahan referensi belajar.

---

## 📋 Daftar Isi

- [Part 1 — Membuat Database & Tabel](#-part-1--membuat-database--tabel)
- [Part 2 — Constraint, Alias & Fungsi String](#-part-2--constraint-alias--fungsi-string)
- [Part 3 — Filtering dengan WHERE & ORDER BY](#-part-3--filtering-dengan-where--order-by)
- [Part 4 — Fungsi Matematika & Agregasi](#-part-4--fungsi-matematika--agregasi)
- [Part 5 — CASE WHEN & Aggregasi Lanjutan](#-part-5--case-when--aggregasi-lanjutan)
- [Part 6 — JOIN Tabel](#-part-6--join-tabel)
- [Part 7 — JOIN Kompleks & BETWEEN](#-part-7--join-kompleks--between)
- [Part 8 — Eksplorasi Database Subscription](#-part-8--eksplorasi-database-subscription)
- [Part 9 — Pengenalan Data CSV](#-part-9--pengenalan-data-csv)
- [Part 10 — GROUP BY, HAVING & Subquery JOIN](#-part-10--group-by-having--subquery-join)

---

## 📌 Part 1 — Membuat Database & Tabel

**Topik:** `CREATE DATABASE`, `CREATE TABLE`, `INSERT INTO`, `SELECT`

Part ini memperkenalkan cara membuat database baru, mendefinisikan struktur tabel, mengisi data, dan menampilkan data sederhana menggunakan perintah dasar SQL.

### Yang dipelajari:
- Membuat database `quiz_db1` dan berpindah ke dalamnya menggunakan `USE`
- Membuat tabel `ms_produk` dengan kolom: `no_urut` (INT), `kode_produk` (VARCHAR), `nama_produk` (VARCHAR), dan `harga` (INT)
- Memasukkan 10 data produk DQLab sekaligus menggunakan `INSERT INTO ... VALUES`
- Menampilkan kolom tertentu (`nama_produk`, `harga`) menggunakan `SELECT`
- Membatasi jumlah baris yang ditampilkan menggunakan `LIMIT 5`

### Contoh Query:
```sql
-- Membuat database
CREATE DATABASE quiz_db1;
USE quiz_db1;

-- Membuat tabel
CREATE TABLE ms_produk (
    no_urut INT,
    kode_produk VARCHAR(10),
    nama_produk VARCHAR(50),
    harga INT
);

-- Memasukkan data
INSERT INTO ms_produk VALUES
    (1, 'prod-01', 'Kotak Pensil DQLab', 62500),
    (2, 'prod-02', 'Flashdisk DQLab 64 GB', 55000),
    ...;

-- Menampilkan data terbatas
SELECT nama_produk, harga FROM ms_produk LIMIT 5;
```

---

## 📌 Part 2 — Constraint, Alias & Fungsi String

**Topik:** `PRIMARY KEY`, `AS` (alias kolom), `CONCAT`, table alias

Part ini memperluas pemahaman tentang pembuatan tabel dengan constraint, penggunaan alias untuk mempercantik output, serta manipulasi string pada kolom hasil query.

### Yang dipelajari:
- Membuat tabel `ms_pelanggan` dengan `no_urut INT PRIMARY KEY` sebagai kunci utama
- Menggunakan `AS` untuk memberi alias pada kolom, contohnya mengubah tampilan `no_urut` menjadi `nomor` dan `nama_produk` menjadi `nama`
- Perbedaan antara alias menggunakan kata kunci `AS` dan tanpa kata kunci `AS` — keduanya menghasilkan output yang sama
- Menggunakan `CONCAT('Rp ', harga)` untuk menggabungkan teks dengan nilai kolom sehingga harga tampil dalam format `Rp 62500`
- Menggunakan table alias (`FROM produk t2`) untuk merujuk tabel dengan nama pendek

### Contoh Query:
```sql
-- Alias kolom dengan AS
SELECT no_urut AS nomor, nama_produk AS nama FROM produk;

-- Alias kolom tanpa AS
SELECT no_urut nomor, nama_produk nama FROM produk;

-- CONCAT untuk format harga
SELECT CONCAT('Rp ', harga) harga_jual FROM produk;

-- Table alias
SELECT * FROM produk t2;
```

---

## 📌 Part 3 — Filtering dengan WHERE & ORDER BY

**Topik:** `WHERE`, `AND`, `OR`, operator perbandingan (`>`, `<`), `ORDER BY`

Part ini membahas cara memfilter data dengan kondisi tertentu menggunakan klausa WHERE, termasuk mengombinasikan beberapa kondisi sekaligus dan mengurutkan hasil query.

### Yang dipelajari:
- Filtering data berdasarkan nilai kolom yang tepat: `WHERE nama_produk = 'Tas Travel Organizer DQLab'`
- Menggunakan operator `OR` untuk mencari lebih dari satu nilai sekaligus
- Menggunakan operator `>` untuk mencari data dengan harga di atas batas tertentu (contoh: `WHERE harga > 50000` menghasilkan 7 produk)
- Mengombinasikan `AND` dengan operator perbandingan: `WHERE harga < 50000 AND no_urut = 8`
- Menampilkan data transaksi dengan kalkulasi total (`qty * harga`) dan menggunakan `ORDER BY total DESC` untuk mengurutkan dari nilai terbesar

### Contoh Query:
```sql
-- Filter satu nilai
SELECT * FROM ms_produk WHERE nama_produk = 'Tas Travel Organizer DQLab';

-- Filter beberapa nilai dengan OR
SELECT * FROM ms_produk
WHERE nama_produk = 'Flashdisk DQLab 64 GB'
   OR nama_produk = 'Tas Travel Organizer DQLab'
   OR nama_produk = 'Gantungan Kunci DQLab';

-- Filter harga dengan operator
SELECT * FROM ms_produk WHERE harga > 50000;

-- Kombinasi AND
SELECT * FROM ms_produk WHERE harga < 50000 AND no_urut = 8;

-- Order by dengan kalkulasi
SELECT kode_pelanggan, nama_produk, qty, harga, (qty * harga) AS total
FROM ms_transaksi
WHERE (qty * harga) >= 100000
ORDER BY total DESC;
```

---

## 📌 Part 4 — Fungsi Matematika & Agregasi

**Topik:** `MOD`, `EXP`, `UPPER`, `LOWER`, `MIN`, `MAX`

Part ini menggunakan database mahasiswa (`students`) untuk mempraktikkan berbagai fungsi bawaan MySQL, mulai dari fungsi matematika hingga fungsi agregasi dasar.

### Yang dipelajari:
- Menggunakan `MOD(Semester1, 2)` untuk menghitung sisa bagi nilai semester
- Menggunakan `EXP(MarkGrowth)` untuk menghitung nilai eksponensial dari pertumbuhan nilai
- Menggunakan `UPPER(FirstName)` untuk mengubah teks menjadi huruf kapital semua
- Menggunakan `LOWER(LastName)` untuk mengubah teks menjadi huruf kecil semua
- Menggunakan `MIN()` dan `MAX()` untuk menemukan nilai minimum dan maksimum dari kolom Semester1 dan Semester2 sekaligus dalam satu query

### Contoh Query:
```sql
-- Fungsi matematika
SELECT StudentID, FirstName, LastName,
       MOD(Semester1, 2) AS Semester1,
       Semester2,
       EXP(MarkGrowth) AS 'EXP(MarkGrowth)'
FROM students;

-- Fungsi string
SELECT StudentID,
       UPPER(FirstName) AS FirstName,
       LOWER(LastName) AS LastName
FROM students;

-- Agregasi MIN dan MAX
SELECT MIN(Semester1) AS Min1, MAX(Semester1) AS Max1,
       MIN(Semester2) AS Min2, MAX(Semester2) AS Max2
FROM students;
```

---

## 📌 Part 5 — CASE WHEN & Aggregasi Lanjutan

**Topik:** `CASE WHEN`, `SUM`, `AVG`, `GROUP BY`, `HAVING`

Part ini menggunakan database penjualan skala besar (tabel `orderdetails` dan `ms_transaksi`) untuk mempraktikkan logika kondisional dan agregasi per grup.

### Yang dipelajari:
- Menggunakan `CASE WHEN ... THEN ... ELSE ... END` untuk mengklasifikasikan data secara otomatis:
  - Total penjualan ≥ 50.000 → `'Target Achieved'`
  - Total penjualan ≤ 20.000 → `'Less performed'`
  - Selain itu → `'Follow Up'`
- Menggunakan `GROUP BY orderNumber` untuk menghitung total per nomor pesanan dari ratusan baris data
- Menghitung total revenue keseluruhan dengan `SUM(qty * harga)` → hasil: **Rp 3.326.600**
- Menghitung total kuantitas seluruh transaksi dengan `SUM(qty)` → hasil: **43 unit**
- Merangkum data per produk: total qty dan total revenue per `kode_produk`
- Menghitung rata-rata belanja per pelanggan menggunakan `AVG(qty * harga)` dengan `GROUP BY kode_pelanggan`
- Mengklasifikasikan pelanggan berdasarkan total revenue menggunakan `CASE WHEN` dengan `GROUP BY`

### Contoh Query:
```sql
-- CASE WHEN untuk klasifikasi performa order
SELECT orderNumber,
       SUM(quantityOrdered * priceEach) AS total_penjualan,
       CASE
           WHEN SUM(quantityOrdered * priceEach) >= 50000 THEN 'Target Achieved'
           WHEN SUM(quantityOrdered * priceEach) <= 20000 THEN 'Less performed'
           ELSE 'Follow Up'
       END AS remark
FROM orderdetails
GROUP BY orderNumber;

-- Agregasi total revenue
SELECT SUM(qty * harga) AS total_revenue FROM ms_transaksi;

-- Rata-rata belanja per pelanggan
SELECT kode_pelanggan, AVG(qty * harga) AS rata_rata_belanja
FROM ms_transaksi GROUP BY kode_pelanggan;
```

---

## 📌 Part 6 — JOIN Tabel

**Topik:** `INNER JOIN`, relasi antar tabel, kalkulasi kolom terhitung

Part ini memperkenalkan konsep penggabungan dua tabel menggunakan `INNER JOIN` untuk menghasilkan laporan yang lebih informatif dari data yang tersebar di beberapa tabel.

### Yang dipelajari:
- Melakukan `INNER JOIN` antara tabel `tr_penjualan` dan `ms_produk` berdasarkan kolom relasi `kode_produk`
- Memahami perbedaan antara penulisan `INNER JOIN` eksplisit dan penulisan dengan koma (`FROM tr_penjualan, ms_produk`) — keduanya menghasilkan output yang setara jika kondisi JOIN dituliskan di klausa `WHERE`
- Menampilkan kolom dari dua tabel sekaligus dalam satu hasil query, termasuk: `id_transaksi`, `kode_transaksi`, `kode_pelanggan`, `kode_produk`, `nama_produk`, `qty`, `harga`
- Menghitung nilai `total` secara langsung di dalam query menggunakan ekspresi `(ms_produk.harga * tr_penjualan.qty) AS total`

### Contoh Query:
```sql
-- INNER JOIN eksplisit
SELECT *
FROM tr_penjualan
INNER JOIN ms_produk
ON tr_penjualan.kode_produk = ms_produk.kode_produk;

-- JOIN dengan kalkulasi total
SELECT tr_penjualan.kode_transaksi,
       tr_penjualan.kode_pelanggan,
       tr_penjualan.kode_produk,
       ms_produk.nama_produk,
       ms_produk.harga,
       tr_penjualan.qty,
       (ms_produk.harga * tr_penjualan.qty) AS total
FROM tr_penjualan
INNER JOIN ms_produk
ON tr_penjualan.kode_produk = ms_produk.kode_produk;
```

---

## 📌 Part 7 — JOIN Kompleks & BETWEEN

**Topik:** `JOIN` dengan filter `WHERE`, `DISTINCT`, `LIKE`, `BETWEEN`, `ORDER BY`

Part ini memperdalam penggunaan JOIN dengan menambahkan berbagai kondisi filter yang lebih kompleks, serta memperkenalkan penggunaan dua tabel terpisah yang berisi data berbeda.

### Yang dipelajari:
- Menggabungkan hasil query JOIN dengan filter `WHERE kode_pelanggan = 'polibest03'` untuk menampilkan riwayat transaksi pelanggan tertentu
- Menggunakan `SELECT DISTINCT` bersama JOIN untuk menampilkan daftar pelanggan unik yang pernah membeli produk tertentu, dengan kondisi `LIKE '%Kotak Pensil%'` atau nama produk spesifik
- Menggunakan `ORDER BY mp.kode_pelanggan` untuk mengurutkan hasil
- Memfilter produk menggunakan `BETWEEN` pada `kode_produk`: satu rentang untuk harga < 100.000 dan rentang lain untuk harga < 50.000
- Bekerja dengan dua tabel berbeda: `ms_produk_1` (produk prod-01 s/d prod-05) dan `ms_produk_2` (produk prod-06 s/d prod-10)

### Contoh Query:
```sql
-- Filter transaksi per pelanggan
SELECT kode_transaksi, kode_pelanggan, no_urut, kode_produk,
       nama_produk, qty, harga, (qty * harga) AS total
FROM tr_penjualan
WHERE kode_pelanggan = 'polibest03';

-- DISTINCT + LIKE + JOIN
SELECT DISTINCT mp.kode_pelanggan, mp.nama_customer, mp.alamat
FROM ms_pelanggan mp
JOIN tr_penjualan tp ON mp.kode_pelanggan = tp.kode_pelanggan
WHERE tp.nama_produk LIKE '%Kotak Pensil%'
   OR tp.nama_produk = 'Flashdisk 32 GB'
   OR tp.nama_produk = 'Sticky Note 500 Sheets'
ORDER BY mp.kode_pelanggan;

-- BETWEEN pada kode produk
SELECT DISTINCT nama_produk, kode_produk, harga
FROM ms_produk
WHERE (kode_produk BETWEEN 'prod-01' AND 'prod-05' AND harga < 100000)
   OR (kode_produk BETWEEN 'prod-06' AND 'prod-10' AND harga < 50000)
ORDER BY kode_produk;
```

---

## 📌 Part 8 — Eksplorasi Database Subscription

**Topik:** `DESCRIBE`, `SELECT * LIMIT`, eksplorasi struktur database nyata

Part ini beralih ke database yang lebih kompleks dan realistis — sistem **layanan subscription digital** — dengan cara mengeksplorasi struktur setiap tabel menggunakan perintah `DESCRIBE` dan melihat sampel datanya.

### Tabel-tabel yang dieksplorasi:

| Tabel | Deskripsi |
|---|---|
| `customer` | Data pelanggan (nama, alamat, gender, email, tanggal lahir, usia, kelompok usia) |
| `product` | Daftar produk digital (nama, kategori, harga, stok, deskripsi) |
| `subscription` | Langganan pelanggan terhadap produk (tanggal mulai, tanggal akhir, status) |
| `invoice` | Tagihan per langganan (tanggal invoice, jatuh tempo, total, status) |
| `payment` | Pembayaran invoice (tanggal, metode pembayaran, jumlah, status) |

### Yang dipelajari:
- Menggunakan `DESCRIBE` untuk memahami struktur tabel: nama kolom, tipe data, apakah nullable, primary key, dan foreign key
- Membaca sampel data menggunakan `SELECT * FROM ... LIMIT 5` untuk memahami isi nyata tabel
- Memahami relasi antar tabel: `customer` → `subscription` → `invoice` → `payment`
- Mengenali berbagai tipe data: `INT`, `VARCHAR`, `TEXT`, `DATETIME`, `DATE`, `DECIMAL`
- Contoh data produk: Netflix Premium (Rp 149.900), Spotify Family (Rp 79.900), YouTube Premium (Rp 89.900), Microsoft 365 Family (Rp 799.900)

### Contoh Query:
```sql
-- Melihat struktur tabel
DESCRIBE customer;
DESCRIBE product;
DESCRIBE subscription;
DESCRIBE invoice;
DESCRIBE payment;

-- Melihat sampel data
SELECT * FROM customer LIMIT 5;
SELECT * FROM product LIMIT 5;
SELECT * FROM subscription LIMIT 5;
SELECT * FROM invoice LIMIT 5;
SELECT * FROM payment LIMIT 5;
```

---

## 📌 Part 9 — Pengenalan Data CSV

**Topik:** Pengenalan format file CSV sebagai sumber data eksternal

Part ini memperkenalkan format file **CSV (Comma-Separated Values)** sebagai salah satu cara umum untuk menyimpan dan berbagi data tabular yang nantinya dapat diimpor ke dalam database.

### Yang dipelajari:
- Memahami struktur file CSV: setiap baris merepresentasikan satu record, dan setiap kolom dipisahkan oleh koma
- File CSV yang digunakan sebagai sampel memiliki kolom: `Timestamp`, `Name of person presenting`, dan `Name of project/news package`
- Mengenali bagaimana data dalam format CSV dapat diimpor ke MySQL menggunakan perintah `LOAD DATA INFILE` atau melalui tool seperti phpMyAdmin
- Memahami pentingnya data collection yang terstruktur sebagai pondasi analisis data yang akurat

### Catatan:
File CSV adalah format yang ringan, universal, dan dapat dibuka oleh hampir semua aplikasi spreadsheet maupun database. Dalam konteks basis data, CSV sering digunakan sebagai media transfer data antar sistem.

---

## 📌 Part 10 — GROUP BY, HAVING & Subquery JOIN

**Topik:** `GROUP BY`, `HAVING`, kombinasi `WHERE` + `HAVING`, `JOIN` multi-kondisi

Part ini merupakan bagian tingkat lanjut yang membahas cara menyaring hasil agregasi menggunakan `HAVING`, sekaligus menggabungkannya dengan `JOIN` dan kondisi berlapis.

### Yang dipelajari:
- Menggunakan `GROUP BY orderNumber` dan `ORDER BY orderNumber` untuk mengelompokkan dan mengurutkan data dari tabel `orderdetails`
- Menghitung `itemsCount` (total qty per order) dan `total` (nilai penjualan per order)
- Menggunakan `HAVING` untuk memfilter hasil agregasi — berbeda dari `WHERE` yang memfilter baris individual, `HAVING` memfilter hasil setelah pengelompokan:
  - `HAVING SUM(...) > 1000` — hanya tampilkan order dengan total di atas 1.000
  - `HAVING SUM(...) > 1000 AND SUM(quantityOrdered) > 600` — kombinasi dua kondisi agregat
- Menggabungkan `WHERE` (filter baris sebelum agregasi) dengan `HAVING` (filter setelah agregasi):
  - `WHERE o.status = 'Shipped'` dikombinasikan dengan `HAVING SUM(...) > 1500`
- Melakukan `JOIN` antara tabel `orders` (alias `o`) dan `orderdetails` (alias `od`) berdasarkan `orderNumber`

### Contoh Query:
```sql
-- GROUP BY dasar
SELECT orderNumber,
       SUM(quantityOrdered) AS itemsCount,
       SUM(quantityOrdered * priceEach) AS total
FROM orderdetails
GROUP BY orderNumber
ORDER BY orderNumber;

-- HAVING untuk filter agregasi
SELECT orderNumber,
       SUM(quantityOrdered) AS itemsCount,
       SUM(quantityOrdered * priceEach) AS total
FROM orderdetails
GROUP BY orderNumber
HAVING SUM(quantityOrdered * priceEach) > 1000
ORDER BY total DESC;

-- HAVING dengan dua kondisi
SELECT orderNumber,
       SUM(quantityOrdered) AS itemsCount,
       SUM(quantityOrdered * priceEach) AS total
FROM orderdetails
GROUP BY orderNumber
HAVING SUM(quantityOrdered * priceEach) > 1000
   AND SUM(quantityOrdered) > 600
ORDER BY total DESC;

-- WHERE + HAVING + JOIN
SELECT o.orderNumber, o.status,
       SUM(od.quantityOrdered * od.priceEach) AS total
FROM orders o
JOIN orderdetails od ON o.orderNumber = od.orderNumber
WHERE o.status = 'Shipped'
GROUP BY o.orderNumber, o.status
HAVING SUM(od.quantityOrdered * od.priceEach) > 1500
ORDER BY o.orderNumber;
```

---

## 🛠️ Tools & Environment

- **Database:** MySQL
- **Interface:** MySQL CLI, phpMyAdmin
- **Dataset:** DQLab store dataset, Students dataset, Orders dataset, Subscription dataset

---

## 📚 Ringkasan Konsep per Part

| Part | Konsep Utama |
|------|-------------|
| 1 | CREATE DATABASE, CREATE TABLE, INSERT, SELECT, LIMIT |
| 2 | PRIMARY KEY, Alias (AS), CONCAT, Table Alias |
| 3 | WHERE, AND, OR, Operator Perbandingan, ORDER BY |
| 4 | MOD, EXP, UPPER, LOWER, MIN, MAX |
| 5 | CASE WHEN, SUM, AVG, GROUP BY, HAVING |
| 6 | INNER JOIN, Kolom Terhitung |
| 7 | DISTINCT, LIKE, BETWEEN, JOIN Kompleks |
| 8 | DESCRIBE, Eksplorasi Tabel, Tipe Data |
| 9 | Format CSV, Import Data |
| 10 | GROUP BY, HAVING, WHERE + HAVING, JOIN Multi-tabel |

---

> 📝 **Catatan:** Seluruh tugas dikerjakan sebagai bagian dari pembelajaran mata kuliah Basis Data, dengan fokus pada penguasaan SQL untuk pengelolaan dan analisis data relasional.
