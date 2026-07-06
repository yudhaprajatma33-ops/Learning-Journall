
**Topik:** Analisis Malware Infostealer Menggunakan Reverse Engineering

## Materi Pembelajaran

Pada pertemuan ini saya mempelajari analisis sebuah file executable yang teridentifikasi sebagai malware infostealer. Analisis dilakukan menggunakan pendekatan Reverse Engineering untuk memahami struktur, fungsi, dan perilaku malware tanpa memiliki akses ke source code asli. Metode yang digunakan terdiri dari Static Analysis dan Dynamic Analysis.

### Reverse Engineering Malware

Reverse Engineering malware adalah proses membongkar dan menganalisis program berbahaya untuk mengetahui cara kerja, tujuan, serta teknik yang digunakan oleh penyerang. Proses ini sangat penting dalam bidang keamanan siber karena dapat membantu analis memahami ancaman dan menentukan langkah mitigasi yang tepat.

### Static Analysis

Static Analysis dilakukan tanpa menjalankan program. Teknik ini digunakan untuk mengidentifikasi informasi penting yang terdapat di dalam file executable.

Beberapa aktivitas yang dilakukan dalam static analysis:

- Analisis struktur Portable Executable (PE).
- Identifikasi strings yang mencurigakan.
- Analisis library dan API yang digunakan.
- Pemeriksaan nilai entropy untuk mendeteksi packing atau enkripsi.
- Dekompilasi kode menggunakan tools seperti dnSpy.

### Portable Executable (PE)

Portable Executable (PE) merupakan format standar file executable pada sistem operasi Windows. Struktur PE terdiri dari beberapa bagian penting:

- **DOS Header** : informasi kompatibilitas dengan sistem DOS.
- **PE Header** : berisi informasi arsitektur, jumlah section, dan entry point.
- **.text** : berisi kode program yang dieksekusi.
- **.data** : berisi data yang dapat berubah selama program berjalan.
- **.rdata** : berisi data hanya-baca seperti string dan konstanta.
- **.rsrc** : berisi resource seperti ikon, gambar, dan manifest.

### Dynamic Analysis

Dynamic Analysis dilakukan dengan menjalankan malware pada lingkungan yang aman seperti sandbox atau virtual machine. Tujuannya adalah untuk mengamati perilaku malware secara langsung.

Aktivitas yang diamati meliputi:

- Perubahan file pada sistem.
- Aktivitas registry.
- Proses yang berjalan.
- Aktivitas jaringan.
- Komunikasi dengan server Command and Control (C2).

### Teknik Malware yang Ditemukan

Berdasarkan hasil analisis, malware menggunakan beberapa teknik untuk menghindari deteksi:

#### Packing dan Enkripsi

Kode malware disembunyikan menggunakan packing dan enkripsi sehingga sulit dianalisis secara langsung.

#### Obfuscation

Nama fungsi dan variabel dibuat tidak jelas untuk mempersulit proses analisis.

#### Reflective Loading

Payload malware dimuat langsung ke memori menggunakan `Assembly.Load` tanpa membuat file baru pada disk sehingga lebih sulit dideteksi antivirus.

#### Steganografi

Malware menyembunyikan payload terenkripsi di dalam file gambar menggunakan manipulasi data piksel.

#### Persistence

Malware membuat dirinya tetap aktif setelah komputer direstart dengan memodifikasi registry Windows.

### Tools yang Digunakan

- VirusTotal
- ANY.RUN
- dnSpy
- Strings
- PE Tree

## Apa yang Dipahami

Saya memahami bahwa proses Reverse Engineering tidak hanya berfokus pada membaca kode program, tetapi juga memahami perilaku program saat dijalankan. Saya juga memahami bagaimana malware modern menggunakan teknik packing, obfuscation, reflective loading, dan steganografi untuk menghindari deteksi sistem keamanan.

Selain itu, saya memahami pentingnya penggunaan sandbox atau virtual machine untuk melakukan analisis secara aman tanpa membahayakan sistem utama.

## Hal yang Masih Membingungkan

Saya masih perlu mempelajari lebih dalam mengenai proses dekripsi payload yang disembunyikan menggunakan steganografi. Saya juga masih ingin memahami mekanisme kerja reflective loading secara detail pada lingkungan .NET serta teknik anti-debugging dan anti-sandbox yang digunakan malware modern untuk menghindari proses analisis.

## Kesimpulan

Materi ini memberikan pemahaman bahwa Reverse Engineering merupakan keterampilan penting dalam keamanan siber. Dengan menggabungkan Static Analysis dan Dynamic Analysis, seorang analis dapat mengidentifikasi fungsi, perilaku, serta tingkat bahaya sebuah malware sehingga dapat membantu dalam proses deteksi dan mitigasi ancaman keamanan.
