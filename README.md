# Nara-game v2 — Android Kotlin

Project baru untuk game puzzle reward dengan Start.io. Dibuat ulang, bukan patch project lama.

## Aturan ekonomi (konfigurasi awal)
- 59.000 koin = Rp1.000.
- 5.900 koin = nilai nominal Rp100.
- Reward target untuk 1 video **Rewarded Video yang selesai**: 5.900 koin.
- Interstitial (mis. gagal / restart / lanjut level) tidak menghasilkan koin.
- Reward nominal Rp100/video adalah target produk, BUKAN jaminan bahwa pendapatan Start.io per tayangan mencapai Rp100. Jangan aktifkan penarikan uang sungguhan sebelum dashboard pendapatan, fill rate, eCPM, biaya, dan fraud diuji. Nilai reward dapat diubah di `app/src/main/java/com/nara/game/Economy.kt`.

## Iklan Start.io
- Publisher App ID: `210355804` (dari screenshot pemilik).
- SDK: `com.startapp:inapp-sdk:5.3.1`.
- Manifest initialization, sesuai dokumentasi resmi.
- Rewarded Video dipanggil melalui `loadAd(AdMode.REWARDED_VIDEO)`, `setVideoListener`, `showAd`.
- Interstitial dipanggil dengan `StartAppAd.showAd(activity)`.
- 5 langkah berhasil: tawarkan Rewarded Video dengan persetujuan pemain.
- Gagal, mulai ulang, lanjut level: interstitial dengan cooldown agar tidak spam.
- Hanya callback `onVideoCompleted()` yang memicu reward prototype. Callback di perangkat tetap bisa dimodifikasi; bukan bukti server yang aman untuk pembayaran uang.

## Buka project
1. Ekstrak ZIP.
2. Android Studio > Open > pilih folder `Nara-game-v2`.
3. Gunakan JDK 17 dan Android SDK 35.
4. Sync Gradle, jalankan di perangkat Android.
5. Pastikan perangkat online dan App ID sudah terdaftar/aktif di portal Start.io.

## Status payout
UI menampilkan DANA, OVO, GoPay, ShopeePay dan nilai konversi. Pengiriman uang sungguhan sengaja belum diaktifkan. Integrasi payout butuh akun merchant/disbursement resmi atau aggregator, backend, autentikasi, ledger server, validasi webhook, serta uji sandbox. Start.io adalah jaringan iklan, bukan penyedia transfer e-wallet.

## Referensi
- https://support.start.io/hc/en-us/articles/360014774799-Integration-via-Maven
- https://support.start.io/hc/en-us/articles/360006662474-Advanced-Usage
