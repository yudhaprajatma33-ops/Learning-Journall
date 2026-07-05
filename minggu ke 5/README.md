# Reverse Engineering
## Week 5 - Dynamic Analysis dan Debugging

---

# Capaian Pembelajaran

Setelah mengikuti perkuliahan pada minggu kelima, mahasiswa diharapkan mampu memahami konsep **Dynamic Analysis**, menjelaskan perbedaan antara Static Analysis dan Dynamic Analysis, menggunakan debugger untuk menganalisis perilaku program saat dijalankan, memonitor aktivitas proses, memori, registry, dan jaringan, serta mampu mendokumentasikan hasil analisis menggunakan berbagai tools Dynamic Analysis. Mahasiswa juga diharapkan mampu melakukan debugging dasar menggunakan **x64dbg** dan mengidentifikasi perilaku suatu executable ketika sedang berjalan.

---

# Pendahuluan

Pada minggu sebelumnya mahasiswa telah mempelajari bagaimana membangun laboratorium Reverse Engineering menggunakan Virtual Machine. Setelah lingkungan analisis selesai dipersiapkan, langkah berikutnya adalah melakukan **Dynamic Analysis**. Berbeda dengan Static Analysis yang dilakukan tanpa menjalankan program, Dynamic Analysis dilakukan dengan mengeksekusi program di lingkungan yang aman untuk mengamati perilakunya secara langsung.

Dynamic Analysis bertujuan untuk mengetahui aktivitas program ketika dijalankan, seperti proses yang dibuat, file yang diakses, registry yang dimodifikasi, koneksi jaringan yang dibangun, serta perubahan memori yang terjadi selama proses eksekusi. Teknik ini sangat penting dalam analisis malware karena banyak malware yang menyembunyikan perilaku sebenarnya hingga program dijalankan.

Melalui Dynamic Analysis, seorang reverse engineer dapat memahami alur eksekusi program, mengidentifikasi fungsi penting, serta memperoleh bukti digital mengenai aktivitas yang dilakukan oleh executable. Oleh karena itu, Dynamic Analysis merupakan tahapan lanjutan setelah Static Analysis dan menjadi salah satu kemampuan utama dalam Reverse Engineering.

---

# 1. Pengertian Dynamic Analysis

Dynamic Analysis adalah proses menganalisis sebuah program dengan cara menjalankannya di lingkungan yang terkontrol untuk mengamati perilaku program secara langsung.

Berbeda dengan Static Analysis yang hanya memeriksa isi file, Dynamic Analysis berfokus pada aktivitas yang terjadi ketika executable dijalankan.

Tujuan Dynamic Analysis antara lain:

- Mengetahui perilaku program saat berjalan.
- Mengidentifikasi aktivitas malware.
- Memantau perubahan registry.
- Memantau perubahan file.
- Mengamati komunikasi jaringan.
- Menganalisis penggunaan memori.
- Mengidentifikasi proses baru yang dibuat.

---

# 2. Perbedaan Static Analysis dan Dynamic Analysis

| Static Analysis | Dynamic Analysis |
|-----------------|------------------|
| Tidak menjalankan program | Menjalankan program |
| Aman terhadap malware | Memerlukan lingkungan aman |
| Lebih cepat | Lebih kompleks |
| Analisis struktur file | Analisis perilaku program |
| Tidak membutuhkan debugger | Membutuhkan debugger |

Kedua metode saling melengkapi. Dalam praktiknya, analis biasanya melakukan Static Analysis terlebih dahulu sebelum melanjutkan ke Dynamic Analysis.

---

# 3. Workflow Dynamic Analysis

Proses Dynamic Analysis dapat dilakukan melalui tahapan berikut:

```text
Executable

↓

Virtual Machine

↓

Monitoring Tools

↓

Debugger

↓

Program Execution

↓

Behavior Analysis

↓

Documentation
```

Workflow ini membantu analis memperoleh informasi secara sistematis selama proses analisis berlangsung.

---

# 4. Debugger

Debugger adalah perangkat lunak yang digunakan untuk mengontrol jalannya program saat sedang dieksekusi.

Fungsi debugger antara lain:

- Menghentikan program.
- Menjalankan program langkah demi langkah.
- Melihat isi register.
- Melihat isi memori.
- Mengubah nilai memori.
- Mengubah nilai register.
- Mengamati alur eksekusi.

Debugger merupakan alat utama dalam Dynamic Analysis.

---

# 5. x64dbg

x64dbg merupakan debugger open-source yang dirancang khusus untuk sistem operasi Windows.

Fitur utama:

- Breakpoint
- Memory Viewer
- Register Viewer
- Stack Viewer
- Disassembler
- Hex Dump
- Call Stack
- Plugin Support

Keunggulan x64dbg:

- Gratis.
- Mudah digunakan.
- Mendukung aplikasi 32-bit dan 64-bit.
- Banyak digunakan dalam komunitas Reverse Engineering.

---

# 6. Breakpoint

Breakpoint digunakan untuk menghentikan eksekusi program pada instruksi tertentu.

Jenis Breakpoint:

## Software Breakpoint

Breakpoint menggunakan instruksi INT3.

Kelebihan:

- Mudah digunakan.
- Cepat.

Kekurangan:

- Dapat dideteksi malware.

---

## Hardware Breakpoint

Breakpoint menggunakan fitur debug register pada CPU.

Kelebihan:

- Sulit dideteksi.
- Tidak mengubah kode program.

Kekurangan:

- Jumlahnya terbatas.

---

# 7. Step Into dan Step Over

Debugger menyediakan beberapa mode eksekusi.

## Step Into (F7)

Masuk ke dalam fungsi yang dipanggil.

Contoh:

```text
main()

↓

printf()

↓

instruksi printf
```

---

## Step Over (F8)

Melewati fungsi tanpa masuk ke dalamnya.

```text
main()

↓

printf()

↓

langsung ke instruksi berikutnya
```

---

## Run (F9)

Menjalankan program hingga breakpoint berikutnya.

---

# 8. Register Analysis

Selama proses debugging, register CPU akan berubah mengikuti jalannya program.

Register penting:

| Register | Fungsi |
|----------|--------|
| RAX | Hasil operasi |
| RBX | Base Register |
| RCX | Counter |
| RDX | Data |
| RIP | Instruction Pointer |
| RSP | Stack Pointer |
| RBP | Base Pointer |

Mengamati perubahan register membantu memahami bagaimana program memproses data.

---

# 9. Memory Analysis

Memory Analysis bertujuan untuk melihat data yang disimpan di RAM saat program berjalan.

Informasi yang dapat diamati:

- Heap
- Stack
- String
- Variabel
- Buffer
- Shellcode

Tools:

- x64dbg
- Process Hacker
- Process Explorer

---

# 10. API Monitoring

Windows API adalah kumpulan fungsi yang digunakan aplikasi untuk berinteraksi dengan sistem operasi.

Contoh API penting:

| API | Fungsi |
|------|---------|
| CreateFile | Membuat file |
| ReadFile | Membaca file |
| WriteFile | Menulis file |
| DeleteFile | Menghapus file |
| CreateProcess | Membuat proses |
| VirtualAlloc | Alokasi memori |
| LoadLibrary | Memuat DLL |
| InternetOpen | Membuka koneksi internet |

Melalui API Monitoring, analis dapat mengetahui aktivitas program secara rinci.

---

# 11. Registry Monitoring

Registry Windows menyimpan konfigurasi sistem operasi dan aplikasi.

Malware sering memodifikasi registry untuk:

- Persistence
- Startup otomatis
- Menyembunyikan aktivitas

Tools:

- Process Monitor
- Regshot
- Autoruns

---

# 12. File System Monitoring

Program dapat melakukan berbagai aktivitas terhadap file.

Contoh:

- Membuat file.
- Menghapus file.
- Mengubah file.
- Menyalin file.

Monitoring dilakukan menggunakan:

- Process Monitor
- Process Hacker

---

# 13. Network Monitoring

Malware modern umumnya melakukan komunikasi jaringan.

Aktivitas yang dapat diamati:

- DNS Query
- HTTP Request
- HTTPS
- TCP Connection
- UDP Connection

Tools:

- Wireshark
- TCPView
- FakeNet
- INetSim

---

# 14. Process Monitoring

Ketika program dijalankan, dapat terjadi:

- Membuat Process baru.
- Membuat Thread baru.
- Inject Process.
- Suspend Process.

Tools:

- Process Hacker
- Process Explorer

---

# 15. Call Stack

Call Stack menunjukkan urutan fungsi yang sedang dipanggil.

Contoh:

```text
main()

↓

login()

↓

encrypt()

↓

sendData()
```

Call Stack membantu memahami hubungan antar fungsi selama program berjalan.

---

# 16. Studi Kasus

Misalkan diperoleh file **sample.exe** yang diduga merupakan malware.

Langkah analisis:

1. Jalankan pada Virtual Machine.
2. Aktifkan Process Monitor.
3. Aktifkan Wireshark.
4. Buka x64dbg.
5. Pasang breakpoint pada Entry Point.
6. Jalankan program.
7. Amati register.
8. Amati Call Stack.
9. Analisis perubahan registry.
10. Analisis koneksi jaringan.
11. Simpan hasil analisis.

Dari proses tersebut analis dapat mengetahui perilaku malware secara lengkap tanpa merusak sistem operasi utama.

---

# Ringkasan

Pada minggu kelima mahasiswa mempelajari Dynamic Analysis sebagai teknik untuk menganalisis perilaku program ketika dijalankan. Materi meliputi penggunaan debugger, breakpoint, register analysis, memory analysis, API monitoring, registry monitoring, file system monitoring, network monitoring, process monitoring, serta call stack analysis. Mahasiswa juga mempraktikkan penggunaan x64dbg, Process Monitor, Wireshark, dan Process Hacker sebagai alat utama dalam Dynamic Analysis.


---

# Refleksi Pembelajaran

## Apa yang Dipelajari

Pada minggu kelima saya mempelajari konsep Dynamic Analysis sebagai metode untuk mengamati perilaku program saat dijalankan. Saya belajar menggunakan debugger x64dbg, memahami fungsi breakpoint, melakukan analisis register, memori, registry, file system, proses, dan jaringan. Saya juga mempelajari penggunaan Process Monitor, Process Hacker, Wireshark, dan TCPView untuk memonitor aktivitas executable secara langsung.

---

## Apa yang Saya Pahami

Saya memahami bahwa Dynamic Analysis memberikan informasi yang tidak dapat diperoleh hanya melalui Static Analysis. Dengan menjalankan program di Virtual Machine, saya dapat melihat perubahan yang terjadi pada sistem secara real-time, seperti pembuatan file, perubahan registry, komunikasi jaringan, dan penggunaan memori. Saya juga mulai memahami cara kerja debugger dalam menghentikan program, membaca register, dan menelusuri alur eksekusi menggunakan Step Into maupun Step Over.

---

## Apa yang Masih Membingungkan

Saya masih ingin mempelajari teknik debugging yang lebih lanjut, seperti analisis multi-thread, penanganan exception, teknik bypass anti-debugging, dan analisis malware yang menggunakan packing atau enkripsi tingkat lanjut. Selain itu, saya ingin memahami lebih dalam mengenai teknik memory dumping serta cara menganalisis shellcode yang dieksekusi langsung di memori.

---
