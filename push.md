# 🚀 Panduan Lengkap Git & GitHub: Push dari PC Lain & Link Lain

Dokumentasi ini berisi panduan lengkap langkah demi langkah untuk mengelola repositori ini, baik dari PC saat ini, dari PC lain (kampus/laptop), maupun jika kamu ingin mengubah link repositori ke GitHub lain.

---

## 📌 Informasi Repositori
- **URL Repositori:** `https://github.com/Aditpakez/kisi-kisi-pab.git`
- **Branch Utama:** `main`

---

## 💻 1. Cara Push Update dari PC Ini (PC Sekarang)

Jika kamu telah selesai mengedit atau menambah fitur baru di PC ini, jalankan perintah berikut di terminal:

```bash
# 1. Cek file mana saja yang berubah
git status

# 2. Tambahkan semua perubahan ke staging
git add .

# 3. Buat commit dengan pesan yang jelas
git commit -m "Update fitur atau perbaikan kode"

# 4. Kirim (push) ke GitHub
git push
```

---

## 🖥️ 2. Cara Bekerja & Push Melalui PC Lain (PC Kampus / Laptop Lain)

Jika kamu sedang berada di kampus atau menggunakan komputer lain yang belum memiliki proyek ini:

### Langkah A: Ambil (Clone) Proyek dari GitHub
1. Buka terminal (CMD / PowerShell / Git Bash).
2. Pindah ke direktori tempat kamu ingin menyimpan proyek, misalnya `Documents` atau `Desktop`:
   ```bash
   cd Desktop
   ```
3. Clone proyek dari repositori kamu:
   ```bash
   git clone https://github.com/Aditpakez/kisi-kisi-pab.git
   ```
4. Masuk ke folder proyek yang baru diunduh:
   ```bash
   cd kisi-kisi-pab
   ```
5. Install dependensi Flutter:
   ```bash
   flutter pub get
   ```

### Langkah B: Konfigurasi Identitas Git (Wajib di PC Baru)
Agar nama kamu tercatat sebagai pembuat commit:
```bash
git config --global user.name "Aditpakez"
git config --global user.email "email_kamu@example.com"
```

### Langkah C: Lakukan Perubahan & Push ke GitHub
Setelah kamu mengedit kode di PC lain tersebut:
```bash
# 1. Cek file yang berubah
git status

# 2. Simpan semua perubahan
git add .

# 3. Buat commit
git commit -m "Pengerjaan dari PC kampus"

# 4. Push ke GitHub
git push origin main
```

> **Catatan Autentikasi di PC Lain:**
> Saat pertama kali menjalankan `git push`, Git akan meminta login akun GitHub. Kamu bisa:
> 1. Klik **"Sign in with your browser"** pada jendela pop-up yang muncul.
> 2. Atau jika menggunakan **Personal Access Token (PAT)**, masukkan username GitHub kamu dan masukkan Token sebagai password (bukan password akun biasa).

---

## 🔗 3. Cara Push ke Link Repository Lain (Ganti URL / Pindah Repo)

Jika kamu ingin mengunggah proyek ini ke repositori baru atau link GitHub yang berbeda:

### Kasus 1: Mengganti Link Remote yang Sudah Ada (Paling Sering Dipakai)
Jika repositori lokal sudah ada tapi kamu ingin mengarahkannya ke link repository baru:

```bash
# 1. Cek link remote yang sedang aktif saat ini
git remote -v

# 2. Ganti link origin ke link GitHub yang baru
git remote set-url origin https://github.com/USERNAME_BARU/NAMA_REPO_BARU.git

# 3. Pastikan link sudah berubah
git remote -v

# 4. Pastikan branch bernama main
git branch -M main

# 5. Push ke repository baru tersebut
git push -u origin main
```

---

### Kasus 2: Menambahkan Remote Tambahan (Memiliki 2 Target Push)
Jika kamu ingin menyimpan link lama, namun ingin menambahkan link cadangan:

```bash
# 1. Tambahkan remote baru dengan nama berbeda (misalnya 'backup')
git remote add backup https://github.com/USERNAME/REPO_CADANGAN.git

# 2. Push ke remote 'backup'
git push -u backup main

# 3. Ke depannya, jika ingin push ke remote backup:
git push backup main
```

---

### Kasus 3: Memulai Repo Baru dari Folder Biasa di PC Lain
Jika kamu meng-copy folder proyek ini via Flashdisk ke PC lain tanpa folder `.git`:

```bash
# 1. Masuk ke folder proyek
cd nama_folder_projek

# 2. Inisialisasi Git
git init

# 3. Buat branch main
git branch -M main

# 4. Hubungkan ke GitHub
git remote add origin https://github.com/Aditpakez/kisi-kisi-pab.git

# 5. Tambahkan semua file dan commit
git add .
git commit -m "Initial commit dari PC lain"

# 6. Push ke GitHub
git push -u origin main
```

---

## ⚠️ 4. Solusi Masalah / Error Umum (Troubleshooting)

### A. Error: `Updates were rejected because the remote contains work...`
- **Penyebab:** Ada perubahan di GitHub yang belum kamu ambil ke komputer lokal (misalnya kamu baru saja edit file di PC lain atau di web GitHub).
- **Solusi:**
  ```bash
  git pull origin main --rebase
  git push origin main
  ```

### B. Error: `remote origin already exists`
- **Penyebab:** Kamu menjalankan `git remote add origin ...` padahal remote `origin` sudah pernah dibuat.
- **Solusi:**
  Gunakan perintah `set-url` untuk mengubahnya:
  ```bash
  git remote set-url origin <LINK_BARU>
  ```

### C. Ingin Mengambil Update Terbaru Sebelum Mulai Ngoding di PC Rumah/PC Lain
Selalu biasakan menarik update terbaru sebelum mulai bekerja:
```bash
git pull origin main
```

### D. Error `403: Permission denied` (Jika PC memiliki lebih dari 1 akun GitHub)
- **Penyebab:** Di PC kamu atau PC kampus, ada akun GitHub orang lain yang tersimpan di Windows Credential Manager / browser, sehingga Git otomatis memakai akun tersebut.
- **Solusi:**
  Paksa Git menggunakan username GitHub kamu dengan menyisipkan `USERNAME@` di depan URL repository:
  ```bash
  git remote set-url origin https://Aditpakez@github.com/Aditpakez/kisi-kisi-pab.git
  git push -u origin main
  ```
  Dengan cara ini, Git akan meminta verifikasi akun `Aditpakez` secara spesifik tanpa tertukar dengan akun lain.
