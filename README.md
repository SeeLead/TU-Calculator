# Kalkulator Batch — EA Tunggak Semi

Kalkulator statis (HTML + JS, tanpa backend) untuk mengestimasi risiko sistem
**batch averaging & cutloss** ala EA grid/martingale "Tunggak Semi":

- Total lot per batch (mengikuti rumus `GetBatchLotSize` di EA)
- Estimasi loss per batch saat cutloss batch penuh terpicu
- Akumulasi loss/profit dari batch ke-1 sampai batch ke-n
- Target profit (TP) tiap batch, termasuk pemulihan loss batch sebelumnya
- Estimasi margin & modal yang diperlukan untuk menahan grid penuh

Perhitungan berat dijalankan di **Web Worker** dengan **cache/memoization**
berbasis hash parameter, supaya UI tetap responsif walau mensimulasikan
puluhan/ratusan batch, dan input yang sama tidak dihitung ulang.

⚠️ Ini alat bantu estimasi berbasis logika EA, **bukan hasil backtest**.
Spread, slippage, swap, dan pergerakan harga riil tidak diperhitungkan.

## Menjalankan

Buka `index.html` langsung di browser, atau aktifkan GitHub Pages
(Settings → Pages → Deploy from branch → `main` / `root`) agar bisa diakses
via link publik.

## Lisensi

Bebas digunakan dan dimodifikasi untuk keperluan pribadi.
