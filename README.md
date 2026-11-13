# Nara-game — Native Android Kotlin

Ini adalah project **Android Native Kotlin + Jetpack Compose**. Bukan HTML, bukan website, dan tidak memakai WebView.

## Struktur kode

- `MainActivity.kt` — entry point Android.
- `game/GameEngine.kt` — aturan puzzle dan pencarian blok terhubung.
- `game/GameScreen.kt` — layar permainan.
- `game/GameViewModel.kt` — state dan alur level.
- `ads/StartIoAds.kt` — integrasi Start.io rewarded + interstitial.
- `wallet/WalletRepository.kt` — penyimpanan saldo prototipe lokal.
- `wallet/RewardManager.kt` — aturan reward koin.
- `wallet/WalletScreen.kt` — layar dompet dan konversi.
- `wallet/WithdrawalScreen.kt` — UI metode e-wallet; payout dinonaktifkan sampai backend resmi siap.
- `settings/SettingsScreen.kt` — pengaturan.
- `docs/` — dokumentasi integrasi, ekonomi, payout, dan build.
- `.github/workflows/android.yml` — build APK otomatis di GitHub Actions.

## Ketentuan ekonomi
Konversi tetap: **59.000 koin = Rp1.000**.
Reward sesuai aturan: 590–885 koin acak per rewarded video selesai (nilai nominal Rp10–Rp15). Konversi tetap 59.000 koin = Rp1.000. Iklan interstitial tidak memberi koin. Pendapatan Start.io sekitar Rp35 bukan tarif tetap atau jaminan; verifikasi dashboard, pendapatan bersih, biaya, dan margin sebelum membuka payout sungguhan.

## Start.io
Publisher App ID yang dimasukkan: `210355804`.
SDK dependency menggunakan Maven Central `com.startapp:inapp-sdk:5.3.1`.
Inisialisasi menggunakan AndroidManifest sesuai panduan Start.io.
- Setiap 5 langkah berhasil: pemain ditawari rewarded video.
- Koin hanya diberikan pada `VideoListener.onVideoCompleted()`.
- Gagal, mulai ulang, lanjut level: meminta interstitial; interstitial tidak memberikan koin.
- Jika iklan belum siap / tidak ada inventory, SDK tidak akan menampilkan iklan. Tidak ada jaminan iklan selalu tersedia.

Dokumentasi resmi: https://support.start.io/hc/en-us/articles/360014774799-Integration-via-Maven

## Batasan sebelum rilis uang sungguhan
Saldo Android saat ini lokal untuk uji UI. Callback iklan pada perangkat bukan bukti server yang aman. Penarikan DANA/OVO/GoPay/ShopeePay belum tersambung. Sebelum uang sungguhan, implementasikan backend ledger, autentikasi, validasi reward anti-replay/fraud, API disbursement resmi/aggregator, verifikasi webhook, rekonsiliasi, syarat minimum, privasi, dan kebijakan Google Play.

## Build APK
Cara termudah dari GitHub:
1. Upload semua isi ZIP ke repository.
2. Buka tab **Actions**.
3. Pilih workflow **Build Nara-game APK** lalu tekan **Run workflow**.
4. Setelah selesai, buka hasil run dan unduh artifact `Nara-game-debug-apk`.
5. Pasang APK di perangkat uji.

Workflow menggunakan Gradle 8.11.1 + Android Gradle Plugin 8.10.1 + JDK 17.
