# Panduan Setup Google Search Console, Bing & AI — hilmimokhsen.com

Panduan ini berisi langkah setelah website online agar **hilmimokhsen.com** cepat terindeks Google, Bing, dan AI (ChatGPT, Gemini, Perplexity, Claude). Kerjakan berurutan dan centang yang sudah selesai.

> **Perkiraan waktu:** halaman biasanya terindeks dalam 2 hari–2 minggu setelah sitemap dikirim. Peringkat untuk kata kunci seperti "content creator NTT" butuh beberapa minggu sampai bulan, tergantung tautan dari luar (bio sosial media, media, Undana).

---

## 0. Pastikan website sudah online

> **Status saat ini (7 Oktober 2026):** website sudah online di GitHub Pages: <https://ihsanmokhsen.github.io/hilmimokhsen.com/>. Domain **hilmimokhsen.com belum terdaftar**, jadi beli dulu domainnya (Niagahoster, Domainesia, Rumahweb, Cloudflare Registrar, dll.), lalu pasang ke GitHub Pages:
> 1. Di pengelola DNS domain, tambahkan 4 record `A` untuk `@`: `185.199.108.153`, `185.199.109.153`, `185.199.110.153`, `185.199.111.153`, dan 1 record `CNAME` untuk `www` → `ihsanmokhsen.github.io`.
> 2. Repo *Settings → Pages → Custom domain* → isi `hilmimokhsen.com` → *Save* → tunggu cek DNS hijau → centang *Enforce HTTPS*.
> 3. Baru setelah itu lanjut ke langkah 1 (Search Console). **Jangan daftarkan alamat github.io ke Search Console.** Halaman ini sudah menunjuk `hilmimokhsen.com` sebagai alamat resmi (canonical).

- [ ] Website dapat dibuka di `https://hilmimokhsen.com` (pakai **https**, bukan http).
- [ ] `https://www.hilmimokhsen.com` otomatis dialihkan ke `https://hilmimokhsen.com` (atau sebaliknya, asal konsisten). Situs ini memakai alamat **tanpa www** di canonical, sitemap, dan data terstruktur.
- [ ] File berikut bisa dibuka:
  - `https://hilmimokhsen.com/robots.txt`
  - `https://hilmimokhsen.com/sitemap.xml`
  - `https://hilmimokhsen.com/llms.txt`
  - `https://hilmimokhsen.com/og-image.jpg`

**Pilihan hosting dari repo ini (gratis):**

| Hosting | Cara singkat |
|---|---|
| Cloudflare Pages | *Workers & Pages → Create → Pages → Connect to Git* → pilih repo ini → Build command dikosongkan, output directory `/` → tambahkan custom domain `hilmimokhsen.com`. |
| Netlify | *Add new site → Import from Git* → pilih repo → tanpa build command, publish directory `/` → *Domain management* → tambahkan domain. |
| Vercel | *Add New → Project* → import repo → Framework preset "Other" → tambahkan domain. |
| GitHub Pages | Repo *Settings → Pages* → Source: branch `main`, folder `/ (root)` → isi Custom domain `hilmimokhsen.com` → centang *Enforce HTTPS*. |

Setiap push ke branch `main` otomatis memperbarui website.

---

## 1. Google Search Console

### 1a. Tambahkan properti
1. Buka <https://search.google.com/search-console> dan login dengan akun Google milik Hilmi.
2. Klik **Tambahkan properti** → pilih **Domain** → isi `hilmimokhsen.com`.
3. Google memberi kode **TXT** (contoh: `google-site-verification=xxxx`).
4. Masuk ke pengelola DNS domain (tempat domain dibeli, atau Cloudflare jika DNS dikelola di sana) → tambahkan record:
   - Type: `TXT`
   - Name/Host: `@`
   - Value: kode dari Google
5. Kembali ke Search Console → klik **Verifikasi**. Jika gagal, tunggu 10–60 menit lalu coba lagi.

> **Alternatif tanpa akses DNS:** pilih tipe **Awalan URL** → `https://hilmimokhsen.com/` → metode **Tag HTML**. Salin tag `<meta name="google-site-verification" ...>` lalu tempel di `index.html` tepat di bawah baris `<meta name="robots" ...>`. Commit, push, tunggu situs ter-update, lalu klik Verifikasi.

### 1b. Kirim sitemap
- [ ] Menu **Peta Situs** → isi `sitemap.xml` → **Kirim**. Status harus "Berhasil".

### 1c. Minta Google mengindeks halaman utama
- [ ] Menu **Inspeksi URL** → tempel `https://hilmimokhsen.com/` → **Minta Pengindeksan**.
- Ulangi langkah ini setiap kali ada perubahan isi yang penting.

### 1d. Cek setelah 3–7 hari
- [ ] **Halaman** → `https://hilmimokhsen.com/` berstatus *Diindeks*.
- [ ] **Peningkatan / Enhancements** → muncul **Profile page** tanpa error (dari data terstruktur ProfilePage + Person).
- [ ] **Performa** → pantau kata kunci: `hilmi mokhsen`, `hilmiyatillah mokhsen`, `content creator ntt`, `influencer kupang`, `influencer ntt`, `pembicara public speaking kupang`.

---

## 2. Bing Webmaster Tools (penting untuk ChatGPT & Copilot)

ChatGPT Search dan Microsoft Copilot mengambil hasil pencarian dari indeks Bing, jadi langkah ini sama pentingnya dengan Google.

1. Buka <https://www.bing.com/webmasters> → login (bisa pakai akun Google).
2. Pilih **Import from Google Search Console**. Situs dan sitemap otomatis ikut, tanpa perlu verifikasi ulang.
   - Jika ingin manual: **Add site** → `https://hilmimokhsen.com/` → verifikasi dengan DNS (CNAME) atau meta tag → **Sitemaps** → kirim `https://hilmimokhsen.com/sitemap.xml`.
3. [ ] **URL Submission** → kirim `https://hilmimokhsen.com/`.

### 2a. IndexNow (memberi tahu Bing secara instan setiap ada update)
Repo ini sudah berisi file kunci IndexNow: `a8c13b5b11f978badb6f3cb9f1b7ed9c.txt` (di folder utama). Jangan dihapus atau diganti namanya.

Setelah website online, dan **setiap kali website diperbarui**, jalankan:

```bash
curl "https://api.indexnow.org/indexnow?url=https://hilmimokhsen.com/&key=a8c13b5b11f978badb6f3cb9f1b7ed9c"
```

Respons `200` atau `202` berarti berhasil. IndexNow juga dipakai Yandex, Seznam, dan Naver.

---

## 3. Uji data terstruktur & tampilan link

- [ ] **Rich Results Test**: <https://search.google.com/test/rich-results> → masukkan `https://hilmimokhsen.com/` → pastikan *Profile page* terdeteksi tanpa error.
- [ ] **Schema Markup Validator**: <https://validator.schema.org/> → masukkan URL → harus ada `Person`, `ProfilePage`, `WebSite`, `EducationEvent` ×2, `Event`, `ScholarlyArticle` ×2, `Book`, tanpa error.
- [ ] **PageSpeed Insights**: <https://pagespeed.web.dev/> → cek versi *Mobile*; target skor Performance ≥ 90.
- [ ] **Pratinjau link WhatsApp/Facebook**: <https://developers.facebook.com/tools/debug/> → masukkan URL → klik *Scrape Again* agar gambar `og-image.jpg` muncul saat link dibagikan.

---

## 4. Tautan dari sosial media (sinyal paling kuat untuk AI)

AI dan Google memastikan situs ini resmi milik Hilmi dengan melihat tautan dua arah: website → akun, dan akun → website.

- [ ] Instagram @hilmimokhsen → *Edit profil → Tautan* → tambahkan `https://hilmimokhsen.com`
- [ ] TikTok @hilmimokhsen → *Edit profil → Situs web*
- [ ] YouTube → *Kustomisasi channel → Info dasar → Link*
- [ ] Threads @hilmimokhsen → *Edit profil → Link*
- [ ] X @HilmiMokhsen → *Edit profile → Website*
- [ ] Jika link bio memakai tr.ee/Linktree, taruh hilmimokhsen.com di urutan **paling atas**.

---

## 5. Profil dosen di website Undana

Klaim "dosen Undana" saat ini belum tercantum di sumber publik mana pun. Profil resmi di domain `undana.ac.id` adalah bukti paling kuat bagi Google dan AI.

- [ ] Minta admin Prodi/Fakultas membuat atau memperbarui halaman profil dosen atas nama **Hilmiyatillah Mokhsen, S.Sos., M.I.Kom.**, dengan tautan ke `https://hilmimokhsen.com`.
- [ ] Jika ada, daftarkan juga profil **SINTA** dan **Google Scholar**. Masukkan jurnal IJIS 2025 (DOI `10.55927/ijis.v4i11.668`).
- [ ] Setelah halaman profil tersebut ada, kirim URL-nya ke developer agar ditambahkan ke `sameAs` di data terstruktur `index.html` dan ke `llms.txt`.

---

## 6. Wikidata (opsional, berdampak besar untuk AI)

Wikidata dipakai Google Knowledge Graph dan banyak model AI sebagai sumber fakta. Entri harus didukung referensi yang dapat diverifikasi, dan sumber yang sudah ada cukup memadai (jurnal MUKASI 2026, berita ANTARA/Undana/DelikNTT, detikcom).

1. Buat akun di <https://www.wikidata.org> → **Create a new Item**.
2. Label: `Hilmi Mokhsen` · Description: `Indonesian content creator and lecturer from Kupang` · Also known as: `Hilmiyatillah Mokhsen`.
3. Tambahkan pernyataan, masing-masing dengan referensi URL:

| Properti | Isi |
|---|---|
| instance of (P31) | human |
| given name (P735) / family name (P734) | Hilmi / Mokhsen |
| occupation (P106) | influencer, content creator, lecturer, master of ceremonies |
| educated at (P69) | Syarif Hidayatullah State Islamic University Jakarta; Nusa Cendana University |
| employer (P108) | Nusa Cendana University |
| residence (P551) | Kupang |
| official website (P856) | https://hilmimokhsen.com |
| Instagram username (P2003) | hilmimokhsen |
| TikTok username (P7085) | hilmimokhsen |
| X username (P2002) | HilmiMokhsen |

> Hanya masukkan fakta yang ada sumbernya. Entri tanpa referensi bisa dihapus moderator.

---

## 7. Perawatan rutin

**Setiap 1–2 bulan:**
- [ ] Perbarui angka pengikut di 3 tempat yang sama:
  1. `index.html` → bagian `<dl class="stats">` (teks yang terlihat) dan teks "Data per …"
  2. `index.html` → `interactionStatistic` di dalam `<script type="application/ld+json">`
  3. `llms.txt` → baris "Audiens"
- [ ] Perbarui tanggal `dateModified` (ProfilePage di `index.html`) dan `<lastmod>` di `sitemap.xml` ke tanggal hari itu.
- [ ] Push ke GitHub → jalankan perintah IndexNow (langkah 2a) → *Minta Pengindeksan* di Search Console (langkah 1c).

**Setiap ada acara atau publikasi baru:**
- [ ] Tambahkan baris di bagian **Pernah Bicara Di** atau **Publikasi** pada `index.html`, sertakan tautan ke berita atau jurnalnya.
- [ ] Tambahkan item yang sama di data terstruktur (`EducationEvent` / `ScholarlyArticle`) dan di `llms.txt`.

**Lainnya:**
- [ ] Hapus banner **#BantuNTT** di `index.html` (ditandai komentar `Aksi sosial — hapus blok ini…`) jika kampanye sudah selesai.

---

## 8. Cek bagaimana AI mengenali Hilmi (setiap bulan)

Tanyakan ke ChatGPT (mode Search), Perplexity, Gemini, dan Claude:

- "Siapa Hilmi Mokhsen?"
- "Siapa Hilmiyatillah Mokhsen?"
- "Rekomendasi content creator atau influencer NTT dari Kupang untuk endorse"
- "Pembicara public speaking di Kupang"

Catat apakah hilmimokhsen.com dikutip sebagai sumber. Jika ada jawaban yang salah, perbaiki atau perjelas faktanya di `index.html` dan `llms.txt`, lalu ulangi langkah perawatan di atas.

---

## Ringkasan file di repo

| File | Fungsi |
|---|---|
| `index.html` | Halaman utama, termasuk data terstruktur schema.org (JSON-LD) |
| `llms.txt` | Ringkasan fakta untuk AI (ChatGPT, Claude, Perplexity, dll.) |
| `robots.txt` | Mengizinkan mesin pencari & bot AI, menunjuk ke sitemap |
| `sitemap.xml` | Daftar halaman & foto untuk Google/Bing |
| `a8c13b5b11f978badb6f3cb9f1b7ed9c.txt` | Kunci IndexNow (Bing) — jangan dihapus |
| `og-image.jpg` | Gambar pratinjau saat link dibagikan |
| `assets/` | Foto (WebP + JPG) |
| `favicon.svg`, `apple-touch-icon.png`, `icon-512.png`, `site.webmanifest` | Ikon & manifest |
