# Panduan Setup Google Search Console, Bing & AI — hilmimokhsen.my.id

Panduan ini berisi langkah setelah website online agar **hilmimokhsen.my.id** cepat terindeks Google, Bing, dan AI (ChatGPT, Gemini, Perplexity, Claude). Kerjakan berurutan dan centang yang sudah selesai.

> **Perkiraan waktu:** halaman biasanya terindeks dalam 2 hari–2 minggu setelah sitemap dikirim. Peringkat untuk kata kunci seperti "content creator NTT" butuh beberapa minggu sampai bulan, tergantung tautan dari luar (bio sosial media, media, Undana).

---

## 0. Pastikan website sudah online

> **Status (8 Oktober 2026): ✅ langkah 0 selesai.** Website online di **https://hilmimokhsen.my.id/** (GitHub Pages + custom domain, sertifikat HTTPS Let's Encrypt, *Enforce HTTPS* aktif). Domain dibeli di Sumopod (registrar PT Exabytes Network Indonesia, name server `ns1/ns2.sumopod.com`) dengan record DNS berikut, jangan diubah:
>
> | Type | Name / Host | Value / Target | TTL |
> |---|---|---|---|
> | A | `@` | `185.199.108.153` | 3600 |
> | A | `@` | `185.199.109.153` | 3600 |
> | A | `@` | `185.199.110.153` | 3600 |
> | A | `@` | `185.199.111.153` | 3600 |
> | CNAME | `www` | `ihsanmokhsen.github.io` | 3600 |
>
> `www.hilmimokhsen.my.id`, `http://`, dan alamat lama `ihsanmokhsen.github.io/hilmimokhsen.com/` semuanya dialihkan (301) ke `https://hilmimokhsen.my.id/`. File `CNAME` di repo menyimpan pengaturan domain ini, jadi jangan dihapus. **Domain berlaku sampai 7 Oktober 2027**: perpanjang sebelum tanggal itu. Lanjut ke langkah 1.

- [x] Website dapat dibuka di `https://hilmimokhsen.my.id` (pakai **https**, bukan http).
- [x] `https://www.hilmimokhsen.my.id` otomatis dialihkan ke `https://hilmimokhsen.my.id` (atau sebaliknya, asal konsisten). Situs ini memakai alamat **tanpa www** di canonical, sitemap, dan data terstruktur.
- [x] File berikut bisa dibuka:
  - `https://hilmimokhsen.my.id/robots.txt`
  - `https://hilmimokhsen.my.id/sitemap.xml`
  - `https://hilmimokhsen.my.id/llms.txt`
  - `https://hilmimokhsen.my.id/og-image.jpg`

**Pilihan hosting dari repo ini (gratis):**

| Hosting | Cara singkat |
|---|---|
| Cloudflare Pages | *Workers & Pages → Create → Pages → Connect to Git* → pilih repo ini → Build command dikosongkan, output directory `/` → tambahkan custom domain `hilmimokhsen.my.id`. |
| Netlify | *Add new site → Import from Git* → pilih repo → tanpa build command, publish directory `/` → *Domain management* → tambahkan domain. |
| Vercel | *Add New → Project* → import repo → Framework preset "Other" → tambahkan domain. |
| GitHub Pages | Repo *Settings → Pages* → Source: branch `main`, folder `/ (root)` → isi Custom domain `hilmimokhsen.my.id` → centang *Enforce HTTPS*. |

Setiap push ke branch `main` otomatis memperbarui website.

---

## 1. Google Search Console

### 1a. Tambahkan properti
1. Buka <https://search.google.com/search-console> dan login dengan akun Google milik Hilmi.
2. Klik **Tambahkan properti** → pilih **Domain** → isi `hilmimokhsen.my.id`.
3. Google memberi kode **TXT** (contoh: `google-site-verification=xxxx`).
4. Masuk ke pengelola DNS domain (tempat domain dibeli, atau Cloudflare jika DNS dikelola di sana) → tambahkan record:
   - Type: `TXT`
   - Name/Host: `@`
   - Value: kode dari Google
5. Kembali ke Search Console → klik **Verifikasi**. Jika gagal, tunggu 10–60 menit lalu coba lagi.

> **Alternatif tanpa akses DNS:** pilih tipe **Awalan URL** → `https://hilmimokhsen.my.id/` → metode **Tag HTML**. Salin tag `<meta name="google-site-verification" ...>` lalu tempel di `index.html` tepat di bawah baris `<meta name="robots" ...>`. Commit, push, tunggu situs ter-update, lalu klik Verifikasi.

### 1b. Kirim sitemap
- [ ] Menu **Peta Situs** → isi `sitemap.xml` → **Kirim**. Status harus "Berhasil".

### 1c. Minta Google mengindeks halaman utama
- [ ] Menu **Inspeksi URL** → tempel `https://hilmimokhsen.my.id/` → **Minta Pengindeksan**.
- Ulangi langkah ini setiap kali ada perubahan isi yang penting.

### 1d. Cek setelah 3–7 hari
- [ ] **Halaman** → `https://hilmimokhsen.my.id/` berstatus *Diindeks*.
- [ ] **Peningkatan / Enhancements** → muncul **Profile page** tanpa error (dari data terstruktur ProfilePage + Person).
- [ ] **Performa** → pantau kata kunci: `hilmi mokhsen`, `hilmiyatillah mokhsen`, `content creator ntt`, `influencer kupang`, `influencer ntt`, `pembicara public speaking kupang`.

---

## 2. Bing Webmaster Tools (penting untuk ChatGPT & Copilot)

ChatGPT Search dan Microsoft Copilot mengambil hasil pencarian dari indeks Bing, jadi langkah ini sama pentingnya dengan Google.

1. Buka <https://www.bing.com/webmasters> → login (bisa pakai akun Google).
2. Pilih **Import from Google Search Console**. Situs dan sitemap otomatis ikut, tanpa perlu verifikasi ulang.
   - Jika ingin manual: **Add site** → `https://hilmimokhsen.my.id/` → verifikasi dengan DNS (CNAME) atau meta tag → **Sitemaps** → kirim `https://hilmimokhsen.my.id/sitemap.xml`.
3. [ ] **URL Submission** → kirim `https://hilmimokhsen.my.id/`.

### 2a. IndexNow (memberi tahu Bing secara instan setiap ada update)
Repo ini sudah berisi file kunci IndexNow: `a8c13b5b11f978badb6f3cb9f1b7ed9c.txt` (di folder utama). Jangan dihapus atau diganti namanya.

Setelah website online, dan **setiap kali website diperbarui**, jalankan:

```bash
curl "https://api.indexnow.org/indexnow?url=https://hilmimokhsen.my.id/&key=a8c13b5b11f978badb6f3cb9f1b7ed9c"
```

Respons `200` atau `202` berarti berhasil. IndexNow juga dipakai Yandex, Seznam, dan Naver.

- [x] **8 Oktober 2026:** halaman utama dan `llms.txt` sudah dikirim ke IndexNow (respons `202` dari api.indexnow.org, `200` dari Bing).

---

## 3. Uji data terstruktur & tampilan link

- [ ] **Rich Results Test**: <https://search.google.com/test/rich-results> → masukkan `https://hilmimokhsen.my.id/` → pastikan *Profile page* terdeteksi tanpa error.
- [x] **Schema Markup Validator**: <https://validator.schema.org/> → masukkan URL → harus ada `Person`, `ProfilePage`, `WebSite`, `EducationEvent` ×2, `Event`, `ScholarlyArticle` ×2, `Book`, tanpa error. *(8 Oktober 2026: 0 error, 0 peringatan.)*
- [x] **Akses crawler AI** *(8 Oktober 2026)*: Googlebot, Bingbot, GPTBot, OAI-SearchBot, ClaudeBot, PerplexityBot, dan CCBot semuanya mendapat status `200` dan membaca seluruh isi halaman (776 kata) tanpa perlu JavaScript.
- [ ] **PageSpeed Insights**: <https://pagespeed.web.dev/> → cek versi *Mobile*; target skor Performance ≥ 90.
- [ ] **Pratinjau link WhatsApp/Facebook**: <https://developers.facebook.com/tools/debug/> → masukkan URL → klik *Scrape Again* agar gambar `og-image.jpg` muncul saat link dibagikan.

---

## 4. Tautan dari sosial media (sinyal paling kuat untuk AI)

AI dan Google memastikan situs ini resmi milik Hilmi dengan melihat tautan dua arah: website → akun, dan akun → website.

- [ ] Instagram @hilmimokhsen → *Edit profil → Tautan* → tambahkan `https://hilmimokhsen.my.id`
- [ ] TikTok @hilmimokhsen → *Edit profil → Situs web*
- [ ] YouTube → *Kustomisasi channel → Info dasar → Link*
- [ ] Threads @hilmimokhsen → *Edit profil → Link*
- [ ] X @HilmiMokhsen → *Edit profile → Website*
- [ ] Jika link bio memakai tr.ee/Linktree, taruh hilmimokhsen.my.id di urutan **paling atas**.

---

## 5. Profil dosen di website Undana

Klaim "dosen Undana" saat ini belum tercantum di sumber publik mana pun. Profil resmi di domain `undana.ac.id` adalah bukti paling kuat bagi Google dan AI.

- [ ] Minta admin Prodi/Fakultas membuat atau memperbarui halaman profil dosen atas nama **Hilmiyatillah Mokhsen, S.Sos., M.I.Kom.**, dengan tautan ke `https://hilmimokhsen.my.id`.
- [ ] Jika ada, daftarkan juga profil **SINTA** dan **Google Scholar**. Masukkan jurnal IJIS 2025 (DOI `10.55927/ijis.v4i11.668`).
- [ ] Setelah halaman profil tersebut ada, kirim URL-nya ke developer agar ditambahkan ke `sameAs` di data terstruktur `index.html` dan ke `llms.txt`.

---

## 6. Wikidata (opsional, berdampak besar untuk AI)

Wikidata dipakai Google Knowledge Graph dan banyak model AI sebagai sumber fakta. Entri harus didukung referensi yang dapat diverifikasi, dan sumber yang sudah ada cukup memadai (jurnal MUKASI 2026, berita ANTARA/Undana/DelikNTT, detikcom).

Datanya sudah disiapkan lengkap dengan referensi di [`docs/wikidata-quickstatements.txt`](wikidata-quickstatements.txt). Belum ada entri Wikidata untuk Hilmi (sudah dicek 8 Oktober 2026), jadi berkas ini membuat entri baru.

1. Buat akun di <https://www.wikidata.org> (*Create account*). QuickStatements mewajibkan akun berumur ≥ 4 hari dengan ≥ 50 suntingan; jika belum memenuhi, pakai cara manual di langkah 4.
2. Buka <https://quickstatements.toolforge.org> → *Log in* (memakai akun Wikidata) → *New batch*.
3. Salin seluruh isi `docs/wikidata-quickstatements.txt` → tempel → *Import V1 commands* → periksa daftarnya → *Run*.
4. **Cara manual:** di Wikidata klik *Create a new Item*, isi label/deskripsi/alias di bawah, lalu tambahkan setiap pernyataan lewat *+ add statement* beserta *reference URL*-nya:

| Properti | Isi (ID Wikidata) | Referensi (reference URL, P854) |
|---|---|---|
| Label / Description (id) | Hilmi Mokhsen · kreator konten, pembicara, dan dosen asal Kupang, Indonesia | — |
| Label / Description (en) | Hilmi Mokhsen · Indonesian content creator, speaker and lecturer from Kupang | — |
| Also known as | Hilmiyatillah Mokhsen · hilmimokhsen | — |
| instance of (P31) | human (Q5) | — |
| occupation (P106) | influencer (Q2906862) | doi.org/10.54259/mukasi.v5i1.6299 |
| occupation (P106) | content creator (Q109459317) | berita undana.ac.id (Entrepreneurship Skill, 2026) |
| occupation (P106) | master of ceremonies (Q497240) | berita delikntt.com (Lembata, 2025) |
| occupation (P106) | university teacher (Q1622272) | hilmimokhsen.my.id |
| employer (P108) | University of Nusa Cendana (Q7896000) | hilmimokhsen.my.id |
| educated at (P69) | Jakarta State Islamic University (Q12523349), kualifikasi *academic degree* (P512) = bachelor's degree (Q163727) | repository.uinjkt.ac.id (skripsi 2018) |
| educated at (P69) | University of Nusa Cendana (Q7896000), kualifikasi *academic degree* (P512) = master's degree (Q183816) | kupang.antaranews.com (M.I.Kom., 2026) |
| residence (P551) | Kupang (Q14155) | doi.org/10.54259/mukasi.v5i1.6299 |
| official website (P856) | https://hilmimokhsen.my.id/ | — |
| Instagram username (P2003) | hilmimokhsen | — |
| TikTok username (P7085) | hilmimokhsen | — |
| X username (P2002) | HilmiMokhsen | — |

5. Setelah entri jadi (misalnya `Q1234567`), kirim ID-nya ke developer agar ditambahkan ke `sameAs` di data terstruktur `index.html` dan ke `llms.txt`. Ini menautkan website dan Wikidata dua arah.

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

Catat apakah hilmimokhsen.my.id dikutip sebagai sumber. Jika ada jawaban yang salah, perbaiki atau perjelas faktanya di `index.html` dan `llms.txt`, lalu ulangi langkah perawatan di atas.

---

## Ringkasan file di repo

| File | Fungsi |
|---|---|
| `index.html` | Halaman utama, termasuk data terstruktur schema.org (JSON-LD) |
| `llms.txt` | Ringkasan fakta untuk AI (ChatGPT, Claude, Perplexity, dll.) |
| `robots.txt` | Mengizinkan mesin pencari & bot AI, menunjuk ke sitemap |
| `sitemap.xml` | Daftar halaman & foto untuk Google/Bing |
| `a8c13b5b11f978badb6f3cb9f1b7ed9c.txt` | Kunci IndexNow (Bing) — jangan dihapus |
| `docs/wikidata-quickstatements.txt` | Data siap-tempel untuk membuat entri Wikidata Hilmi |
| `CNAME` | Custom domain GitHub Pages (hilmimokhsen.my.id) — jangan dihapus |
| `og-image.jpg` | Gambar pratinjau saat link dibagikan |
| `assets/` | Foto (WebP + JPG) |
| `favicon.svg`, `apple-touch-icon.png`, `icon-512.png`, `site.webmanifest` | Ikon & manifest |
