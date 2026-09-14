# Kalkulator Batch — EA Tunggak Semi

Kalkulator statis (HTML + JS, tanpa backend) untuk mengestimasi risiko sistem
**batch averaging & cutloss** ala EA grid/martingale "Tunggak Semi":

- Total lot per batch (mengikuti rumus `GetBatchLotSize` di EA)
- Estimasi loss per batch saat cutloss batch penuh terpicu (dalam USC)
- Akumulasi loss/profit dari batch ke-1 sampai batch ke-n — angka akumulasi
  loss ini sekaligus mencerminkan modal yang perlu disiapkan
- Target profit (TP) tiap batch, termasuk pemulihan loss batch sebelumnya

Perhitungan berat dijalankan di **Web Worker** dengan **cache/memoization**
berbasis hash parameter, supaya UI tetap responsif walau mensimulasikan
puluhan/ratusan batch, dan input yang sama tidak dihitung ulang.

⚠️ Ini alat bantu estimasi berbasis logika EA, **bukan hasil backtest**.
Spread, slippage, swap, dan pergerakan harga riil tidak diperhitungkan.

## Fitur tambahan

- **Icon lengkap** (`icon-192.png`, `icon-512.png`, `apple-touch-icon.png`) +
  `manifest.json`. File SVG data-URI saja tidak cukup untuk shortcut "Add to
  Home Screen" di HP (Android butuh `manifest.json` dengan PNG, iOS Safari
  butuh `apple-touch-icon` PNG terpisah) — sekarang semua sudah disediakan,
  jadi ikon akan muncul saat halaman ditambahkan ke home screen.
- **Auto-update checker**: setiap 60 detik halaman diam-diam mengambil ulang
  dirinya sendiri dengan `cache: 'no-store'`, membandingkan meta `app-version`.
  Jika versi di server berbeda dari yang sedang tampil, muncul banner
  "Versi baru tersedia" dengan tombol untuk memuat ulang paksa (bypass cache).
- Meta `Cache-Control: no-cache, no-store, must-revalidate` ditambahkan agar
  browser tidak menyimpan cache halaman ini sendiri.

**Penting:** upload semua file (`index.html`, `manifest.json`, `icon-192.png`,
`icon-512.png`, `apple-touch-icon.png`) ke repo yang sama, sejajar (bukan di
folder terpisah) — kalau hanya `index.html` yang diupload, ikon tidak akan
ketemu dan home screen tetap pakai ikon default browser.

## Kenapa dulu terasa "tidak update" walau sudah tunggu lama?

GitHub Pages disajikan lewat CDN yang kadang menyimpan cache HTML selama
beberapa menit, ditambah cache browser sendiri. Dua hal itu bisa membuat
perubahan terasa belum masuk walau file di repo sudah ter-update. Dengan
auto-update checker + meta no-cache di atas, begitu file baru live di CDN,
banner reload akan otomatis muncul tanpa perlu bersihkan cache manual.

**Setiap kali upload versi baru, naikkan angka di meta `app-version`** pada
`index.html` (contoh: `1.1.0` → `1.2.0`) supaya checker bisa mendeteksi
perubahan.

## Menjalankan

Buka `index.html` langsung di browser, atau aktifkan GitHub Pages
(Settings → Pages → Deploy from branch → `main` / `root`) agar bisa diakses
via link publik.

## Lisensi

Bebas digunakan dan dimodifikasi untuk keperluan pribadi.
