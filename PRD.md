# Product Requirement Document (PRD)
## LOKA — Your Business, Online

---

### 1. Product Overview
- **Nama Produk**: LOKA
- **Tagline**: *Your Business, Online*
- **Tipe Produk**: B2B SaaS Website & Landing Page Builder
- **Target Pengguna**: Pemilik bisnis lokal, UMKM, dan penyedia jasa (kuliner, klinik, salon, bengkel, retail, pet care) di Indonesia.
- **Value Proposition**: Solusi pembuatan landing page profesional instan tanpa coding, siap pakai dalam < 5 menit dengan bantuan AI atau drag-and-drop editor, dilengkapi integrasi WhatsApp bisnis dan subdomain instan.

---

### 2. Problem Statement & Objectives
#### Problem:
1. Pemilik UMKM kesulitan membuat landing page profesional (butuh coding atau biaya agensi mahal).
2. Platform existing (WordPress, Wix) terlalu rumit, berat, dan minim konteks bisnis lokal (jam buka/tutup dinamis, WhatsApp floating CTA, Open Graph preview WhatsApp).
3. Pembuatan copywriting dan visual memakan waktu lama.

#### Objectives:
1. Memberikan alur pembuatan landing page tercepat via AI Generator dan template industri lokal.
2. Menyediakan visual editor modular (drag-and-drop section) yang ramah pemula.
3. Menghasilkan landing page publik berkecepatan tinggi dengan subdomain otomatis (`namabisnis.ruuby.my.id`).
4. Memaksimalkan konversi bisnis lokal via WhatsApp Direct CTA dan status operasional real-time.

---

### 3. User Persona
- **Profil**: Pemilik usaha mikro, kecil, atau menengah (usia 20–45 tahun).
- **Literasi Digital**: Menengah-kebawah (terbiasa WhatsApp, Instagram, TikTok, namun tidak paham coding/DNS/hosting).
- **Goal**: Memiliki tautan resmi untuk bio Instagram/TikTok dan dibagikan ke calon pelanggan via WhatsApp agar bisnis terlihat terpercaya.

---

### 4. User Journey & Core Flow
```text
Daftar / Masuk
      ↓
Dashboard (Kelola Bisnis & Website)
      ↓
Pilih Metode:
┌─────────────────────────────────┐
│ A. AI Generator (Isi Profil)    │
│ B. Mulai dari Template Industri │
│ C. Halaman Kosong (Manual)      │
└────────────────┬────────────────┘
                 ↓
Visual Editor (Kustomisasi Konten & Seksi)
                 ↓
Live Interactive Preview (Desktop / Mobile)
                 ↓
Publish Website
                 ↓
Akses Live Subdomain (namabisnis.ruuby.my.id)
                 ↓
Share ke WhatsApp (Rich Link Preview / OG Card)
```

---

### 5. Detailed Features & Scope

#### 5.1. Autentikasi & Akun
- Register dan Login berbasis email & password.
- Session management berbasis token / JWT session.
- Multi-website management per user.

#### 5.2. AI Website Generator
- Form input profil bisnis sederhana: Nama, Kategori/Industri, Deskripsi, Target Audiens, Gaya Bahasa (Formal/Santai/Persuasif).
- Backend engine berbasis Google Gemini API (dengan fallback generative rules) untuk memproduksi:
  - Struktur sections yang relevan.
  - Copywriting judul, subjudul, benefit, review, dan FAQ.
  - Palet warna dan tema yang cocok dengan industri.

#### 5.3. Visual Drag-and-Drop Editor
- **Modular Sections**:
  - Hero / Banner Section
  - About / Story Section
  - Services / Menu / Product Catalog Section
  - Operating Hours & Contact Section (terkoneksi status Buka/Tutup)
  - Testimonial / Review Section
  - FAQ (Accordion) Section
  - Gallery Section
  - Location / Google Maps Embed Section
- **Kustomisasi Tema**: Pemilihan warna brand, typography, padding section, dan visual tone.
- **Responsive Preview Switcher**: Tampilan instan mode Desktop, Tablet, dan Mobile.
- **Section Controls**: Reorder seksi (drag-and-drop via dnd-kit), duplicate, delete, hide/show seksi.

#### 5.4. Business & Local Commerce Features
- **Floating WhatsApp Button**: Tombol chat mengambang dengan template pesan otomatis.
- **Smart Operating Hours**: Indikator dinamis ("Buka Sekarang" / "Tutup") sesuai jam dan hari operasional lokal.
- **Profil Kontak Lengkap**: Alamat, nomor telepon, WhatsApp, Instagram handle, maps embed.

#### 5.5. SEO & Social Share (WhatsApp Link Preview)
- Form pengaturan Title, Meta Description, dan OG Image.
- WhatsApp & Telegram live simulator di dalam editor.
- Bot crawler interceptor (Cloudflare Worker) untuk menyajikan rich preview metadata saat tautan dibagikan di media sosial atau chat app.

#### 5.6. Publishing & Domain Management
- **One-Click Publish/Unpublish**: Sinkronisasi status publikasi real-time.
- **Subdomain Otomatis**: Alokasi instan subdomain unik berbasis slug (`<slug>.ruuby.my.id`).
- **Custom Domain Ready**: Fondasi arsitektur untuk mapping domain kustom (fitur upgrade/premium).

#### 5.7. Administration & Monetization (Foundation)
- **Role & Admin Dashboard**: Pemantauan pengguna, situs aktif, dan analitik kunjungan.
- **Payment Gateway Integration**: Modul integrasi Midtrans untuk upgrade paket/berlangganan (Free vs Pro).

---

### 6. Technical Architecture & Tech Stack

#### 6.1. Tech Stack
- **Frontend**: React 18, TypeScript, Vite, Tailwind CSS, Lucide Icons, Framer Motion, `@dnd-kit`.
- **Backend**: Node.js, Express.js, TypeScript, PostgreSQL (Database), Docker container.
- **AI Engine**: Google Gemini API.
- **Infrastructure & Deployment**:
  - Frontend: Firebase Hosting
  - Backend & DB: Azure VM (Docker Compose)
  - Edge Routing & DNS: Cloudflare (Workers untuk subdomain proxy dan bot OG rendering).

#### 6.2. Architecture Diagram
```text
[ Browser / User ] ──► Cloudflare DNS / CDN ──► Firebase Hosting (React SPA)
                                │
                        (Bot / Crawler)
                                │
                                ▼
                       Cloudflare Worker
                       (Dynamic OG Inject)
                                │
[ API Requests ] ───────────────┼──────────────► Azure VM (Express + PostgreSQL)
                                                         │
                                                         ▼
                                                  Google Gemini AI
```

---

### 7. Non-Functional Requirements
- **Performance**: Waktu muat awal public landing page < 1.5 detik.
- **Responsiveness**: 100% responsif di mobile viewport (fokus utama pengguna WhatsApp).
- **Scalability**: Arsitektur stateless API dengan persistent SQL database.
- **Reliability**: Fail-safe AI generation (fallback generator jika AI API limit/gagal).
- **Security**: Validasi input (Zod), password hashing, proteksi CORS, dan sanitasi payload.

---

### 8. Implementation Status & Release Scope

Semua fitur dan tahapan dalam spesifikasi ini **telah sepenuhnya diimplementasikan (100% Implemented)** dan berjalan di lingkungan production:

| Fase & Komponen | Fitur yang Diimplementasikan | Status |
|---|---|---|
| **Fase 1: Core Engine & Auth** | Registrasi, Login JWT Session, Multi-website per user, Template sistem | ✅ Selesai (Live) |
| **Fase 2: AI & Local Features** | Gemini AI Generator, Dynamic Operating Hours, Floating WhatsApp CTA, Visual Drag-and-Drop Editor (`@dnd-kit`) | ✅ Selesai (Live) |
| **Fase 3: SEO, Social & Subdomain** | Subdomain routing otomatis (`namabisnis.ruuby.my.id`), WhatsApp link preview (Cloudflare Worker OG bot crawler), SEO live simulator | ✅ Selesai (Live) |
| **Fase 4: Infrastructure & Deploy** | Azure VM Docker Backend, Firebase Hosting Frontend, Cloudflare Edge Routing, Admin Panel & Midtrans payment base | ✅ Selesai (Live) |
