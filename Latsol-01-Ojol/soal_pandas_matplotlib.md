# Latihan Soal Pandas + Matplotlib: Data Ojek Online 🏍️

**File yang dipakai** (taruh satu folder dengan notebook/script kamu):
- `ride_trips.csv` : data perjalanan (415 baris, **sengaja kotor**)
- `master_driver.csv` : tabel master driver (20 baris)

**Kolom `ride_trips.csv`:** `trip_id`, `waktu_order`, `kota`, `jenis_layanan`, `driver_id`, `jarak_km`, `tarif`, `durasi_menit`, `rating`, `metode_bayar`

**Kolom `master_driver.csv`:** `driver_id`, `nama_driver`, `kota_base`, `tahun_gabung`, `status`

> Tips: jangan langsung percaya datanya. Selalu cek `.info()`, `.isna().sum()`, `.value_counts()`, dan `.describe()` dulu sebelum ngerjain soal.

---

## Bagian A: Eksplorasi & Cleaning

1. Load kedua CSV. Tampilkan `shape`, `dtypes`, dan jumlah missing value per kolom di `ride_trips`. Kolom mana yang tipenya tidak sesuai? Kenapa bisa begitu?
2. Ada berapa baris duplikat di `ride_trips`? Hapus duplikatnya. Duplikat itu berdasarkan seluruh baris atau `trip_id` saja? Jelaskan pilihanmu.
3. Rapikan kolom `kota` dan `jenis_layanan` (spasi berlebih + casing tidak konsisten) sampai `value_counts()`-nya cuma berisi nilai yang valid.
4. Kolom `jarak_km` dan `rating` punya representasi null yang campur-campur. Ubah semuanya jadi `NaN` yang benar, lalu konversi ke tipe numerik.
5. Kolom `tarif` ada yang berformat `Rp12.500`. Bersihkan jadi angka (integer/float).
6. Kolom `waktu_order` formatnya campur (3 format berbeda). Ubah jadi `datetime` yang seragam. Pastikan tidak ada yang gagal parse.
7. Kolom `metode_bayar` ada nilai `unknown` dan kosong. Ubah jadi `NaN`, lalu putuskan: isi atau dibiarkan? Tulis alasanmu dalam komentar kode.
8. Cek outlier di `tarif` (hint: bandingkan tarif vs `jarak_km`, atau pakai IQR per `jenis_layanan`). Berapa baris yang mencurigakan? Apa yang kamu lakukan dengan baris itu dan kenapa?

## Bagian B: Imputasi & Feature Engineering

9. Isi `NaN` di `jarak_km` dengan **median per `jenis_layanan`** (hint: `groupby().transform()`).
10. Isi `NaN` di `durasi_menit` dengan strategi yang menurutmu masuk akal. Jelaskan kenapa. (Pikirkan: apakah ada hubungan dengan kolom lain?)
11. `rating` yang kosong: isi atau biarkan `NaN`? Jelaskan dampaknya ke rata-rata rating.
12. Buat kolom baru:
    - `jam`, `hari` (nama hari), `bulan` dari `waktu_order`
    - `tarif_per_km` = `tarif / jarak_km`
    - `kategori_jarak` pakai `pd.cut()`: Dekat (<3 km), Sedang (3–10 km), Jauh (>10 km)
    - `waktu_hari`: Pagi (05–10), Siang (11–14), Sore (15–18), Malam (19–04)

## Bagian C: GroupBy & Agregasi

13. Total pendapatan (`tarif`) dan jumlah trip per `kota`, urutkan dari pendapatan terbesar.
14. Per `jenis_layanan`: rata-rata tarif, median jarak, dan rata-rata rating dalam **satu** tabel (pakai named aggregation).
15. Pivot table: baris = `kota`, kolom = `jenis_layanan`, isi = jumlah trip. Tambahkan total baris dan kolom (hint: `margins=True`).
16. Rata-rata `tarif_per_km` per `kategori_jarak` per `jenis_layanan`. Bentuk hasilnya jadi tabel lebar pakai `.unstack()`.
17. Jam berapa order paling ramai? Dan hari apa paling sepi? Jawab pakai kode, bukan nebak.
18. Metode pembayaran mana yang paling sering dipakai di tiap kota? (Hint: `idxmax` atau `value_counts` + groupby.)

## Bagian D: Merge / Join

19. Gabungkan `ride_trips` dengan `master_driver` pakai `driver_id` (left join). Berapa baris yang `nama_driver`-nya `NaN` setelah merge? Kenapa?
20. Tampilkan `driver_id` yang ada di `ride_trips` tapi **tidak ada** di `master_driver` (anti-join). Lalu sebaliknya: driver di master yang **tidak pernah** dapat trip.
21. Top 5 driver berdasarkan total pendapatan. Tampilkan `nama_driver`, `kota_base`, total pendapatan, dan rata-rata rating.
22. Hitung persentase trip yang dikerjakan driver yang **bukan** dari kota base-nya (`kota` ≠ `kota_base`). Apakah driver `Nonaktif` masih punya trip? Berapa?
23. Bandingkan rata-rata rating driver berdasarkan `tahun_gabung`. Apakah driver lama punya rating lebih tinggi?

## Bagian E: Visualisasi Matplotlib

Semua grafik **wajib** punya judul, label sumbu, dan ukuran figure yang rapi.

24. **Bar chart**: total pendapatan per kota (urut dari terbesar), tampilkan angka di atas tiap bar.
25. **Line chart**: jumlah trip per minggu atau per bulan. Tandai titik puncaknya pakai `annotate`.
26. **Histogram**: distribusi `jarak_km`. Coba `bins` berbeda (10 dan 25), bandingkan dalam 2 subplot berdampingan.
27. **Pie chart**: proporsi `jenis_layanan` (pakai `autopct`). Setelah selesai, pikirkan: kapan pie chart sebenarnya kurang cocok dipakai?
28. **Scatter plot**: `jarak_km` vs `tarif`, warnai titik berdasarkan `jenis_layanan`. Tambahkan legend.
29. **Grouped bar chart**: jumlah trip per `kota` dipecah per `jenis_layanan` (hasil dari soal 15).
30. **Boxplot**: sebaran `tarif_per_km` per `jenis_layanan`. Apa yang bisa kamu simpulkan dari outliernya?

## Bagian F: Tantangan Akhir 🔥

31. Buat **satu figure dengan grid 2×3 subplot** sebagai "dashboard mini" yang berisi 6 insight paling menarik dari data ini. Beri judul besar untuk keseluruhan figure (`fig.suptitle`) dan simpan hasilnya sebagai `dashboard_ojol.png` dengan `dpi=150`.
32. Tulis 3–5 kalimat kesimpulan bisnis dari data ini (kota mana yang potensial, layanan apa yang paling untung, jam sibuk, dll.) sebagai komentar atau markdown cell di akhir notebook.

---

### Checklist sebelum selesai
- [ ] Tidak ada `inplace=True` yang bikin bingung. Pakai assignment biasa
- [ ] Tipe data semua kolom sudah benar (`df.info()`)
- [ ] Tiap grafik ada judul + label sumbu
- [ ] Ada komentar singkat di keputusan penting (imputasi, outlier, dll.)

Kalau ada error atau mentok di satu soal, kirim ke aku pesan error-nya + kode kamu. Kalau mau kunci jawaban setelah selesai ngerjain, bilang aja. Selamat ngoding! 🚀
