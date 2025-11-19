# **Sapa Tazkia – Web-Based AI Chatbot**

Chatbot akademik berbasis web yang dirancang untuk membantu mahasiswa dan calon pendaftar Institusi Tazkia dalam memperoleh informasi kampus secara cepat, akurat, dan tersedia 24/7. Sistem ini mengintegrasikan teknologi Retrieval-Augmented Generation (RAG), autentikasi mahasiswa, akses database akademik, serta fitur ekspor nilai/transkrip dalam format PDF.

## **1. Deskripsi Proyek**
Sapa Tazkia adalah aplikasi chatbot cerdas yang memanfaatkan Large Language Model (LLM) sebagai asisten virtual kampus. Aplikasi ini menyediakan layanan informasi akademik, administrasi, dan pendaftaran melalui percakapan natural.

## **Fitur utama:**
1. Chatbot berbasis RAG (jawaban akurat dari dokumen kampus)
2. Autentikasi mahasiswa menggunakan database akademik
3. Akses data nilai, IPK, dan riwayat akademik
4. Download transkrip otomatis dalam format PDF
5. History chat untuk pengguna yang login
6. Sistem aman, cepat, dan dapat diakses dari berbagai perangkat
7. Tujuan utama: meningkatkan efisiensi layanan informasi kampus, mengurangi beban staf, serta memberikan akses 24/7 bagi mahasiswa dan calon mahasiswa.

### **2. Arsitektur Sistem**
Sapa Tazkia menggunakan arsitektur modern dengan pemisahan Frontend, Backend, Relational Database, Vector Database, dan AI Processing Layer.

## **Alur kerja sistem:**
1. User mengirim pertanyaan dari frontend
2. Backend memvalidasi, menerapkan rate limit, dan melakukan embedding
3. Sistem melakukan pencarian dokumen dengan RAG melalui Qdrant
4. Backend mengirim context dan pertanyaan ke API LLM (Gemini/GPT)
5. LLM memberikan jawaban berdasarkan dokumen resmi
6. Backend memproses dan mengirim respon ke frontend
7. Pendekatan RAG digunakan untuk menghindari hallucination, memastikan jawaban akurat, serta memungkinkan pembaruan dokumen tanpa retrain model.

## **3. Technology Stack**

   ### **3.1Frontend Stack**
   
| Komponen           | Teknologi          | Keterangan                                                              |
|--------------------|--------------------|-------------------------------------------------------------------------|
| Framework          | React.js 18.2.0    | Library UI berbasis komponen yang cepat dan fleksibel                   |
| CSS Framework      | Tailwind CSS 3.4.1 | Utility-first CSS untuk desain responsif dan modern                     |
| State Management   | Redux / Zustand    | Mengelola state global seperti user session & chat history              |
| HTTP Client        | Axios              | Melakukan HTTP request ke backend dengan interceptor                    |
| UI Component       | shadcn/ui          | Komponen UI modern yang mudah dikustomisasi                             |
| Routing            | React Router v6    | Navigasi aplikasi tanpa reload halaman                                  |

  ### **3.2 Backend Stack**
  
| Komponen          | Teknologi            | Keterangan                                                              |
|-------------------|----------------------|-------------------------------------------------------------------------|
| Bahasa            | Node.js 20.12.2      | Runtime JavaScript untuk backend                                        |
| Framework         | Express.js 4.18.2     | Web framework minimalis dengan routing dan middleware                  |
| Authentication     | JWT                  | Sistem autentikasi berbasis token                                      |
| API Architecture   | RESTful API          | Komunikasi standar antara frontend dan backend                         |
| Password Hashing   | Bcrypt               | Keamanan password dengan hash + salt                                   |
| PDF Generator      | PDFKit / Puppeteer   | Generate dokumen PDF seperti nilai dan transkrip                       |

   ### **2.3 Database Stack**
   
| Komponen            | Teknologi        | Keterangan                                                             |
|---------------------|------------------|------------------------------------------------------------------------|
| Database Utama      | MySQL 8.0        | Menyimpan data user, nilai, jadwal, riwayat akademik                   |
| ORM                 | Prisma 5.x       | Query type-safe dan manajemen schema                                   |
| Database Migration  | Prisma Migrate   | Pengelolaan versi schema database                                      |
| Caching (Opsional)  | Redis 7.2        | Penyimpanan in-memory untuk mempercepat request berulang               |
| Connection Pooling  | Prisma Pool      | Optimasi koneksi database bawaan Prisma                                |


  ### **2.4 DevOps & Infrastruktur**
  
| Komponen                 | Teknologi         | Keterangan                                                              |
|--------------------------|-------------------|-------------------------------------------------------------------------|
| Hosting Frontend         | Vercel            | Deploy React dengan auto-scaling dan CDN                                |
| Hosting Backend          | Railway / Render   | Menjalankan Node.js backend di cloud                                   |
| CI/CD                    | GitHub Actions    | Otomatisasi build, test, dan deployment                                 |
| Containerization         | Docker            | Menjamin environment konsisten                                          |
| Orchestration            | Docker Compose    | Menjalankan multi-container aplikasi                                    |
| Version Control          | Git + GitHub      | Manajemen kode sumber                                                   |
| SSL/TLS                  | Let's Encrypt     | Enkripsi HTTPS gratis                                                   |

  ### **2.5 Security & Monitoring**

| Komponen         | Teknologi             | Keterangan                                                              |
|------------------|------------------------|------------------------------------------------------------------------|
| HTTP Security    | Helmet.js             | Melindungi Express dengan konfigurasi header HTTP                       |
| HTTPS Protocol   | TLS 1.3               | Enkripsi koneksi end-to-end                                             |
| Rate Limiting    | express-rate-limit    | Membatasi request untuk mencegah abuse                                  |
| Logging          | Winston               | Logging production-grade                                                |
| Error Tracking   | Sentry (opsional)     | Monitoring error real-time                                              |
| Monitoring       | Grafana + Prometheus  | Analitik performa dan visualisasi metrics                               |



## **3. Struktur Folder**

```text
SAPA-TAZKIA/
│
├── backend/
│   ├── config/
│   ├── prisma/
│   │   ├── schema.prisma
│   │   └── seed.js
│   ├── src/
│   │   ├── controllers/
│   │   │   ├── aiController.js
│   │   │   ├── authController.js
│   │   │   └── guestController.js
│   │   ├── middleware/
│   │   │   └── authMiddleware.js
│   │   ├── routes/
│   │   │   ├── aiRoutes.js
│   │   │   ├── authRoutes.js
│   │   │   └── guestRoutes.js
│   │   ├── services/
│   │   │   ├── academicService.js
│   │   │   ├── authService.js
│   │   │   ├── emailService.js
│   │   │   ├── openaiService.js
│   │   │   └── pdfService.js
│   │   ├── utils/
│   │   │   └── emailDomainValidator.js
│   │   └── app.js
│   ├── server.js
│   ├── .env
│   ├── .env.bakk
│   ├── package.json
│   └── package-lock.json
│
└── frontend/
    ├── public/
    ├── src/
    │   ├── api/
    │   │   ├── aiService.js
    │   │   └── axiosConfig.js
    │   ├── components/
    │   │   ├── chat/
    │   │   │   ├── ChatInput.jsx
    │   │   │   ├── ChatMessage.jsx
    │   │   │   └── ChatWindow.jsx
    │   │   ├── common/
    │   │   │   ├── AuthModal.jsx
    │   │   │   ├── Button.jsx
    │   │   │   ├── GoogleIcon.jsx
    │   │   │   ├── GradientText.jsx
    │   │   │   └── ProtectedRoute.jsx
    │   │   ├── layout/
    │   │   │   └── SideBar.jsx
    │   │   └── ConfirmationModal.jsx
    │   ├── context/
    │   │   └── AuthContext.js
    │   ├── pages/
    │   │   ├── AboutYouPage.jsx
    │   │   ├── AuthCallback.jsx
    │   │   ├── ChatPage.jsx
    │   │   ├── LandingPage.jsx
    │   │   └── LoginPage.jsx
    │   └── services/
    │       ├── aiService.js
    │       └── api.js
    └── package.json
```

## **4. Team Member**

1. **Muhammad Ichsan Junaedi (Project Manager, Frontend Developer, and Backend Developer)**  
   [LinkedIn – Muhammad Ichsan Junaedi](https://www.linkedin.com/in/muhammad-ichsan-junaedi-74039b288/)

2. **Rahmawati (Business Analyst)**  
   [LinkedIn – Rahmawati](https://www.linkedin.com/in/rahmawati-269732281/)

3. **Rafly Ariel Hidayat (Backend Developer)**  
   [LinkedIn – Rafly Ariel Hidayat](https://www.linkedin.com/in/rafly-ariel-hidayat-794406392/)

4. **Nabila Nurul Haq (UI/UX Designer)**  
   [LinkedIn – Nabila Nurul Haq](https://www.linkedin.com/in/nabila-nurul-haq-1b0694343/)


    
### **credit by : STMIK TAZKIA BOGOR [LinkedIn – STMIK Tazkia](https://www.linkedin.com/company/stmik-tazkia/)**

    






