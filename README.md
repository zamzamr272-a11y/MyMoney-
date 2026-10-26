# My Money — Safari iPhone / Web PWA

Versi web baru My Money yang dirancang mobile-first, dengan nuansa UI hijau-putih dari konsep desain. Website ini dapat dibuka di Safari iPhone dan ditambahkan ke Home Screen sehingga terasa seperti aplikasi.

## Panduan langkah demi langkah

Baca [`PANDUAN_PASANG_1_KALI.md`](PANDUAN_PASANG_1_KALI.md) untuk langkah sederhana dan solusi jika website menampilkan 404 / Page not found.

## Tampilan desain

File konsep antarmuka yang menjadi acuan visual ada di [`docs/ui-reference.png`](docs/ui-reference.png). Website ini merupakan implementasi web responsif yang dibangun ulang untuk Safari; source Flutter lama tidak dijadikan runtime website.

## Cara pasang paling mudah: GitHub Pages + workflow otomatis

> Tidak perlu memasang Flutter, Node, Xcode, atau aplikasi tambahan di iPhone. Publikasi membutuhkan akun GitHub dan internet. Workflow akan menerbitkan website setiap kali kamu mengunggah perubahan ke branch `main`.

1. Unduh ZIP ini lalu **ekstrak** di perangkat yang bisa membuka GitHub (laptop lebih nyaman, tetapi bisa lewat browser iPhone).
2. Buka https://github.com/new dan buat repository baru, misalnya `my-money-safari`. Pilih **Public** agar langkah Pages paling sederhana, lalu buat repository kosong. Jangan tambahkan README atau file lain ketika membuat repo.
3. Di repository baru, pilih **Add file → Upload files**. Unggah **isi folder ZIP**, bukan ZIP-nya dan bukan folder luarnya. Pastikan `index.html`, `app.js`, `styles.css`, `manifest.webmanifest`, `sw.js`, folder `assets/`, dan folder `.github/workflows/` terlihat langsung di root repository.
4. Tekan **Commit changes**. Tunggu hingga workflow `Publish My Money to GitHub Pages` berjalan di tab **Actions**.
5. Buka **Settings → Pages → Build and deployment → Source**, lalu pilih **GitHub Actions** (wajib untuk workflow ini). Kembali ke tab **Actions**; jika perlu pilih workflow `Publish My Money to GitHub Pages` lalu **Run workflow** jika belum berjalan otomatis. Tunggu status hijau.
6. Buka **Settings → Pages** atau detail workflow yang berhasil, lalu tekan tautan website yang berakhir dengan `github.io`. URL tersebut adalah versi live milikmu.
7. Di iPhone, buka URL itu memakai **Safari** (bukan browser dalam aplikasi). Tekan tombol **Bagikan** (ikon kotak dengan panah ke atas) → **Tambahkan ke Layar Utama** → aktifkan **Buka sebagai App/ Open as Web App** jika pilihan itu muncul → **Tambah**.

Selesai. Ikon My Money akan muncul di Home Screen iPhone. Pastikan URL sudah HTTPS dan dibuka melalui Safari sebelum menambahkannya.

## Fitur yang tersedia

- Dashboard saldo, pemasukan dan pengeluaran bulan berjalan.
- Setup nama dan saldo awal.
- Catat, edit, hapus, cari, dan filter transaksi; kategori serta tanggal.
- Saran contoh nominal untuk beberapa item umum. Angka ini hanya contoh, bukan harga pasar langsung.
- Input dengan suara melalui Web Speech API jika browser/perangkat mendukung; kalau tidak, gunakan fitur dikte pada keyboard iPhone.
- Pie chart pengeluaran terbesar dan sumber pemasukan per kategori (ketuk irisan atau baris untuk detail), plus grafik arus kas 6 bulan.
- Target tabungan dan insight pengeluaran sederhana.
- Scan struk: foto langsung atau upload dari galeri; total, tanggal, toko, dan kategori dibaca otomatis (OCR Tesseract.js via CDN), diperiksa sekilas, lalu langsung masuk ke Laporan. Bila OCR tidak bisa dimuat, isi total secara manual.
- Mode Terang / Gelap / Otomatis (ikut pengaturan iPhone): tombol cepat di pojok kanan atas dan pilihan di halaman Akun.
- Tempel teks mutasi, kenali perkiraan nominal, kemudian tinjau dan simpan baris yang diperlukan satu per satu.
- Ekspor CSV, backup JSON, dan pulihkan backup.
- Service worker untuk menyimpan app shell agar halaman lebih tahan saat koneksi putus setelah pemuatan awal.
- UI responsif untuk layar iPhone kecil sampai desktop, dengan safe-area dan navigasi bawah.

## Privasi dan batasan penting

- Transaksi disimpan di `localStorage` browser pada perangkat saat ini. Data tidak otomatis tersinkron ke iCloud atau perangkat lain. Buat backup JSON secara rutin, terutama sebelum membersihkan data Safari.
- Jangan gunakan mode Private Browsing untuk penyimpanan utama. Pembersihan data website dapat menghapus catatan.
- Jangan tempel PIN, password, OTP, atau kredensial bank ke fitur mutasi.
- OCR memuat engine dari CDN dan membutuhkan internet pada penggunaan awal. OCR dapat salah membaca nominal/titik; selalu cek ulang.
- Dikte suara tergantung dukungan browser, izin mikrofon, bahasa, dan layanan suara perangkat. Tombol dikte pada keyboard iPhone bisa menjadi alternatif.
- Di beberapa konfigurasi Safari, unduhan CSV/JSON mungkin terbuka di tab pratinjau atau Files; pilih Share/Save to Files untuk menyimpan.
- Website ini aplikasi pencatat manual, bukan koneksi rekening bank, aplikasi akuntansi resmi, atau layanan nasihat keuangan.

## Memperbarui website

Edit file di repository lalu commit ke branch `main`. GitHub Actions akan menerbitkan versi baru otomatis. Untuk memeriksa deploy: tab **Actions** → workflow `Publish My Money to GitHub Pages` → run terbaru. Tidak perlu menjalankan build lokal.

## Troubleshooting

- **404 / website belum muncul:** pastikan file `index.html` ada langsung di root; workflow hijau; Pages menggunakan **GitHub Actions**. Refresh beberapa menit kemudian.
- **Tampilan lama setelah update:** tutup tab aplikasi lalu buka ulang. Service worker memperbarui shell ketika file diperbarui; bila belum, reload Safari atau bersihkan data website jika memang diperlukan (hal ini juga dapat menghapus transaksi lokal, jadi ekspor backup lebih dahulu).
- **Data tidak muncul di perangkat lain:** ini normal karena penyimpanan lokal tidak tersinkron. Transfer menggunakan Backup JSON → Pulihkan.
- **OCR tidak jalan:** gunakan foto lebih terang dan fokus, pastikan internet aktif, atau masukkan nominal manual.

## Isi paket

```text
index.html                      UI dan modal aplikasi
styles.css                      Desain responsif mobile-first
app.js                          Transaksi, laporan, backup, ekspor, suara, OCR
manifest.webmanifest            Metadata PWA / Home Screen
sw.js                           Cache app shell
assets/icon.svg                 Icon vektor
assets/icon-192.png             Icon PWA
assets/icon-512.png             Icon PWA
.github/workflows/deploy-pages.yml   Publikasi otomatis GitHub Pages
```
