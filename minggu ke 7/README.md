# Reverse Engineering
## Week 7 - Malware Analysis dan Teknik Anti-Reverse Engineering

---

# Capaian Pembelajaran

Setelah mengikuti perkuliahan pada minggu ketujuh, mahasiswa diharapkan mampu memahami konsep dasar **Malware Analysis**, mengenali berbagai jenis malware, memahami tahapan analisis malware, mengidentifikasi teknik yang digunakan malware untuk menghindari proses Reverse Engineering (Anti-Reverse Engineering), serta mampu melakukan analisis terhadap malware menggunakan kombinasi Static Analysis dan Dynamic Analysis. Mahasiswa juga diharapkan dapat mengenali indikator kompromi (Indicators of Compromise/IoC) serta menyusun laporan hasil analisis malware.

---

# Pendahuluan

Perkembangan teknologi informasi yang semakin pesat telah diikuti dengan meningkatnya ancaman keamanan siber. Salah satu ancaman terbesar adalah **malware (malicious software)**, yaitu perangkat lunak yang dirancang untuk merusak sistem, mencuri informasi, memperoleh akses tanpa izin, atau mengganggu operasional suatu perangkat.

Dalam dunia keamanan siber, Reverse Engineering menjadi salah satu metode utama untuk memahami cara kerja malware. Melalui proses Reverse Engineering, seorang analis dapat mengetahui bagaimana malware menginfeksi sistem, bagaimana malware berkomunikasi dengan server, serta bagaimana malware mempertahankan keberadaannya di dalam sistem korban.

Namun, malware modern telah dilengkapi dengan berbagai teknik **Anti-Reverse Engineering** yang bertujuan mempersulit proses analisis. Oleh karena itu, seorang reverse engineer harus memahami teknik-teknik tersebut agar mampu melakukan analisis secara efektif.

---

# 1. Pengertian Malware

Malware merupakan singkatan dari **Malicious Software**, yaitu perangkat lunak yang dibuat dengan tujuan melakukan aktivitas berbahaya pada sistem komputer tanpa izin pengguna.

Tujuan malware antara lain:

- Mencuri data pengguna.
- Mengambil alih sistem.
- Mengenkripsi file korban.
- Memata-matai aktivitas pengguna.
- Menghapus data.
- Menyebarkan malware lain.
- Menjadikan komputer sebagai bagian dari botnet.

---

# 2. Jenis-Jenis Malware

## Virus

Virus merupakan malware yang dapat menyisipkan dirinya ke dalam file lain dan menyebar ketika file tersebut dijalankan.

Karakteristik:

- Membutuhkan host file.
- Menyebar melalui media penyimpanan.
- Menginfeksi executable.

---

## Worm

Worm dapat menyebar secara otomatis melalui jaringan tanpa campur tangan pengguna.

Karakteristik:

- Tidak membutuhkan host.
- Menyebar melalui jaringan.
- Memanfaatkan vulnerability.

---

## Trojan

Trojan adalah malware yang menyamar sebagai aplikasi normal.

Contoh:

- Fake Antivirus
- Fake Installer
- Crack Software

---

## Ransomware

Ransomware mengenkripsi file korban kemudian meminta tebusan agar file dapat dikembalikan.

Contoh:

- WannaCry
- LockBit
- Ryuk

---

## Spyware

Spyware bertugas mengumpulkan informasi pengguna secara diam-diam.

Data yang dicuri:

- Password
- Cookie Browser
- Aktivitas Keyboard
- Screenshot

---

## Rootkit

Rootkit digunakan untuk menyembunyikan keberadaan malware dari sistem operasi maupun antivirus.

---

## Botnet Malware

Botnet menghubungkan komputer korban ke server Command and Control (C2) sehingga dapat dikendalikan dari jarak jauh.

---

# 3. Siklus Serangan Malware

```text
Pengiriman Malware

↓

Korban Menjalankan File

↓

Instalasi Malware

↓

Persistence

↓

Command & Control (C2)

↓

Payload

↓

Eksfiltrasi Data
```

Tahapan tersebut menunjukkan bagaimana malware bekerja mulai dari infeksi hingga menjalankan tujuan akhirnya.

---

# 4. Tahapan Malware Analysis

Analisis malware biasanya dilakukan melalui beberapa tahap berikut:

```text
Sample Malware

↓

Hash Analysis

↓

Static Analysis

↓

Dynamic Analysis

↓

Debugging

↓

Memory Analysis

↓

Laporan Analisis
```

Pendekatan ini membantu analis memperoleh gambaran lengkap mengenai perilaku malware.

---

# 5. Indicators of Compromise (IoC)

Indicators of Compromise (IoC) adalah bukti digital yang menunjukkan bahwa suatu sistem telah terinfeksi malware.

Contoh IoC:

- Hash file
- Nama proses
- Registry Key
- Domain
- IP Address
- URL
- File baru
- Scheduled Task

IoC digunakan untuk mendeteksi infeksi pada sistem lain.

---

# 6. Teknik Persistence Malware

Persistence merupakan teknik agar malware tetap aktif meskipun komputer telah direstart.

Beberapa metode yang sering digunakan:

- Startup Folder
- Registry Run Key
- Windows Service
- Scheduled Task
- DLL Hijacking
- WMI Event Subscription

Tools:

- Autoruns
- Process Monitor
- Regshot

---

# 7. Teknik Anti-Debugging

Malware sering mendeteksi keberadaan debugger untuk menghindari analisis.

Metode Anti-Debugging:

- IsDebuggerPresent()
- CheckRemoteDebuggerPresent()
- Timing Check
- Hardware Breakpoint Detection
- Exception Handling
- PEB Flag Detection

Tujuan:

- Menghentikan program.
- Menyembunyikan payload.
- Mengelabui analis.

---

# 8. Teknik Anti-Virtual Machine

Malware modern sering mendeteksi apakah dijalankan di Virtual Machine.

Metode yang digunakan:

- Memeriksa nama perangkat keras.
- Memeriksa MAC Address.
- Memeriksa Driver VMware.
- Memeriksa Registry VirtualBox.
- Memeriksa jumlah RAM.
- Memeriksa jumlah CPU.

Jika VM terdeteksi, malware dapat menghentikan eksekusinya sehingga perilaku sebenarnya tidak terlihat.

---

# 9. Teknik Obfuscation

Obfuscation adalah teknik menyamarkan kode agar sulit dipahami.

Contoh:

- String Encryption
- Junk Code
- Control Flow Flattening
- Instruction Substitution
- Opaque Predicate

Tujuan:

- Menghambat Reverse Engineering.
- Menghindari deteksi antivirus.

---

# 10. Packing dan Crypter

### Packing

Packing bertujuan memperkecil ukuran file sekaligus menyembunyikan isi executable.

Contoh packer:

- UPX
- MPRESS
- ASPack

### Crypter

Crypter mengenkripsi executable dan mendekripsinya saat dijalankan.

Perbedaan utama:

| Packing | Crypter |
|---------|----------|
| Kompresi file | Enkripsi file |
| Mudah di-unpack | Lebih sulit dianalisis |
| Tidak selalu berbahaya | Umumnya digunakan malware |

---

# 11. Command and Control (C2)

Command and Control adalah server yang digunakan malware untuk menerima perintah dari penyerang.

Aktivitas C2:

- Mengirim data korban.
- Mengunduh malware baru.
- Menjalankan perintah.
- Memperbarui malware.

Monitoring dilakukan menggunakan:

- Wireshark
- FakeNet
- INetSim

---

# 12. Memory Analysis

Beberapa malware hanya berjalan di memori dan tidak meninggalkan file pada hard disk.

Memory Analysis dilakukan untuk:

- Mengambil proses aktif.
- Menemukan shellcode.
- Mengidentifikasi DLL Injection.
- Mengambil artefak malware.

Tools:

- Volatility
- Rekall
- Process Hacker

---

# 13. YARA Rules

YARA digunakan untuk mengidentifikasi malware berdasarkan pola tertentu.

Contoh sederhana:

```yara
rule SuspiciousFile
{
    strings:
        $a = "CreateProcess"
        $b = "cmd.exe"

    condition:
        all of them
}
```

YARA sangat membantu dalam mendeteksi malware pada banyak file sekaligus.

---

# 14. Studi Kasus

Misalkan diperoleh file **invoice.exe** yang diduga merupakan malware.

Langkah analisis:

1. Hitung hash file menggunakan SHA-256.
2. Analisis compiler menggunakan Detect It Easy.
3. Analisis struktur PE menggunakan PEStudio.
4. Analisis string menggunakan FLOSS.
5. Jalankan file di Virtual Machine.
6. Monitor proses menggunakan Process Hacker.
7. Monitor Registry menggunakan Procmon.
8. Monitor jaringan menggunakan Wireshark.
9. Debug menggunakan x64dbg.
10. Dokumentasikan seluruh Indicators of Compromise (IoC).
11. Susun laporan hasil analisis.

---

# Ringkasan

Pada minggu ketujuh mahasiswa mempelajari konsep Malware Analysis, jenis-jenis malware, tahapan analisis malware, Indicators of Compromise (IoC), teknik persistence, serta berbagai teknik Anti-Reverse Engineering seperti Anti-Debugging, Anti-Virtual Machine, Obfuscation, Packing, dan Crypter. Mahasiswa juga mempelajari penggunaan tools seperti YARA, Volatility, Process Monitor, Wireshark, dan x64dbg untuk melakukan analisis malware secara menyeluruh.

---

# Refleksi Pembelajaran

## Apa yang Dipelajari

Pada minggu ketujuh saya mempelajari konsep Malware Analysis, berbagai jenis malware, siklus serangan malware, tahapan analisis malware, Indicators of Compromise (IoC), serta teknik Anti-Reverse Engineering seperti Anti-Debugging, Anti-Virtual Machine, Obfuscation, Packing, dan Crypter. Saya juga mempelajari penggunaan tools seperti YARA, Volatility, Wireshark, Process Monitor, dan x64dbg untuk membantu proses analisis.

---

## Apa yang Saya Pahami

Saya memahami bahwa malware modern memiliki mekanisme yang sangat kompleks untuk menyembunyikan aktivitasnya dan menghindari proses analisis. Saya juga memahami bahwa kombinasi Static Analysis dan Dynamic Analysis diperlukan agar perilaku malware dapat dipahami secara menyeluruh. Selain itu, saya mulai memahami pentingnya mengidentifikasi IoC sebagai dasar dalam mendeteksi infeksi pada sistem lain.

---

## Apa yang Masih Membingungkan

Saya masih ingin mempelajari lebih dalam mengenai teknik bypass Anti-Debugging dan Anti-Virtual Machine, proses analisis malware fileless yang berjalan di memori, serta cara membuat aturan YARA yang lebih kompleks agar mampu mendeteksi berbagai varian malware dengan tingkat akurasi yang tinggi.

---
 Laptops*.
