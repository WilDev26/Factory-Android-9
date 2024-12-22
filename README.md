# Skrip Bash untuk mereset (melalui Termux & ADB ) perangkat Android (Pie)

Skrip bash ini dapat digunakan untuk mereset perangkat Android yang terhubung melalui USB. Skrip ini dapat mereset sebanyak mungkin perangkat yang dapat terhubung secara bersamaan.

Skrip ini bekerja dengan memicu fitur "Factory Reset" bawaan yang terdapat di menu Setelan. Skrip ini mengeksekusi setiap langkah dengan menggunakan simulasi 'ketukan', 'mengetik', dan tindakan lain melalui Android Debug Bridge (adb).

Meskipun ditulis untuk versi Android tertentu, kodenya disusun sedemikian rupa sehingga setiap langkah/tindakan bersifat modular dan diberi komentar dengan baik sehingga fungsi yang sama ini dapat ditata ulang dan dimodifikasi agar sesuai untuk versi Android lainnya.

# Persyaratan

## Perangkat Keras
* Perangkat yang menjalankan Android 9, terhubung ke komputer Anda melalui USB
* Komputer yang menjalankan Ubuntu dan memiliki setidaknya satu port USB
* Hub USB (untuk mencolokkan beberapa perangkat sekaligus)

## Perangkat Lunak
* Komputer harus menjalankan sistem operasi Linux yang dapat mengeksekusi skrip bash. Secara teori, Anda dapat menggunakannya di Windows melalui aplikasi seperti [Git Bash](https://git-scm.com/downloads). Komputer harus memiliki aplikasi berikut yang terinstal dan berfungsi:
* sqlite3
* adb

## Lingkungan
* USB debugging perlu diaktifkan pada perangkat yang akan direset. ([Cara](https://developer.android.com/studio/debug/dev-options))

# Memulai
## Menyiapkan
* Instal semua aplikasi yang diperlukan di komputer
```
sudo apt install -y sqlite3 android-tools-adb
```

* Kloning repositori menggunakan git:
```
git clone http://github.com/amestsantim/decommissioner
cd decommissioner
```

# Penggunaan
## Persiapan
1. Hubungkan hub USB ke komputer, lalu colokkan setiap perangkat Android ke hub USB. 2. Aktifkan USB debugging pada setiap perangkat android

## Menjalankan
Jalankan perintah berikut saat berada di direktori decommissioner.
```
./wipe.sh
```
Skrip akan mencoba menjalankan langkah 'Factory Reset' pada setiap perangkat yang terhubung secara bersamaan dan akan menampilkan hasilnya di layar seperti pada contoh berikut.

<img src="screenshot.png"
alt="Contoh hasil eksekusi"
style="max-width: 70%;" />

## Melihat Laporan
Skrip mencatat hasil upaya 'Factory Reset' untuk setiap perangkat dalam basis data SQLite3. File disimpan dengan nama 'ACTIVITY_LOG.sqlite3' di direktori decommissioner.

Anda dapat menggunakan browser basis data SQLite seperti [DB Browser for SQLite](https://sqlitebrowser.org/) untuk membuka file dan melihat tabel 'hasil'.

Tabel 'hasil' memiliki empat kolom
1. **id** - urutan bilangan bulat yang dibuat secara otomatis mulai dari 1
2. **perangkat** - ID perangkat android
3. **stempel waktu** - tanggal dan waktu saat perangkat disetel ulang
4. **hasil** - hasil percobaan. Nilai yang mungkin di sini adalah 'Berhasil disetel ulang' atau 'Gagal menyetel ulang'

# Catatan
Skrip ini ditugaskan oleh UNECA untuk digunakan oleh negara-negara anggota, sehubungan dengan penghentian penggunaan tablet sensus CAPI.
