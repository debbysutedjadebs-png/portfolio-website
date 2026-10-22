# Deby Suteja — Portfolio Website + CMS Gratis

## Apa yang sudah dibuat
- Desain HTML/CSS lama dipertahankan.
- Seluruh project lama dipindah ke `content/projects.json`.
- Dashboard editor Decap tersedia di `/admin/`.
- Editor bisa menambah/mengubah/mengurutkan project, galeri gambar, dan publikasi.

## Langkah aktivasi (wajib, dilakukan oleh pemilik akun)
1. Buat repository GitHub, misalnya `portfolio-website`, lalu upload **isi folder** ZIP ini ke branch `main` (bukan ZIP sebagai satu file).
2. Pada `admin/config.yml`, ganti `GANTI_USERNAME/portfolio-website` dengan `username/repo` yang sesungguhnya.
3. Buat OAuth App di GitHub dan siapkan OAuth proxy Cloudflare Worker. Decap tidak bisa login ke GitHub hanya dengan website statis. Contoh solusi open source dan petunjuk: https://github.com/sterlingwes/decap-proxy ; dokumentasi resmi: https://decapcms.org/docs/backends-overview/ .
4. Isi alamat Worker OAuth pada `base_url` di `admin/config.yml` (harus sama dengan URL Worker yang aktif). Konfigurasikan callback OAuth sesuai petunjuk proxy yang dipilih. Rahasiakan GitHub OAuth CLIENT_SECRET: masukkan sebagai Worker Secret, jangan di file situs/repo.
5. Hubungkan repo GitHub ke Cloudflare Pages memakai Git integration, branch `main`, tanpa build command, output directory `/` atau `.`, sesuai tampilan dashboard. **Jangan hanya Direct Upload jika ingin CMS memperbarui website secara otomatis dari GitHub.**
6. Buka `https://NAMA-PAGES.pages.dev/admin/` lalu Login with GitHub. Pastikan akun punya izin tulis pada repo.
7. Pilih Portfolio > Kelola Projects, tambah item, upload gambar, lalu Publish. Setelah commit ke GitHub, Pages akan deploy otomatis.

## Catatan penting
- `admin/index.html` adalah halaman editor tetapi login **belum aktif** sampai GitHub dan OAuth Worker dibuat. Paket ini bukan CMS terhubung siap-login.
- Nama domain `*.pages.dev` bergantung ketersediaan.
- Paket Cloudflare/GitHub gratis memiliki kuota serta batas layanan yang dapat berubah.
- Jika website dibuka langsung dari disk (`file://`), pemuatan JSON dapat gagal. Gunakan server lokal (`python3 -m http.server 8000`), atau lihat pada Pages.
- `content/projects.json` dapat juga diperbarui manual tanpa CMS.
- Project memiliki detail dalam modal (bukan halaman URL terpisah), sama seperti desain awal.
