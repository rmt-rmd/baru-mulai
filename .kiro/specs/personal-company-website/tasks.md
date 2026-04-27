# Implementation Tasks

## Personal Company Website

---

## Task Overview

- [ ] 1. Setup Proyek dan Konfigurasi
- [ ] 2. Data Layer dan Utilitas
- [ ] 3. Komponen Dasar (Avatar, Header)
- [ ] 4. Seksi Profil Bos
- [ ] 5. Seksi Daftar Karyawan
- [ ] 6. Pencarian dan Filter Karyawan
- [ ] 7. Modal Detail Karyawan
- [ ] 8. Tema Visual dan Konsistensi
- [ ] 9. Property-Based Tests
- [ ] 10. Unit Tests dan Integration Tests

---

## Task 1: Setup Proyek dan Konfigurasi

- [x] 1.1 Inisialisasi proyek React dengan Vite (`npm create vite@latest`)
- [-] 1.2 Install dependensi: `react`, `react-dom`, `vitest`, `@testing-library/react`, `@testing-library/user-event`, `@testing-library/jest-dom`, `fast-check`, `jsdom`
- [~] 1.3 Konfigurasi Vitest di `vitest.config.js` dengan environment jsdom
- [~] 1.4 Buat struktur folder sesuai desain: `src/components/`, `src/services/`, `src/utils/`, `src/data/`, `src/styles/`
- [~] 1.5 Buat file `src/styles/theme.css` dengan CSS Variables untuk warna, font, dan spacing
- [~] 1.6 Buat file data contoh `src/data/boss.json` dan `src/data/employees.json` dengan minimal 15 karyawan dari berbagai departemen

---

## Task 2: Data Layer dan Utilitas

- [~] 2.1 Buat `src/services/dataService.js` dengan fungsi `fetchBossData()` dan `fetchEmployeesData()` yang membaca dari JSON lokal
- [~] 2.2 Buat `src/utils/avatarUtils.js` dengan fungsi `getInitials(name: string): string`
  - Mengambil huruf pertama setiap kata, maksimal 2 karakter
  - Mengembalikan string huruf kapital
  - Menangani nama kosong dengan mengembalikan string kosong
- [~] 2.3 Buat `src/utils/filterUtils.js` dengan fungsi:
  - `filterByName(employees, query)`: filter case-insensitive berdasarkan nama
  - `filterByDepartment(employees, dept)`: filter berdasarkan departemen
  - `getUniqueDepartments(employees)`: mengembalikan array departemen unik, diurutkan
- [~] 2.4 Buat `src/utils/colorUtils.js` dengan fungsi:
  - `getContrastRatio(color1, color2)`: menghitung rasio kontras WCAG
  - `meetsWCAGAA(textColor, bgColor)`: mengembalikan true jika rasio ≥ 4.5
- [~] 2.5 Buat `src/utils/textUtils.js` dengan fungsi `truncateText(text, maxLength)` yang memotong teks dan menambahkan `...`

---

## Task 3: Komponen Dasar

- [~] 3.1 Buat komponen `<Avatar name photoUrl size />` di `src/components/Avatar/`
  - Tampilkan `<img>` jika `photoUrl` tersedia
  - Tampilkan inisial dari `getInitials(name)` jika `photoUrl` null
  - Handle `onError` pada `<img>` untuk fallback ke inisial
  - Support ukuran: `sm` (32px), `md` (64px), `lg` (96px)
  - Styling dengan CSS Modules, background warna aksen, teks kontras
- [~] 3.2 Buat komponen `<Header />` di `src/components/Header/`
  - Tampilkan nama perusahaan (dari konstanta atau props)
  - Tampilkan tagline perusahaan
  - Tampilkan navigasi dengan tautan anchor ke `#boss-profile` dan `#employee-list`
  - Responsif: hamburger menu pada mobile
  - Smooth scroll saat tautan navigasi diklik
- [~] 3.3 Buat komponen `<ErrorBoundary fallback />` di `src/components/ErrorBoundary/`
  - Class component dengan `componentDidCatch`
  - Render `fallback` prop saat terjadi error

---

## Task 4: Seksi Profil Bos

- [~] 4.1 Buat komponen `<BossProfile boss />` di `src/components/BossProfile/`
  - Tampilkan `<Avatar>` ukuran `lg` dengan foto atau inisial bos
  - Tampilkan nama lengkap, jabatan
  - Tampilkan deskripsi yang di-truncate ke 300 karakter dengan tombol "Selengkapnya" jika lebih panjang
  - Tampilkan informasi kontak (email, telepon, LinkedIn, Twitter) — minimal satu harus ada
  - Gunakan background polos sesuai tema
  - Tambahkan `id="boss-profile"` untuk anchor navigasi
- [~] 4.2 Integrasikan `<BossProfile>` ke `App.jsx` dengan data dari `dataService`
- [~] 4.3 Tambahkan loading state saat data bos sedang dimuat
- [~] 4.4 Tambahkan error state dengan pesan "Data tidak dapat dimuat, silakan coba lagi" jika fetch gagal

---

## Task 5: Seksi Daftar Karyawan (Tampilan Dasar)

- [~] 5.1 Buat komponen `<EmployeeCard employee onClick />` di `src/components/EmployeeCard/`
  - Tampilkan `<Avatar>` ukuran `md` dengan foto atau inisial karyawan
  - Tampilkan nama lengkap, jabatan, departemen
  - Hover state: perubahan visual (shadow, border, atau background)
  - Cursor pointer, accessible dengan keyboard (Enter/Space untuk klik)
- [~] 5.2 Buat komponen `<EmployeeList employees />` di `src/components/EmployeeList/`
  - Tampilkan total jumlah karyawan di bagian atas (`X Karyawan`)
  - Render grid `<EmployeeCard>` untuk setiap karyawan
  - Grid: 3 kolom desktop, 2 kolom tablet, 1 kolom mobile (CSS Grid)
  - Tampilkan hanya 12 karyawan pertama secara default
  - Tampilkan tombol "Lihat Semua" jika total karyawan > 12
  - Tambahkan `id="employee-list"` untuk anchor navigasi
- [~] 5.3 Integrasikan `<EmployeeList>` ke `App.jsx` dengan data dari `dataService`
- [~] 5.4 Tambahkan loading state dan error state pada `<EmployeeList>`

---

## Task 6: Pencarian dan Filter Karyawan

- [~] 6.1 Buat komponen `<SearchBar value onChange placeholder />` di `src/components/SearchBar/`
  - Input teks dengan ikon pencarian
  - Debounce input 300ms untuk performa
  - Tombol clear (×) yang muncul saat ada teks
  - Accessible: label, aria-label
- [~] 6.2 Buat komponen `<DepartmentFilter departments value onChange />` di `src/components/DepartmentFilter/`
  - Dropdown `<select>` dengan opsi "Semua Departemen" sebagai default
  - Populate opsi dari array `departments` yang diterima via props
  - Accessible: label, aria-label
- [~] 6.3 Integrasikan `<SearchBar>` dan `<DepartmentFilter>` ke dalam `<EmployeeList>`
  - State: `searchQuery` (string), `selectedDepartment` (string)
  - Terapkan `filterByName()` dan `filterByDepartment()` dari `filterUtils`
  - Hitung `uniqueDepartments` dari `getUniqueDepartments(employees)` untuk props `<DepartmentFilter>`
  - Tampilkan pesan "Karyawan tidak ditemukan" jika hasil filter kosong
  - Reset ke tampilkan semua saat `searchQuery` dikosongkan

---

## Task 7: Modal Detail Karyawan

- [~] 7.1 Buat komponen `<EmployeeDetailModal employee onClose />` di `src/components/EmployeeDetailModal/`
  - Render `null` jika `employee` adalah `null`
  - Overlay gelap semi-transparan di belakang modal
  - Tampilkan `<Avatar>` ukuran `lg`, nama, jabatan, departemen, deskripsi, kontak
  - Tombol tutup (×) di pojok kanan atas
  - Tutup modal saat overlay diklik atau tombol Escape ditekan
  - Background polos konsisten dengan tema
  - Accessible: `role="dialog"`, `aria-modal="true"`, focus trap
- [~] 7.2 Integrasikan modal ke `<EmployeeList>`
  - State: `selectedEmployee` (Employee | null)
  - Set `selectedEmployee` saat `<EmployeeCard>` diklik
  - Set `selectedEmployee = null` saat modal ditutup
  - Simpan posisi scroll sebelum modal dibuka, kemudian restore saat modal ditutup
- [~] 7.3 Tambahkan error state pada modal jika data detail gagal dimuat

---

## Task 8: Tema Visual dan Konsistensi

- [~] 8.1 Finalisasi `src/styles/theme.css` dengan CSS Variables:
  - `--color-background`: warna background polos utama
  - `--color-primary`: warna utama
  - `--color-accent`: warna aksen
  - `--color-text`: warna teks utama
  - `--color-text-secondary`: warna teks sekunder
  - `--font-primary`: font utama
  - `--font-secondary`: font sekunder (opsional)
  - Pastikan maksimal 3 warna utama dan 2 jenis font
- [~] 8.2 Verifikasi rasio kontras semua pasangan warna teks/background menggunakan `colorUtils.getContrastRatio()` — semua harus ≥ 4.5:1
- [~] 8.3 Pastikan semua komponen menggunakan `var(--color-background)` yang sama untuk background
- [~] 8.4 Tambahkan hover state pada semua elemen interaktif: `<EmployeeCard>`, tombol, tautan navigasi
- [~] 8.5 Verifikasi responsivitas di tiga breakpoint: desktop (≥1024px), tablet (768–1023px), mobile (≤767px)
- [~] 8.6 Tambahkan `<meta name="viewport">` dan pastikan tidak ada horizontal scroll pada mobile

---

## Task 9: Property-Based Tests

- [~] 9.1 Buat file `src/utils/__tests__/avatarUtils.test.js`
  - **[PBT] Property 1**: `getInitials(name)` — for any non-empty string, hasil harus berupa huruf kapital, panjang 1–2 karakter
  - Tag: `// Feature: personal-company-website, Property 1: Inisial Avatar Selalu Benar`
  - Konfigurasi: `{ numRuns: 100 }`

- [~] 9.2 Buat file `src/utils/__tests__/textUtils.test.js`
  - **[PBT] Property 2**: `truncateText(text, 300)` — for any string, hasil tidak boleh melebihi 300 karakter
  - Tag: `// Feature: personal-company-website, Property 2: Truncation Deskripsi Bos`
  - Konfigurasi: `{ numRuns: 100 }`

- [~] 9.3 Buat file `src/utils/__tests__/filterUtils.test.js`
  - **[PBT] Property 6**: `filterByName(employees, query)` — for any employees array dan query, semua hasil mengandung query di nama (case-insensitive), tidak ada yang terlewat
  - Tag: `// Feature: personal-company-website, Property 6: Filter Nama Hanya Menampilkan Hasil yang Cocok`
  - **[PBT] Property 7**: `getUniqueDepartments(employees)` — for any employees array, hasil adalah himpunan departemen unik yang tepat
  - Tag: `// Feature: personal-company-website, Property 7: Dropdown Departemen Mencakup Semua Departemen`
  - **[PBT] Property 8**: `filterByDepartment(employees, dept)` — for any employees array dan dept, semua hasil memiliki departemen yang sama dengan dept
  - Tag: `// Feature: personal-company-website, Property 8: Filter Departemen Hanya Menampilkan Departemen yang Dipilih`
  - **[PBT] Property 9**: `filterByName(employees, "")` — for any employees array, filter dengan query kosong mengembalikan semua karyawan
  - Tag: `// Feature: personal-company-website, Property 9: Reset Pencarian Mengembalikan Semua Karyawan`
  - Konfigurasi: `{ numRuns: 100 }` untuk setiap properti

- [~] 9.4 Buat file `src/utils/__tests__/colorUtils.test.js`
  - **[PBT] Property 11**: `getContrastRatio(color1, color2)` — for any pasangan warna tema, rasio ≥ 4.5
  - Tag: `// Feature: personal-company-website, Property 11: Rasio Kontras Warna Memenuhi WCAG AA`
  - Konfigurasi: `{ numRuns: 100 }`

- [~] 9.5 Buat file `src/components/EmployeeList/__tests__/EmployeeList.pbt.test.jsx`
  - **[PBT] Property 3**: for any array N karyawan, render tepat N kartu dengan nama, jabatan, departemen yang benar
  - Tag: `// Feature: personal-company-website, Property 3: Kartu Karyawan Lengkap`
  - **[PBT] Property 4**: for any array karyawan, tombol "Lihat Semua" muncul iff jumlah > 12
  - Tag: `// Feature: personal-company-website, Property 4: Tombol Lihat Semua Sesuai Threshold`
  - **[PBT] Property 5**: for any array N karyawan, angka total yang ditampilkan = N
  - Tag: `// Feature: personal-company-website, Property 5: Total Karyawan Akurat`
  - Konfigurasi: `{ numRuns: 100 }` untuk setiap properti

- [~] 9.6 Buat file `src/components/EmployeeDetailModal/__tests__/EmployeeDetailModal.pbt.test.jsx`
  - **[PBT] Property 10**: for any employee object valid, detail view menampilkan nama, jabatan, departemen, deskripsi, dan kontak
  - Tag: `// Feature: personal-company-website, Property 10: Detail Karyawan Menampilkan Semua Field`
  - Konfigurasi: `{ numRuns: 100 }`

---

## Task 10: Unit Tests dan Integration Tests

- [~] 10.1 Buat `src/components/Header/__tests__/Header.test.jsx`
  - Menampilkan nama perusahaan dan tagline
  - Navigasi memiliki tautan ke `#boss-profile` dan `#employee-list`

- [~] 10.2 Buat `src/components/Avatar/__tests__/Avatar.test.jsx`
  - Menampilkan `<img>` saat `photoUrl` tersedia
  - Menampilkan inisial saat `photoUrl` null
  - Fallback ke inisial saat `<img>` error
  - Menampilkan ukuran yang benar (sm, md, lg)

- [~] 10.3 Buat `src/components/BossProfile/__tests__/BossProfile.test.jsx`
  - Menampilkan semua field yang diperlukan (nama, jabatan, deskripsi, kontak)
  - Deskripsi di-truncate ke 300 karakter
  - Menampilkan placeholder avatar saat foto tidak ada
  - Menampilkan minimal satu informasi kontak

- [~] 10.4 Buat `src/components/EmployeeCard/__tests__/EmployeeCard.test.jsx`
  - Menampilkan nama, jabatan, departemen
  - Memanggil `onClick` saat diklik
  - Memanggil `onClick` saat Enter/Space ditekan (keyboard accessibility)

- [~] 10.5 Buat `src/components/EmployeeList/__tests__/EmployeeList.test.jsx`
  - Menampilkan pesan "Karyawan tidak ditemukan" saat pencarian tidak ada hasil
  - Menampilkan 12 karyawan pertama secara default
  - Menampilkan semua karyawan setelah tombol "Lihat Semua" diklik
  - Filter nama bekerja dengan benar (contoh spesifik)
  - Filter departemen bekerja dengan benar (contoh spesifik)

- [~] 10.6 Buat `src/components/EmployeeDetailModal/__tests__/EmployeeDetailModal.test.jsx`
  - Modal tidak render saat `employee` null
  - Modal render saat `employee` tersedia
  - Memanggil `onClose` saat tombol × diklik
  - Memanggil `onClose` saat overlay diklik
  - Memanggil `onClose` saat tombol Escape ditekan
  - Menampilkan pesan error saat data gagal dimuat

- [~] 10.7 Verifikasi semua test lulus dengan menjalankan `npx vitest --run`
