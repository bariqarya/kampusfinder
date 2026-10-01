# KAMPUSFINDER — Platform Riset Perguruan Tinggi Negeri Indonesia

> **"Temukan Kampus dan Jurusan yang Tepat untuk Masa Depanmu."**

KAMPUSFINDER adalah web application modern, *production-ready*, scalable, dan responsif yang dibangun untuk membantu calon mahasiswa Indonesia mencari Perguruan Tinggi Negeri (PTN), program studi, jalur penerimaan, informasi pendaftaran, perkiraan biaya UKT, serta layanan fasilitas aksesibilitas ramah disabilitas secara faktual dengan rujukan sumber resmi.

---

## 🌟 Prinsip Utama Aplikasi

1. **Non-Prescriptive (Tidak Menentukan Pilihan Pengguna)**: KAMPUSFINDER tidak memberikan skor semu, ranking sepihak, atau klaim manipulatif seperti *"kampus terbaik untuk Anda"*. Seluruh data disajikan secara objektif berdampingan agar calon mahasiswa dapat mengambil keputusan mandiri.
2. **Zero Fabrication (Tanpa Data Palsu)**: Jadwal, biaya, akreditasi, dan fasilitas tidak dikarang. Jika belum diumumkan sumber resmi, sistem secara transparan menampilkan *"Informasi belum tersedia"* atau *"Belum ditemukan sumber resmi"*.
3. **Official Verification System**: Setiap data dilengkapi status badge **TERVERIFIKASI** atau **BELUM DIVERIFIKASI**, tanggal audit pemeriksaan, serta tautan langsung ke portal resmi (SNPMB, PDDikti, BAN-PT, website universitas) dengan atribut keamanan `target="_blank" rel="noopener noreferrer"`.

---

## 🛠️ Tech Stack & Arsitektur

- **Framework**: [Next.js 14](https://nextjs.org/) (App Router, Server Components & Route Handlers)
- **UI & Styling**: [React 18](https://react.dev/), [TypeScript](https://www.typescriptlang.org/), [Tailwind CSS](https://tailwindcss.com/)
- **Icons**: [Lucide React](https://lucide.dev/)
- **ORM & Database**: [Prisma ORM](https://www.prisma.io/) dengan SQLite out-of-the-box (dapat langsung dialihkan ke PostgreSQL untuk production)
- **Authentication**: JWT berbasis `jose` dan `bcryptjs` password hashing dengan cookie session `httpOnly`
- **Validation**: [Zod](https://zod.dev/) untuk input API, registrasi, login, dan form admin
- **Testing**: Test suite otomatis terintegrasi (`tsx tests/test-flow.ts`)

---

## 📁 Struktur Direktori Proyek

```text
kampusfinder/
├── prisma/
│   ├── schema.prisma        # Skema database relasional 9 model
│   └── seed.ts              # Dataset seed realita PTN Indonesia
├── src/
│   ├── app/
│   │   ├── (public)
│   │   ├── layout.tsx       # Root layout + SEO metadata + semantic HTML
│   │   ├── page.tsx         # Homepage (Hero, search, metrics, categories)
│   │   ├── ptn/             # Direktori & Filter PTN (/ptn & /ptn/[slug])
│   │   ├── jurusan/         # Direktori Jurusan (/jurusan & /jurusan/[slug])
│   │   ├── jalur-masuk/     # Pusat Jalur Masuk SNBP, SNBT, Mandiri
│   │   ├── aksesibilitas/   # Direktori Fasilitas Disabilitas Kampus
│   │   ├── compare/         # Komparasi faktual hingga 4 PTN berdampingan
│   │   ├── favorit/         # Halaman Favorit Pengguna
│   │   ├── tentang/         # Kebijakan verifikasi data & transparansi
│   │   ├── dashboard/       # Dashboard User terautentikasi
│   │   ├── admin/           # Admin Dashboard CRUD & verifikasi audit
│   │   ├── login/           # Autentikasi Masuk Akun
│   │   ├── register/        # Registrasi Akun Pengguna
│   │   ├── sitemap.ts       # Generator sitemap dinamis SEO
│   │   ├── robots.ts        # Konfigurasi robots.txt
│   │   ├── not-found.tsx    # Halaman custom 404
│   │   ├── error.tsx        # Global error boundary (500)
│   │   └── api/             # REST API layer dengan proteksi role & Zod
│   ├── components/
│   │   ├── Navbar.tsx       # Navigation bar responsif + status auth
│   │   ├── Footer.tsx       # Footer + disclaimer + rujukan kementerian
│   │   ├── UniversityCard.tsx
│   │   ├── StudyProgramCard.tsx
│   │   ├── SourceCard.tsx
│   │   └── ui/              # Reusable design system components
│   ├── lib/
│   │   ├── prisma.ts        # Singleton Prisma Client
│   │   ├── auth.ts          # JWT helper, session, hash, requireAdmin
│   │   ├── validations.ts   # Zod schema definitions
│   │   └── utils.ts         # Indonesian formatters (Rupiah, tanggal)
│   └── middleware.ts        # Middleware proteksi route /admin dan /dashboard
├── tests/
│   └── test-flow.ts         # Automated test suite (17 tes lolos)
├── .env.example
├── package.json
└── README.md
```

---

## ⚙️ Environment Variables

Salin `.env.example` menjadi `.env`:

```env
# Koneksi Database
# Default lokal (SQLite tanpa konfigurasi rumit):
DATABASE_URL="file:./dev.db"

# Untuk PostgreSQL (jika menggunakan database server):
# DATABASE_URL="postgresql://user:password@localhost:5432/kampusfinder?schema=public"

# Kunci Rahasia JWT (minimal 32 karakter)
AUTH_SECRET="super-secret-key-change-this-in-production-min-32-chars-long"

# URL Publik Aplikasi
NEXT_PUBLIC_APP_URL="http://localhost:3000"
```

---

## 🚀 Panduan Menjalankan Proyek

### 1. Install Dependencies
```bash
npm install
```

### 2. Setup Database & Generate Prisma Client
```bash
npm run prisma:push
```

### 3. Seed Database dengan Data PTN Faktual
```bash
npm run prisma:seed
```
*Data seed mencakup akun Administrator, Demo User, PTN terkemuka (UI, ITB, UGM, ITS, UNAIR, UNDIP, UB, UNHAS, POLBAN), program studi, jadwal penerimaan 2025, biaya UKT, dan pusat layanan disabilitas.*

### 4. Menjalankan Server Development
```bash
npm run dev
```
Buka browser pada: `http://localhost:3000`

### 5. Menjalankan Automated Test
```bash
npm run test
```
*Memvalidasi pencarian, multi-faceted filtering, perbandingan, relasi database, hashing kata sandi, token JWT, dan validasi Zod.*

### 6. Build Production & Jalankan Server Production
```bash
npm run build
npm run start
```

---

## 🔑 Akun Bawaan (Development & Testing)

| Peran | Email | Kata Sandi | Akses |
|---|---|---|---|
| **Administrator** | `admin@kampusfinder.id` | `AdminKampus123!` | `/admin` (CRUD PTN, Prodi, Sumber, Role User) |
| **Demo User** | `user@kampusfinder.id` | `UserKampus123!` | `/dashboard`, simpan `/favorit`, `/compare` |

---

## 🔒 Fitur Keamanan & Validasi

- **Server-Side Authorization**: Proteksi route `/admin` dilakukan pada layer Next.js Middleware dan verifikasi ganda di API route handlers (`requireAdmin()`).
- **Input Sanitization**: Skema Zod memvalidasi format URL resmi, nilai numerik positif, string slug, dan batasan jenjang.
- **Audit-Friendly Timestamps**: Seluruh record PTN, prodi, dan sumber mencatat `createdAt`, `updatedAt`, dan `lastVerifiedAt`.
