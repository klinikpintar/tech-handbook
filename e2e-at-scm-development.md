# Panduan E2E AT SCM Development
Berikut merupakan panduan dalam mengembangkan *e2e automation test* menggunakan [Codeceptjs](https://codecept.io/) dan [Monika](https://monika.hyperjump.tech/).

#### Konten:
1. Environment
2. Execution Guideline
3. Naming
4. Flow
5. Tips & Trick
6. Known Problem

---

## 1. Environment

Bagian environment [Codeceptjs](https://codecept.io/) yang wajib untuk dipahami secara berurutan antara lain:
1. Package
2. Configuration
3. Terminal Command (CLI)
4. Basic Command/Function
5. Debug
6. Retries
7. Conditional Actions
8. Multiple Sessions

Bagian environment [Monika](https://monika.hyperjump.tech/) yang wajib untuk dipahami secara berurutan antara lain:
1. Configuration
2. Terminal Command (CLI)
3. Probes
4. Alerts and Notifications
5. Debug

---
## 2. Execution Guideline

Secara default alur utama pembuatan **e2e automation test** pada platform **supply chain management** mengikuti alur umum **e2e testing** akan tetapi pendekatan *automation* pada modul yang telah dikerjakan akan diterapkan di iterasi berikutnya.

Alur pengujian dilakukan secara berurutan setiap modul dengan melengkapi kebutuhan pendekatan manual, membuat script automation, dan deploy ke server untuk dijalankan secara berkala setiap hari.

Berikut checklist pengujian yang mesti dilakukan beserta statusnya:
### Functional
Daftar teknik/pengujian:
- Unit testing
- Integration testing **(Done - Manual)**
- Smoke testing **(Done - Manual/Automation)**
- Sanity testing **(Done - Manual)**
- Regression testing **(Done - Manual/Automation)**
- Exploratory testing **(Done - Manual)**
- User acceptance testing **(Done - Manual)**

### Non Functional
Daftar teknik/pengujian:
- Load testing
- Performance testing
- Stress testing
- Security testing
- Accessibility testing

---

## 3. Naming
Masing - masing *widget/ui components* memiliki aturan dalam penamaan untuk memudahkan identifikasi & kegunaan, yakni:
- **Text/Label**: `txt_<Nama>/txt_<Nama>_<Akronim Deskripsi>` (ex: `txt_title`, `txt_count_lbl`).
- **Text Field**: `tf_<Nama>/tf_<Nama>_<Akronim Deskripsi>` (ex: `tf_email`).
- **Dropdown/Select**: `dd_<Nama>` (ex: `dd_status`).
- **Checkbox**: `cb_<Nama>` (ex: `cb_reason`).
- **Radio Button**: `rb_<Nama>` (ex: `rb_gender`).
- **Button**: `btn_<Nama>` (ex: `btn_save`).
- **Divider**: `div_<Nama>` (ex: `div_assessment`).
- **Section**: `sec_<Nama>` (ex: `sec_clinic`).
- **Table**: `tbl_<Nama>` (ex: `tbl_data`).

Untuk kasus file yang tak punya aturan penamaan, by default mengikuti aturan penamaan `<Nama Komponen>_<Nama>_<Akronim Deskripsi>`.

Selain itu, penamaan komponen dalam table/daftar, tinggal menambahkan urutan dari data yang tampil setelah penamaan komponennya.
`<Nama Komponen>_<Nama>_<Akronim Deskripsi>_<Urutan>` (ex: `txt_product_title_0`, `btn_detail_0`, `btn_edit_0`).

Selain penamaan komponen **widget/ui components**, penamaan atribut **class** pada **widget/ui components** juga memiliki aturan umum yakni:
- **Styling**: `<FontName>-<Weight>-<Size>-<Color>-<Other>` (ex: `roboto-400-16-black`, `roboto-400-16-black-italic`).
- **Margin**: `<Section/Component>-<State>` (ex: `title-primary`,`card-secondary`).
- **Other Style Attribut**: `<Custom>-<Akronim Description>` (ex: `custom-animated-hover`,`custom-sign`), menggunakan dash jika ada spasi.

Ketiga aturan tersebut dijadikan satu menggunakan format:
 `<Styling> <Margin> <Other Style Atribut>` (ex: `roboto-400-16-black card-secondary custom-animated-hover`, `roboto-400-16-black title-primary`).
 
Beberapa aturan lainnya yang perlu diperhatikan ialah:
- Jika nama terlalu panjang, bisa menggunakan akronim (ex: edit data pasien = edp).
- Hindari nama yang kompleks & panjang.
---

## 4. Flow
Alur dalam penyusunan *test script* secara *default* terdiri dari 4 alur/skenario, yakni:

**Pembacaan Data**
  - Akses halaman.
  - Pencarian data.
  - Penerapan Filter.
  - Menampilkan rincian data.
  - Mengecek komponen tampilan.
  - Mengecek data.
  - *Pagination* (opsional).

**Penambahan Data**
  - Akses halaman tambah.
  - Mengecek komponen tampilan.
  - Menambah data.

**Perubahan Data**
  - Pencarian data.
  - Akses halaman ubah.
  - Mengecek komponen tampilan.
  - Mengecek data.
  - Menyimpan data.

**Penghapusan Data**
  - Pencarian data.
  - Mengecek data.
  - Menghapus data.

Untuk alur lainnya ditambahkan dan disesuaikan dengan kebutuhan bisnis.

---

## 5. Tips & Trick
Berikut daftar saran yang sebaiknya dilakukan saat melakukan pengembangan:
1. **Duplicate before create**, sebelum membuat script baru pastikan untuk mengecek apa yang sudah ada untuk menghindari kondisi buat dari awal.
2. **Stable internet connection is a must**, untuk kesehatan mental yang lebih baik.
3. **Codeceptjs is prime suspect before your code**, bug aneh? silakan cek bagian **known problem** dan [forum curhat](https://github.com/codeceptjs/CodeceptJS/issues) terlebih dahulu.
4. **Start with small scenario**, pastikan untuk membagi scenario secara kecil untuk memudahkan debugging.
5. **Don't forget waiting time**, selalu gunakan wait untuk semua perintah crud maupun navigasi halaman.

---

## 6. Known Problem
Berikut daftar masalah yang teridentifikasi sebagai bug/anomaly/error aneh yang ditemukan dalam pengembangan:
1. Butuh waktu tunggu lebih untuk proses cud sehingga perlu diatur lebih lama (current accepted waiting time = 7-10 seconds).

Silakan tambahkan kesini jika menemukan bug/anomaly/error aneh terbaru dan tambahkan label **[Solved]** jika tidak pernah terjadi lagi atau ada pemberitahuan masalah tersebut telah diselesaikan.