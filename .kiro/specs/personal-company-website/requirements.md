# Requirements Document

## Introduction

Website pribadi perusahaan yang menampilkan profil bos (pimpinan) dan daftar karyawan. Website dirancang dengan tampilan bersih dan sederhana menggunakan background polos (solid color), sehingga informasi personal mudah dibaca dan dipahami oleh pengunjung. Website ini berfungsi sebagai halaman profil perusahaan yang memperkenalkan tim kepada publik.

## Glossary

- **Website**: Aplikasi web yang dapat diakses melalui browser.
- **Halaman_Utama**: Halaman pertama yang ditampilkan saat pengunjung membuka website.
- **Profil_Bos**: Seksi yang menampilkan data diri pimpinan perusahaan.
- **Daftar_Karyawan**: Seksi yang menampilkan daftar seluruh karyawan perusahaan.
- **Kartu_Karyawan**: Komponen visual yang menampilkan data diri satu karyawan.
- **Background_Polos**: Latar belakang halaman menggunakan satu warna solid tanpa gambar atau pola.
- **Pengunjung**: Pengguna yang mengakses website melalui browser.
- **Admin**: Pengelola konten website yang memperbarui data profil dan karyawan.

---

## Requirements

### Requirement 1: Halaman Utama dengan Background Polos

**User Story:** Sebagai pengunjung, saya ingin melihat halaman website dengan tampilan bersih dan sederhana, sehingga saya dapat fokus membaca informasi tanpa gangguan visual.

#### Acceptance Criteria

1. THE Website SHALL menampilkan Halaman_Utama dengan Background_Polos menggunakan satu warna solid.
2. THE Website SHALL menampilkan nama perusahaan dan tagline di bagian atas Halaman_Utama.
3. THE Website SHALL menampilkan navigasi yang memuat tautan ke seksi Profil_Bos dan Daftar_Karyawan.
4. WHEN Pengunjung mengakses Halaman_Utama, THE Website SHALL memuat seluruh konten dalam waktu kurang dari 3 detik.
5. THE Website SHALL menampilkan layout yang responsif pada ukuran layar desktop (≥1024px), tablet (768px–1023px), dan mobile (≤767px).

---

### Requirement 2: Profil Bos

**User Story:** Sebagai pengunjung, saya ingin melihat data diri pimpinan perusahaan, sehingga saya dapat mengenal sosok pemimpin organisasi tersebut.

#### Acceptance Criteria

1. THE Website SHALL menampilkan seksi Profil_Bos yang memuat foto, nama lengkap, jabatan, dan deskripsi singkat bos.
2. THE Website SHALL menampilkan informasi kontak bos yang mencakup minimal satu dari: alamat email, nomor telepon, atau tautan media sosial profesional.
3. WHEN foto bos tidak tersedia, THE Website SHALL menampilkan gambar placeholder dengan inisial nama bos.
4. THE Website SHALL menampilkan Profil_Bos dengan Background_Polos yang konsisten dengan warna tema halaman.
5. THE Website SHALL menampilkan deskripsi bos dengan panjang maksimal 300 karakter pada tampilan default.

---

### Requirement 3: Daftar Karyawan

**User Story:** Sebagai pengunjung, saya ingin melihat daftar seluruh karyawan perusahaan, sehingga saya dapat mengenal anggota tim secara keseluruhan.

#### Acceptance Criteria

1. THE Website SHALL menampilkan seksi Daftar_Karyawan yang memuat Kartu_Karyawan untuk setiap karyawan.
2. THE Kartu_Karyawan SHALL menampilkan foto, nama lengkap, jabatan, dan departemen karyawan.
3. WHEN foto karyawan tidak tersedia, THE Website SHALL menampilkan gambar placeholder dengan inisial nama karyawan.
4. THE Website SHALL menampilkan Daftar_Karyawan dalam format grid dengan minimal 2 kolom pada tampilan desktop dan 1 kolom pada tampilan mobile.
5. WHEN jumlah karyawan melebihi 12 orang, THE Website SHALL menampilkan tombol "Lihat Semua" untuk memuat karyawan tambahan.
6. THE Website SHALL menampilkan total jumlah karyawan di bagian atas seksi Daftar_Karyawan.

---

### Requirement 4: Pencarian dan Filter Karyawan

**User Story:** Sebagai pengunjung, saya ingin mencari dan memfilter karyawan berdasarkan nama atau departemen, sehingga saya dapat menemukan informasi karyawan tertentu dengan cepat.

#### Acceptance Criteria

1. THE Website SHALL menampilkan kolom pencarian di bagian atas seksi Daftar_Karyawan.
2. WHEN Pengunjung mengetikkan teks pada kolom pencarian, THE Website SHALL memfilter Kartu_Karyawan yang namanya mengandung teks tersebut dalam waktu kurang dari 500ms.
3. THE Website SHALL menampilkan dropdown filter departemen yang memuat seluruh departemen yang tersedia.
4. WHEN Pengunjung memilih departemen pada dropdown filter, THE Website SHALL menampilkan hanya Kartu_Karyawan yang berasal dari departemen tersebut.
5. IF pencarian tidak menghasilkan karyawan yang cocok, THEN THE Website SHALL menampilkan pesan "Karyawan tidak ditemukan" pada seksi Daftar_Karyawan.
6. WHEN Pengunjung mengosongkan kolom pencarian, THE Website SHALL menampilkan kembali seluruh Kartu_Karyawan.

---

### Requirement 5: Tampilan Detail Karyawan

**User Story:** Sebagai pengunjung, saya ingin melihat informasi lengkap seorang karyawan, sehingga saya dapat mengetahui detail profil karyawan tersebut.

#### Acceptance Criteria

1. WHEN Pengunjung mengklik Kartu_Karyawan, THE Website SHALL menampilkan halaman atau modal detail karyawan.
2. THE Website SHALL menampilkan detail karyawan yang mencakup foto, nama lengkap, jabatan, departemen, deskripsi singkat, dan informasi kontak.
3. WHEN halaman detail karyawan ditampilkan, THE Website SHALL menggunakan Background_Polos yang konsisten dengan tema website.
4. WHEN Pengunjung menutup halaman atau modal detail karyawan, THE Website SHALL kembali menampilkan Daftar_Karyawan pada posisi scroll sebelumnya.
5. IF data detail karyawan gagal dimuat, THEN THE Website SHALL menampilkan pesan kesalahan "Data tidak dapat dimuat, silakan coba lagi".

---

### Requirement 6: Konsistensi Tema Visual

**User Story:** Sebagai pengunjung, saya ingin melihat tampilan website yang konsisten dan profesional, sehingga saya mendapatkan pengalaman visual yang nyaman.

#### Acceptance Criteria

1. THE Website SHALL menggunakan satu palet warna yang terdiri dari maksimal 3 warna utama di seluruh halaman.
2. THE Website SHALL menggunakan Background_Polos dengan warna yang sama di seluruh seksi halaman.
3. THE Website SHALL menggunakan tipografi yang konsisten dengan maksimal 2 jenis font di seluruh halaman.
4. THE Website SHALL menampilkan elemen interaktif (tombol, tautan, kartu) dengan perubahan visual yang terlihat saat Pengunjung mengarahkan kursor ke elemen tersebut (hover state).
5. THE Website SHALL memenuhi rasio kontras warna minimal 4.5:1 antara teks dan Background_Polos sesuai standar WCAG 2.1 Level AA.
