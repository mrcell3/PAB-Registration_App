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

Pesan error muncul otomatis di bawah setiap field segera setelah pengguna berinteraksi dengan field tersebut — tanpa harus menekan tombol submit terlebih dahulu. Ini mencegah pengguna melewati field yang belum diisi atau diisi dengan format yang salah.

Contoh pesan error yang muncul:
- *"Nama wajib diisi"* / *"Nama minimal 3 karakter"*
- *"Email wajib diisi"* / *"Format email tidak valid"*
- *"Password wajib diisi"* / *"Password minimal 8 karakter"*
- *"Pilih program studi"*
- *"Tanggal lahir wajib diisi"*

---

### 3. Date Picker

Saat field **Tanggal Lahir** ditekan, muncul dialog kalender interaktif bawaan Flutter. Pengguna dapat menavigasi bulan dan tahun untuk memilih tanggal lahir. Kalender dibatasi antara tahun **1990** hingga **hari ini**, sehingga tidak bisa memilih tanggal yang tidak logis.

Kalender langsung terbuka di tanggal **1 Januari 2004** sebagai titik awal yang relevan untuk mahasiswa. Setelah dipilih, tanggal akan otomatis terisi ke dalam field dengan format yang sudah diformat, contoh: *1 Januari 2004*.

---

### 4. Dialog Registrasi Berhasil

Setelah semua field terisi dengan benar dan tombol **DAFTAR SEKARANG** ditekan, muncul dialog konfirmasi yang menampilkan nama peserta yang baru saja terdaftar. Dialog ini muncul di atas halaman form (form tidak tertutup).

Terdapat dua pilihan aksi:
- **Daftar Lagi** — menutup dialog dan mereset seluruh form ke kondisi kosong
- **Lihat Daftar** — menutup dialog dan langsung menuju halaman Daftar Peserta

---

### 5. Halaman Daftar Peserta

Menampilkan seluruh peserta yang sudah berhasil mendaftar dalam bentuk list kartu. Jumlah peserta ditampilkan secara dinamis pada judul halaman, misalnya *"Daftar Peserta (1)"*.

Setiap item di list menampilkan:
- **Avatar** — lingkaran dengan inisial huruf pertama nama peserta
- **Nama lengkap** peserta
- **Program studi** dan **email** sebagai subtitle
- **Ikon hapus** (merah) di sisi kanan untuk menghapus peserta

---

### 6. Dialog Konfirmasi Hapus

Ketika ikon hapus (🗑️) ditekan, muncul dialog konfirmasi sebelum data benar-benar dihapus. Ini mencegah pengguna kehilangan data secara tidak sengaja karena salah tekan.

Dialog menampilkan nama peserta yang akan dihapus dan dua tombol:
- **Batal** — menutup dialog tanpa menghapus data
- **Hapus** (merah) — menghapus data dan otomatis memperbarui list

---

### 7. Halaman Detail Peserta

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
| `TextFormField` | Nama, Email, Password, Tanggal Lahir | Input teks terintegrasi dengan `Form`, mendukung validasi dan controller |
| `RadioListTile` | Jenis Kelamin | Pilihan tunggal dari beberapa opsi; semua radio berbagi `groupValue` yang sama |
| `DropdownButtonFormField` | Program Studi | Dropdown terintegrasi `Form` untuk memilih satu opsi dari daftar tetap |
| `CheckboxListTile` | Syarat & Ketentuan | Kombinasi `Checkbox` + `ListTile`; menampilkan centang beserta judul dan subjudul |
| `showDatePicker` | Tanggal Lahir | Fungsi bawaan Flutter yang membuka dialog kalender; mengembalikan `Future<DateTime?>` |
| `Form` | Registration Page | Container untuk mengelompokkan field dan mengontrol validasi secara serentak |
| `Consumer<T>` | AppBar Badge, List Page | Me-rebuild hanya bagian yang dibungkus saat state Provider berubah |
| `Badge` | AppBar (ikon peserta) | Menampilkan notifikasi angka kecil di atas widget lain |
| `AlertDialog` | Sukses registrasi, Konfirmasi hapus | Dialog modal di atas halaman untuk notifikasi dan konfirmasi |
| `ListView.builder` | Registrant List Page | Render daftar secara *lazy* — hanya item yang terlihat di layar yang dibuat |
| `CircleAvatar` | List Page, Detail Page | Avatar lingkaran berisi inisial nama pendaftar |
| `SnackBar` | Validasi tambahan | Notifikasi singkat di bawah layar untuk pesan error non-field |

---

## 🔧 Konsep Utama yang Digunakan

| Konsep | Digunakan Di | Fungsi |
|--------|-------------|--------|
| `ChangeNotifier` + `notifyListeners()` | Provider | Memberitahu widget untuk rebuild saat data berubah |
| `Consumer<T>` | List Page, AppBar | Widget yang rebuild otomatis saat Provider update |
| `context.read<T>()` | Submit form, Detail page | Membaca Provider tanpa subscribe rebuild |
| `GlobalKey<FormState>` | Registration Page | Mengontrol validasi seluruh form sekaligus |
| `TextEditingController` | Semua field teks | Membaca dan mengatur nilai input field |
| `ListView.builder` | List Page | Render item secara lazy, efisien untuk list panjang |
| `Navigator.pushNamed` | Semua halaman | Navigasi antar halaman menggunakan named route |

---