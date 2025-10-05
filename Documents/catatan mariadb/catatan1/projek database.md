## Catatan penting 
## A. buat ngehapus database yang telah di buat; 

## Step by step: 
- SHOW DATABASES;
- DROP DATABASE (nama database kalian) 



## 1. MEMBUAT DATABASE PERTAMA

```
CREATE DATABASE nama data base kalian
DEFAULT CHARACTER SET utf8mb4
COLLATE utf8mb4_general_ci; 
```

## 2.  memilih database yang telah dibuat
```
use nama database;
```

## Kode tambahan 

```
show databases; (melihat database yang dibuat)

select database(); (melihat database yg dipilih)

```

## 3. Membuat table anggota

```
create table anggota (
id_anggota int primary key auto_increment
nama varchar (100),
alamat varchar (150),
no_telepon (20)
);
```

## Penjelasan setiap tipe data 

```
`id_anggota` menggunakan INT dengan AUTO\_INCREMENT agar setiap baris unik.
```

```
nama` dan `alamat` menggunakan VARCHAR untuk fleksibilitas teks.
```

```
Sementara nomor telepon disimpan sebagai VARCHAR agar tidak kehilangan angka nol di depan.
```

## 4. Membuat table buku
```
create table buku (
id_buku int primary key auto_increment,
judul varchar (150) not null,
penulis varchar (100),
tahun_terbit year,
isbn varchar (20) unique
);
```

## 5. membuat tabel peminjaman 
```
create table peminjaman (
id_peminjaman int primary key auto_increment,
id_anggota int not null,
id_buku int not null,
tahun_terbit year, 
isbn varchar(20) unique
);
```

## 6. menambahkan data buku
```
INSERT INTO buku (judul, penulis, tahun_terbit, isbn) VALUES
('Statistik untuk Sains', 'Teguh Prasetyo', 2015, '9786023211111'),
('Kecerdasan Buatan', 'Nur Aisyah', 2021, '9786023212222'),
('Dasar Pemrograman Web', 'Indra Kusuma', 2018, '9786023213333');
```


## penjelasan setiap perintah 

```
'insert' digunakan untuk menambahkan baris data baru ke dalam tabel. biasanya di barengi dengan perintah 'into'. seperti yang diatas
```


## 7. melihat isi semua isi tabel 

```
select * from buku; (jika ingin melihat tabel buku)

select * from anggota; (jika ingin melihat tabel anggota)

select * from peminjaman; (jika ingin melihat tabel peminjaman)
```


## Format perintah yang lebih rapih melihat sebagian isi tabel
```
SELECT judul, penulis FROM buku;
```

## Format perintah menggunakan alias untuk tabel lebih spesifik
```
select judul as "judul buku", penulis as "nama penulis" from buku;
```

## Format perintah untuk membatasi hasil tabel

```
select * from buku limit 5;
```

## Perintah melihat struktur tabel untuk melihat kolom beserta tipe datanya.
```
describe anggota; (melihat struktur anggota)

describe peminjaman; (melihat strutktur peminjaman)

describe buku; (melihat struktur buku)
```

## Perintah UPDATE untuk memperbarui nilai satu atau lebih kolom dalam tabel

```
UPDATE buku SET penulis = 'Joko Purnomo' WHERE id_buku = 1;
```

Perintah di atas akan mengubah kolom `penulis` hanya untuk baris dengan `id_buku = 1`. Kolom lainnya tetap tidak berubah. Hal ini memperlihatkan betapa pentingnya klausa `WHERE` dalam menjaga ketepatan perubahan.

## Perintah dasar DELETE

Kata kunci `WHERE` sangat penting karena menentukan baris mana yang akan dihapus. Tanpa `WHERE`, semua baris dalam tabel akan hilang. Misalnya, untuk menghapus satu buku dengan `id_buku = 5`, query yang digunakan adalah:

```
DELETE FROM buku WHERE id_buku = 5;
```

Selain menghapus satu baris, perintah ini juga dapat digunakan untuk menghapus lebih dari satu baris sekaligus. misal menghapus semua buku yang terbit sebelum tahun 2000:

```
DELETE FROM buku WHERE tahun_terbit < 2000;
```

Perintah `DELETE` memungkinkan pengguna menghapus banyak baris sekaligus dengan menggunakan kondisi tertentu. Misalnya, jika perpustakaan ingin menghapus semua buku yang tidak memiliki ISBN (kosong), maka query yang digunakan adalah:

```
DELETE FROM buku WHERE isbn IS NULL;
```

## Perintah membatalkan baris yang sudah di hapus sebelumnya

```
START TRANSACTION;
DELETE FROM buku WHERE tahun_terbit < 1990;
ROLLBACK;
```

## Sebelum menghapus lakukan backup pada buku 

```
CREATE TABLE buku_backup AS SELECT * FROM buku;
```

## Perintah memeriksa data 
```
SELECT '9786021110009' NOT IN (SELECT isbn FROM buku) AS is_unique;
```

```
SELECT * FROM buku WHERE judul = 'Data Mining';
```

## Jika ingin memilih daftar buku a sampai z

```
select judul, tahun_terbit from buku order by tahun_terbit asc;
```

## Jika ingin sebaliknya 

```
select judul, tahun_terbit from buku order by tahun_terbit desc;
```

## menambahkan buku yang akan di pinjam oleh member perpus
```
INSERT INTO peminjaman (id_anggota, id_buku, tanggal_pinjam) VALUES
(1, 10, '2025-02-03'),
(2, 5, '2025-02-04');
```
## 8. Menambahkan member perpustakaan kedalam table anggota

```
INSERT INTO anggota (nama, alamat, tanggal_daftar)
VALUES ('Sinta Dewi', 'Jl. Anggrek No. 7', '2025-02-01');
```

## 9. dalam kasus yang sama membuat table peminjaman dengan menghubungkannya ke table anggota menggunakan foreign key 

```
CREATE TABLE peminjaman (
id_peminjaman INT AUTO_INCREMENT PRIMARY KEY,
id_anggota INT,
id_buku INT,
tanggal_pinjam DATE,
FOREIGN KEY (id_anggota) REFERENCES anggota(id_anggota)
);
```

## 10. Kalo pengen ngeliat data nama yang udah minjem saja 

```
SELECT a.nama, b.judul, p.tanggal_pinjam
FROM anggota a
INNER JOIN peminjaman p ON a.id_anggota = p.id_anggota
INNER JOIN buku b ON p.id_buku = b.id_buku;
```

## ht
