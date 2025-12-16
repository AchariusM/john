# SIKP Oyako - Panduan Instalasi & Menjalankan Aplikasi (Windows)

Dokumen ini berisi panduan langkah demi langkah untuk menjalankan aplikasi SIKP Oyako (Backend & Frontend) di laptop Windows.

## Prasyarat (Prerequisites)

Sebelum memulai, pastikan software berikut sudah terinstal di laptop Anda:

1.  **Node.js (LTS Version)**
    *   Download dan instal dari: [https://nodejs.org/](https://nodejs.org/)
    *   Pilih versi **LTS** (Long Term Support).
    *   Setelah instalasi, buka Command Prompt (cmd) atau PowerShell dan ketik `node -v` dan `npm -v` untuk memastikan sudah terinstal.

2.  **Git**
    *   Download dan instal dari: [https://git-scm.com/download/win](https://git-scm.com/download/win)
    *   Gunakan pengaturan default saat instalasi.

3.  **Visual Studio Code (VS Code)** (Opsional, tapi sangat disarankan)
    *   Download dari: [https://code.visualstudio.com/](https://code.visualstudio.com/)

4.  **PostgreSQL Database** (Atau akun Supabase)
    *   Aplikasi ini menggunakan database PostgreSQL. Anda bisa menginstalnya secara lokal atau menggunakan layanan cloud seperti [Supabase](https://supabase.com/).

---

## Langkah 1: Clone Repository

1.  Buka folder di mana Anda ingin menyimpan proyek ini.
2.  Klik kanan dan pilih **Open Git Bash Here** (atau gunakan Terminal/CMD).
3.  Jalankan perintah berikut:
    ```bash
    git clone https://github.com/John/John.git
    ```
    *(Ganti URL di atas dengan URL repository yang sesuai jika berbeda)*
4.  Masuk ke folder proyek:
    ```bash
    cd John
    ```

---

## Langkah 2: Setup Backend

1.  Buka terminal baru (bisa di VS Code) dan masuk ke folder `backend`:
    ```bash
    cd backend
    ```

2.  **Instal Dependencies**:
    ```bash
    npm install
    ```

3.  **Konfigurasi Environment Variables**:
    *   Buat file baru bernama `.env` di dalam folder `backend`.
    *   Salin isi berikut ke dalam file `.env` dan sesuaikan nilainya:

    ```env
    # Server Configuration
    PORT=3000

    # Database Configuration (Supabase/PostgreSQL Connection String)
    # Format: postgresql://USER:PASSWORD@HOST:PORT/DATABASE?schema=public
    DATABASE_URL="postgresql://postgres:[PASSWORD]@[HOST]:[PORT]/postgres"

    # Supabase Configuration (Untuk fitur upload gambar/storage)
    SUPABASE_URL="https://your-project-id.supabase.co"
    SUPABASE_KEY="your-anon-key"

    # Security
    JWT_SECRET="rahasia_super_aman_ganti_ini"
    ```

4.  **Setup Database (Prisma)**:
    *   Generate Prisma Client:
        ```bash
        npx prisma generate
        ```
    *   Push schema ke database (membuat tabel):
        ```bash
        npx prisma db push
        ```
    *   (Opsional) Isi data awal (Seeding):
        ```bash
        node prisma/seed.js
        ```

5.  **Jalankan Backend**:
    ```bash
    npm run dev
    ```
    *   Jika berhasil, akan muncul pesan: `Server is running on port 3000`.
    *   Biarkan terminal ini tetap terbuka.

---

## Langkah 3: Setup Frontend

1.  Buka terminal **baru** (Terminal kedua) dan masuk ke folder `frontend`:
    ```bash
    cd frontend
    ```

2.  **Instal Dependencies**:
    ```bash
    npm install
    ```

3.  **Konfigurasi Environment Variables**:
    *   Buat file baru bernama `.env` di dalam folder `frontend`.
    *   Isi dengan konfigurasi berikut:

    ```env
    VITE_API_URL=http://localhost:3000
    ```

4.  **Jalankan Frontend**:
    ```bash
    npm run dev
    ```
    *   Terminal akan menampilkan URL lokal, biasanya `http://localhost:5173`.

---

## Langkah 4: Membuka Aplikasi

1.  Buka browser (Chrome, Edge, dll).
2.  Akses URL yang muncul di terminal frontend (contoh: `http://localhost:5173`).
3.  Login dengan akun yang sudah dibuat (jika sudah di-seed) atau daftar akun baru jika fitur registrasi aktif.

---

## Troubleshooting (Masalah Umum di Windows)

*   **'npm' is not recognized...**: Pastikan Node.js sudah terinstal dan Anda sudah me-restart terminal/VS Code setelah instalasi.
*   **Script execution disabled (PowerShell)**: Jika muncul error keamanan saat menjalankan script, jalankan perintah ini di PowerShell (Run as Administrator):
    ```powershell
    Set-ExecutionPolicy RemoteSigned
    ```
*   **Database Connection Error**: Pastikan `DATABASE_URL` di file `.env` backend sudah benar dan database server (PostgreSQL) sedang berjalan.

---

## Struktur Folder

*   `/backend`: Kode server (API), database schema, dan logika bisnis.
*   `/frontend`: Kode antarmuka pengguna (React + Vite).
