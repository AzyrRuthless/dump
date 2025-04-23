# Dump - Auto Commit Bot 🤖

[![GitHub Workflow Status](https://github.com/AzyrRuthless/dump/actions/workflows/autocommit.yml/badge.svg)](https://github.com/AzyrRuthless/dump/actions/workflows/autocommit.yml)

Repositori ini (`AzyrRuthless/dump`) menggunakan GitHub Actions untuk secara otomatis memperbarui file `LAST_UPDATED` dengan timestamp saat ini dan melakukan commit perubahan tersebut kembali ke repositori.

## Tujuan

Tujuan utama repositori ini adalah untuk:

1.  Menunjukkan contoh penggunaan GitHub Actions untuk otomatisasi tugas Git dasar.
2.  Menjaga repositori ini tetap "aktif" dengan adanya commit otomatis secara berkala (misalnya, untuk aktivitas profil GitHub).
3.  Menyimpan catatan sederhana kapan terakhir kali proses otomatis ini berhasil berjalan.

## Bagaimana Cara Kerjanya?

Sebuah workflow GitHub Actions (didefinisikan dalam file `.github/workflows/auto_commit.yml`) dikonfigurasi untuk berjalan secara otomatis pada kondisi berikut:

1.  **Setiap `push` ke branch `master`**: Workflow akan terpicu setiap kali ada perubahan yang di-push ke branch utama.
2.  **Jadwal Harian**: Workflow dijadwalkan untuk berjalan **setiap hari** pada pukul **07:00, 09:00, dan 11:00 UTC** (`0 7,9,11 * * *`).

### Langkah-langkah Workflow:

1.  **Checkout**: Mengambil kode terbaru dari repositori.
2.  **Update Timestamp**: Memperbarui konten file `LAST_UPDATED` dengan tanggal dan waktu saat ini dalam format ISO 8601 UTC.
3.  **Cek Perubahan & Pencegahan Loop**:
    *   Memeriksa apakah file `LAST_UPDATED` benar-benar memiliki perubahan yang belum di-commit.
    *   Memeriksa pesan commit terakhir. Jika commit terakhir juga merupakan auto-commit dari workflow ini (memiliki pola `chore(bot): ... auto commit`), proses commit dan push akan **dilewati** untuk **mencegah loop tak terbatas**.
4.  **Commit**: Jika ada perubahan dan commit terakhir *bukan* dari bot ini, workflow akan melakukan `git commit` dengan salah satu pesan acak yang telah ditentukan (contoh: `chore(bot): 🤖 auto commit`).
5.  **Push**: Mendorong (push) commit baru tersebut kembali ke branch `master` di repositori GitHub.

## File Penting

*   `LAST_UPDATED`: File teks sederhana yang berisi timestamp UTC terakhir kali workflow berhasil berjalan dan melakukan commit.
*   `.github/workflows/auto_commit.yml`: File konfigurasi GitHub Actions yang menjalankan otomatisasi ini. *(Pastikan nama file ini sesuai dengan yang ada di repositori Anda)*

## Melihat Workflow

Anda dapat melihat detail konfigurasi workflow dan riwayat eksekusinya di:

*   Tab **Actions** repositori ini: [https://github.com/AzyrRuthless/dump/actions](https://github.com/AzyrRuthless/dump/actions)
*   File Workflow itu sendiri: [`./.github/workflows/autocommit.yml`](./.github/workflows/autocommit.yml) *(Klik link ini jika nama file-nya sudah benar)*

---

*Repositori ini terutama berfungsi sebagai demonstrasi dan untuk menjaga aktivitas profil GitHub.*
