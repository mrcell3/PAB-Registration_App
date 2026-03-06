# Nama : Marcela Persa Linthin
# Nim  : 2409116072

---

# 📋 Registrasi Event App

Aplikasi Flutter untuk manajemen pendaftaran event dengan fitur form registrasi, daftar peserta, dan halaman detail. Dibangun menggunakan Provider sebagai state management.

---

## 📱 Tampilan Aplikasi

### 1. Halaman Form Pendaftaran


Halaman utama yang pertama kali muncul saat aplikasi dibuka. Berisi form lengkap yang harus diisi oleh calon peserta sebelum bisa mendaftar. Di bagian AppBar terdapat ikon dengan **badge angka** yang menunjukkan jumlah peserta yang sudah terdaftar secara real-time.

Elemen yang tampil di halaman ini:
- Field **Nama Lengkap** — input teks biasa
- Field **Email** — keyboard otomatis beralih ke mode email
- Field **Password** — karakter disembunyikan, ada tombol toggle tampilkan/sembunyikan
- Pilihan **Jenis Kelamin** — dua opsi radio: Laki-laki / Perempuan
- Dropdown **Program Studi** — memilih dari 5 pilihan prodi
- Field **Tanggal Lahir** — menampilkan dialog kalender saat ditekan
- Checkbox **Syarat & Ketentuan** — wajib dicentang sebelum submit
- Tombol **DAFTAR SEKARANG** dan **Reset Form**

---

### 2. Validasi Form

<img width="744" height="948" alt="Screenshot 2026-03-06 125628" src="https://github.com/user-attachments/assets/f79ff07b-0eef-4dd2-9937-94dfe7aaa0e9" />

Pesan error muncul otomatis di bawah setiap field segera setelah pengguna berinteraksi dengan field tersebut — tanpa harus menekan tombol submit terlebih dahulu. Ini mencegah pengguna melewati field yang belum diisi atau diisi dengan format yang salah.

Contoh pesan error yang muncul:
- *"Nama wajib diisi"* / *"Nama minimal 3 karakter"*
- *"Email wajib diisi"* / *"Format email tidak valid"*
- *"Password wajib diisi"* / *"Password minimal 8 karakter"*
- *"Pilih program studi"*
- *"Tanggal lahir wajib diisi"*

---

### 3. Date Picker

<img width="748" height="947" alt="Screenshot 2026-03-06 131008" src="https://github.com/user-attachments/assets/e6581f8b-05c8-4348-bca5-ad0226c656ec" />

Saat field **Tanggal Lahir** ditekan, muncul dialog kalender interaktif bawaan Flutter. Pengguna dapat menavigasi bulan dan tahun untuk memilih tanggal lahir. Kalender dibatasi antara tahun **1990** hingga **hari ini**, sehingga tidak bisa memilih tanggal yang tidak logis.

Kalender langsung terbuka di tanggal **1 Januari 2004** sebagai titik awal yang relevan untuk mahasiswa. Setelah dipilih, tanggal akan otomatis terisi ke dalam field dengan format yang sudah diformat, contoh: *1 Januari 2004*.

---

### 4. Dialog Registrasi Berhasil

<img width="746" height="889" alt="Screenshot 2026-03-06 131118" src="https://github.com/user-attachments/assets/d0fe3095-d7c9-428c-9c36-4c497d2ebe1a" />

Setelah semua field terisi dengan benar dan tombol **DAFTAR SEKARANG** ditekan, muncul dialog konfirmasi yang menampilkan nama peserta yang baru saja terdaftar. Dialog ini muncul di atas halaman form (form tidak tertutup).

Terdapat dua pilihan aksi:
- **Daftar Lagi** — menutup dialog dan mereset seluruh form ke kondisi kosong
- **Lihat Daftar** — menutup dialog dan langsung menuju halaman Daftar Peserta

---

### 5. Halaman Daftar Peserta

<img width="746" height="948" alt="Screenshot 2026-03-06 125831" src="https://github.com/user-attachments/assets/c2efe814-6100-40ac-8e16-2a7fed6f54cc" />

Menampilkan seluruh peserta yang sudah berhasil mendaftar dalam bentuk list kartu. Jumlah peserta ditampilkan secara dinamis pada judul halaman, misalnya *"Daftar Peserta (1)"*.

Setiap item di list menampilkan:
- **Avatar** — lingkaran dengan inisial huruf pertama nama peserta
- **Nama lengkap** peserta
- **Program studi** dan **email** sebagai subtitle
- **Ikon hapus** (merah) di sisi kanan untuk menghapus peserta

---

### 6. Dialog Konfirmasi Hapus

<img width="747" height="946" alt="Screenshot 2026-03-06 132053" src="https://github.com/user-attachments/assets/8df3eecc-cdd0-41cd-b116-5a462b16c419" />

Ketika ikon hapus (🗑️) ditekan, muncul dialog konfirmasi sebelum data benar-benar dihapus. Ini mencegah pengguna kehilangan data secara tidak sengaja karena salah tekan.

Dialog menampilkan nama peserta yang akan dihapus dan dua tombol:
- **Batal** — menutup dialog tanpa menghapus data
- **Hapus** (merah) — menghapus data dan otomatis memperbarui list

---

### 7. Halaman Detail Peserta

<img width="747" height="947" alt="Screenshot 2026-03-06 131154" src="https://github.com/user-attachments/assets/65b98969-f370-4dcf-95bb-85174de1b63b" />

Muncul saat pengguna mengetuk salah satu item di daftar peserta. Menampilkan semua informasi peserta secara lengkap dalam bentuk kartu-kartu info yang rapi.

Informasi yang ditampilkan:
- **Avatar besar** dengan inisial nama di tengah halaman
- **Nama lengkap** dan waktu registrasi
- Kartu **Email**
- Kartu **Jenis Kelamin**
- Kartu **Program Studi**
- Kartu **Tanggal Lahir** beserta **usia** yang dihitung otomatis, contoh: *1 Jan 2004 (22 tahun)*

---

### 8. Empty State — Belum Ada Peserta

<img width="745" height="946" alt="Screenshot 2026-03-06 125537" src="https://github.com/user-attachments/assets/a3157c85-b7b4-40b1-85b4-93a3f7e739e0" />

Jika belum ada peserta yang terdaftar (atau semua sudah dihapus), halaman daftar menampilkan tampilan kosong yang informatif agar pengguna tidak bingung. Terdapat ikon besar, teks *"Belum ada pendaftar"*, dan ajakan untuk segera mendaftar.

---

## 🗂️ Struktur Project

```
lib/
├── models/
│   └── registrant_model.dart       
├── providers/
│   └── registration_provider.dart  
├── pages/
│   ├── registration_page.dart      
│   ├── registrant_list_page.dart   
│   └── registrant_detail_page.dart 
└── main.dart                       
```

---

## 🧩 Penjelasan Widget

| Widget | Digunakan Di | Fungsi |
|--------|-------------|--------|
| `TextFormField` | Nama, Email, Password, Tanggal Lahir | Kotak isian teks untuk pengguna mengetik data |
| `RadioListTile` | Jenis Kelamin | Tombol pilihan bulat — hanya satu yang bisa dipilih dalam satu waktu |
| `DropdownButtonFormField` | Program Studi | Menu pilihan yang muncul ke bawah saat ditekan |
| `CheckboxListTile` | Syarat & Ketentuan | Kotak centang dengan label di sampingnya |
| `showDatePicker` | Tanggal Lahir | Membuka dialog kalender agar pengguna bisa memilih tanggal |
| `Form` | Registration Page | Pembungkus semua field agar validasinya bisa dicek sekaligus |
| `Consumer<T>` | AppBar Badge, List Page | Memantau perubahan data dan otomatis memperbarui tampilan yang terkait |
| `Badge` | AppBar (ikon peserta) | Angka kecil di atas ikon yang menunjukkan jumlah peserta terdaftar |
| `AlertDialog` | Sukses registrasi, Konfirmasi hapus | Kotak pop-up di tengah layar untuk menampilkan pesan atau meminta konfirmasi |
| `ListView.builder` | Registrant List Page | Menampilkan daftar item secara berurutan ke bawah, efisien untuk data banyak |
| `CircleAvatar` | List Page, Detail Page | Avatar lingkaran berisi inisial nama peserta |
| `SnackBar` | Validasi tambahan | Notifikasi singkat di bawah layar untuk pesan error non-field |

---

## 🔧 Konsep Utama yang Digunakan

| Konsep | Digunakan Di | Fungsi |
|--------|-------------|--------|
| `ChangeNotifier` + `notifyListeners()` | Provider | Memberitahu widget untuk rebuild saat data berubah |
| `Consumer<T>` | List Page, AppBar | Widget yang rebuild otomatis saat Provider update |
| `context.read<T>()` | Submit form, Detail page | Mengambil data dari Provider satu kali tanpa terus-menerus memantau perubahannya |
| `GlobalKey<FormState>` | Registration Page | Mengontrol validasi seluruh form sekaligus |
| `TextEditingController` | Semua field teks | Membaca dan mengatur nilai input field |
| `ListView.builder` | List Page | Menampilkan daftar panjang secara hemat — item hanya dibuat saat benar-benar terlihat di layar |
| `Navigator.pushNamed` | Semua halaman | Berpindah ke halaman lain menggunakan nama route yang sudah didaftarkan di `main.dart` |

---
