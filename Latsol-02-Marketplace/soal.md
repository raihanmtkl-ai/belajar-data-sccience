# Latsol Pandas + Matplotlib: Marketplace Online

**File:** `orders.csv` (transaksi) dan `master_produk.csv` (master produk).
Kerjain di notebook sendiri, simpan jawaban sebagai `jawaban.ipynb` di folder ini.

> Dataset sengaja kotor. Jangan langsung percaya sama data, cek dulu.

---

## Bagian A. Eksplorasi & Cleaning

1. Load kedua CSV. Tampilkan `.info()`, jumlah baris, dan jumlah nilai kosong per kolom di `orders`.
2. Cek dan buang baris duplikat. Tulis berapa baris yang dibuang. (Hati-hati: duplikat berdasarkan *seluruh baris* atau *order_id* doang? Jelasin pilihan lu.)
3. Bersihin kolom `status`, `kota`: samain casing dan hapus spasi berlebih. Buktikan pakai `.value_counts()` sebelum vs sesudah.
4. Kolom `tanggal` formatnya campur-campur. Ubah jadi datetime yang benar, lalu bikin kolom `bulan` dan `hari_dalam_minggu`.
5. Kolom `qty` berisi nilai aneh (`NA`, `-`, kosong). Ubah jadi numerik. Terus putusin: baris dengan qty tidak valid itu diisi atau dibuang? Alasannya apa?
6. Kolom `diskon_persen` ada yang kosong. Isi pakai strategi yang menurut lu masuk akal, dan jelasin kenapa (median / 0 / lainnya).

## Bagian B. Merge & Feature

7. Gabungin `orders` dengan `master_produk` (left join dari orders). Berapa baris yang `nama_produk`-nya NaN? Tampilkan `id_produk` penyebabnya.
8. Bikin kolom `total_bayar = qty * harga * (1 - diskon_persen/100)`.
9. Dari data yang sudah bersih, filter cuma order berstatus `selesai`. Semua analisis di Bagian C pakai data ini, kecuali disebut lain.

## Bagian C. Analisis + Visualisasi

10. **Bar chart:** total pendapatan per kategori, urut dari terbesar. Kasih judul, label sumbu, dan angka di atas bar.
11. **Line chart:** tren pendapatan per bulan. Tandai bulan dengan pendapatan tertinggi.
12. **Horizontal bar:** 5 produk terlaris berdasarkan total `qty`.
13. **Histogram:** distribusi `total_bayar`. Coba 2 nilai `bins` berbeda, bandingin side by side pakai subplot. Menurut lu bins mana yang lebih informatif?
14. **Pie chart:** proporsi `metode_bayar` berdasarkan jumlah order. Terus tulis 1 kalimat: kenapa pie chart sering dianggap kurang bagus?
15. **Groupby + pivot:** bikin tabel rata-rata `rating` per `kategori` x `kota` (pakai `.pivot_table()` atau `.unstack()`). Visualisasiin pakai `plt.imshow` atau `ax.matshow` (heatmap sederhana tanpa seaborn).
16. **Scatter:** `diskon_persen` vs `qty`. Ada pola? Tulis kesimpulan singkat.

## Bagian D. Dashboard Akhir

17. Bikin 1 figure `2x2` subplot berisi: (a) pendapatan per kategori, (b) tren bulanan, (c) top 5 produk, (d) rasio status order (selesai/batal/dikirim, pakai data sebelum difilter). Kasih `suptitle`, `tight_layout()`, lalu simpan jadi `dashboard.png`.

## Bonus

18. Hitung *cancellation rate* (persen order batal) per kota dan per metode bayar. Metode bayar mana yang paling sering batal?
19. Customer mana (`id_customer`) yang total belanjanya paling besar? Berapa persen kontribusinya ke total pendapatan?

---
Kerjain sendiri dulu. Kalau mentok atau ada error, tempel kode + pesan errornya ke sini.
