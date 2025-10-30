# Dump - Auto Commit Bot 🤖

[![GitHub Workflow Status](https://github.com/AzyrRuthless/dump/actions/workflows/autocommit.yml/badge.svg)](https://github.com/AzyrRuthless/dump/actions/workflows/autocommit.yml)

Repositori ini (`AzyrRuthless/dump`) menggunakan GitHub Actions untuk secara otomatis memperbarui file `LAST_UPDATED` dengan timestamp UTC saat ini dan melakukan commit perubahan tersebut kembali ke repositori.

## Tujuan

- Menunjukkan contoh penggunaan GitHub Actions untuk otomatisasi tugas Git dasar.
- Menjaga repositori ini tetap aktif dengan commit otomatis berkala.
- Menyimpan catatan sederhana kapan terakhir kali proses otomatis ini berhasil berjalan.

## Pemicu

- Jadwal harian: workflow berjalan setiap hari pukul 07:00, 09:00, dan 11:00 UTC dengan cron `0 7,9,11 * * *`.
- Manual: dapat dijalankan dari tab Actions melalui `workflow_dispatch`.
- Catatan: workflow ini TIDAK memiliki pemicu `push`.

## Cara Kerjanya

- Checkout kode repositori pada runner Ubuntu.
- Tulis timestamp UTC dalam format ISO 8601 ke berkas `LAST_UPDATED`.
- Lakukan commit hanya jika ada perubahan pada `LAST_UPDATED` (untuk menghindari commit kosong).
- Push perubahan ke branch `master` menggunakan `GITHUB_TOKEN` dengan izin `contents: write`.

## Berkas Penting

- `LAST_UPDATED`: berisi timestamp UTC terakhir kali workflow sukses berjalan.
- `.github/workflows/autocommit.yml`: definisi workflow yang mencakup `schedule` dan `workflow_dispatch`.

## Melihat Workflow

- Tab **Actions** repositori ini: `https://github.com/AzyrRuthless/dump/actions`
- File workflow: `./.github/workflows/autocommit.yml`

## Catatan

- Event `schedule` di GitHub Actions selalu dievaluasi dalam waktu UTC.
- Pastikan `branch` pada langkah push sesuai dengan default branch repositori Anda (contoh ini memakai `master`).
- Anda dapat memverifikasi ekspresi cron menggunakan editor seperti crontab.guru.