# My Money — Cara pasang paling mudah (iPhone/Safari)

Ikuti langkah satu per satu. Kamu tidak perlu Flutter, terminal, atau GitHub Desktop.

## Kalau semua file sudah kamu upload

1. Buka repository MyMoney kamu di GitHub.
2. Tekan tab **Code**. Pastikan `index.html`, `app.js`, `styles.css`, `manifest.webmanifest`, `sw.js`, dan folder `assets` terlihat di halaman utama repository.
3. Pastikan workflow berada persis di `.github/workflows/deploy-pages.yml`. Nama `blank.yml` tidak dibutuhkan. Jika kamu pernah membuat `blank.yml` yang kosong, hapus file itu agar tidak membingungkan.
4. Tekan **Settings → Pages**.
5. Di bagian **Build and deployment**, ubah **Source** menjadi **GitHub Actions**. Jangan pilih `Deploy from a branch` untuk workflow ini.
6. Kembali ke **Actions**. Pilih **Publish My Money to GitHub Pages**. Jika belum berjalan, tekan **Run workflow** (pilih branch `main` atau `master` yang memang ada), lalu konfirmasi tombol hijau **Run workflow**.
7. Buka run terbaru dan tunggu sampai tanda centang hijau. Tekan job **Check and publish website**, lalu cari tautan website. Ringkasan workflow juga akan menampilkan URL jika berhasil.
8. Buka tautan itu dengan Safari di iPhone. Tekan **Bagikan → Tambahkan ke Layar Utama → Tambah**. Jika ada pilihan **Buka sebagai App Web**, aktifkan.

## Kalau kamu perlu mengunggah ulang paket

- Unduh ZIP `MyMoney_Safari_PWA.zip`, kemudian ekstrak di komputer.
- Unggah **isi ZIP**, bukan file ZIP itu sendiri. Berkas `index.html` harus langsung berada di root repository.
- Folder tersembunyi `.github` sangat penting. Pastikan di dalam repository ada `.github/workflows/deploy-pages.yml`.
- Tekan **Commit changes**. Push ke `main` atau `master` akan memulai workflow secara otomatis.

## Kalau masih “Page not found”

1. Buka **Actions → Publish My Money to GitHub Pages**. Jika run merah, buka run itu dan baca langkah yang merah. Langkah pemeriksaan akan menyebut file yang hilang.
2. Jika run hijau, buka **Settings → Pages**, pastikan Source = **GitHub Actions**, lalu buka URL yang ditampilkan oleh job deployment. Jangan menebak URL sendiri karena nama akun dan repository harus tepat.
3. Pastikan kamu membuka URL lengkap yang ditampilkan GitHub, biasanya berbentuk `https://NAMA-AKUN.github.io/NAMA-REPOSITORY/`.
4. Coba refresh Safari setelah beberapa menit. Untuk pemasangan di iPhone, website harus dibuka melalui HTTPS.

## Hal penting

- Workflow membantu memeriksa file lalu menerbitkan website; ia tidak dapat masuk ke akun GitHub atau mengubah pengaturan akun atas namamu.
- Pengaturan awal **Settings → Pages → Source = GitHub Actions** tetap perlu dilakukan satu kali.
- Data transaksi disimpan di browser/perangkat itu saja. Data tidak otomatis sinkron ke perangkat lain. Ekspor backup secara berkala.
- Setelah berhasil, catatan berikutnya yang kamu commit ke branch `main` atau `master` akan diterbitkan otomatis.
