# Dashboard Taman Nasional Baluran

Halaman statis (HTML + JavaScript) dengan data karhutla di Supabase dan hosting di GitHub Pages.

## Isi folder
- `index.html` — seluruh aplikasi
- `config.js` — alamat dan kunci Supabase
- `supabase-schema.sql` — tabel dan aturan keamanan

## 1. Siapkan Supabase
1. Buat akun dan project baru di supabase.com.
2. Buka **SQL Editor**, tempel isi `supabase-schema.sql`, klik **Run**.
3. Buka **Authentication > Users > Add user**, buat akun email dan kata sandi untuk tiap petugas.
4. Buka **Authentication > Sign In / Providers** dan matikan **Allow new users to sign up**. Ini penting, karena petugas yang login boleh mengubah data.
5. Buka **Project Settings > API**, salin **Project URL** dan kunci **anon / publishable**.

## 2. Isi config.js
Tempel URL dan kunci tadi ke `config.js`. Jangan pakai kunci `service_role`.

## 3. Pasang di GitHub Pages
1. Buat repository baru di GitHub (publik).
2. Unggah ketiga file (**Add file > Upload files**) lalu commit.
3. Buka **Settings > Pages**, pilih **Deploy from a branch**, branch `main`, folder `/ (root)`, Save.
4. Setelah 1–2 menit, situs tersedia di `https://NAMA-AKUN.github.io/NAMA-REPO/`.

Setiap kali Anda mengedit file di GitHub dan commit, situs ikut diperbarui otomatis.

## Uji di komputer sendiri
```
python3 -m http.server 8000
```
lalu buka http://localhost:8000. Jika `config.js` masih kosong, aplikasi memakai mode contoh (data di peramban).

## Cara mengubah (cari di index.html)
| Yang ingin diubah | Cari |
|---|---|
| Daftar resort dan koordinatnya | `const KW=[` |
| Nama dan warna status | `const ST=[` dan variabel warna `--s1` … `--s6` di `<style>` |
| Angka tab Data dinamis (kunjungan, patroli, satwa) | `const DATA={` |
| Warna dan tema | blok `:root{` di `<style>` |
| Judul halaman | `<h1>` di `<header>` |

Nama kolom tabel ada di fungsi `fromDb` dan `toDb`. Jika Anda menambah kolom di Supabase, tambahkan juga di dua fungsi itu dan di form.

## Catatan
- Pengunjung umum hanya bisa melihat. Mengisi, mengubah, atau menghapus laporan butuh login petugas.
- Data dimuat ulang otomatis tiap 60 detik.
- Tab Data dinamis masih memakai angka contoh di kode. Agar angkanya juga dari Supabase, tambahkan tabel baru dengan pola yang sama dengan `laporan`.
