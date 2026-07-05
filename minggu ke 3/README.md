# Reverse Engineering
## Week 3 - Analisis Kode Statis (Static Analysis)

---

# Capaian Pembelajaran

Setelah mengikuti perkuliahan pada minggu ketiga, mahasiswa diharapkan mampu memahami konsep **Static Analysis**, menjelaskan tujuan dan manfaat analisis statis dalam Reverse Engineering, menggunakan berbagai tools untuk menganalisis file executable tanpa menjalankannya, mengidentifikasi struktur program, fungsi, string, import library, serta mengenali indikasi malware melalui analisis statis. Mahasiswa juga diharapkan mampu membuat laporan hasil analisis menggunakan tools seperti **Ghidra**, **IDA Free**, **Detect It Easy (DIE)**, dan **PEStudio**.

---

# Pendahuluan

Pada minggu sebelumnya telah dipelajari mengenai struktur file executable dan bagaimana sebuah program disusun dalam bentuk machine code. Langkah berikutnya dalam proses Reverse Engineering adalah melakukan **Static Analysis**. Static Analysis merupakan teknik analisis terhadap sebuah file executable tanpa menjalankan program tersebut. Tujuannya adalah memperoleh informasi sebanyak mungkin mengenai karakteristik program, struktur internal, fungsi-fungsi yang digunakan, serta kemungkinan adanya aktivitas berbahaya.

Static Analysis merupakan tahapan pertama yang hampir selalu dilakukan oleh seorang reverse engineer maupun malware analyst karena metode ini relatif aman dan tidak memberikan risiko menjalankan malware secara langsung. Dengan melakukan analisis statis, seorang analis dapat memperoleh gambaran awal mengenai program sebelum melanjutkan ke tahap Dynamic Analysis.

---

# 1. Pengertian Static Analysis

Static Analysis adalah proses menganalisis sebuah program tanpa mengeksekusinya. Analisis dilakukan dengan membaca struktur executable, machine code, metadata, library yang digunakan, string yang tersimpan di dalam program, serta hubungan antar fungsi.

Keuntungan utama Static Analysis adalah program tidak perlu dijalankan sehingga risiko infeksi malware dapat diminimalkan. Selain itu, metode ini memungkinkan analis memperoleh informasi penting mengenai program sebelum melakukan analisis lebih lanjut.

Beberapa tujuan Static Analysis antara lain:

- Mengetahui fungsi program.
- Mengidentifikasi compiler yang digunakan.
- Mengetahui arsitektur executable.
- Mengetahui library yang digunakan.
- Mengidentifikasi string penting.
- Menemukan indikasi malware.
- Memahami alur program.

---

# 2. Alur Static Analysis

Proses Static Analysis umumnya dilakukan secara bertahap.

```text
Executable

↓

Hash Analysis

↓

Detect Compiler

↓

Strings Analysis

↓

Import Analysis

↓

Disassembly

↓

Decompiler

↓

Control Flow Analysis

↓

Laporan Analisis
```

Setiap tahapan memberikan informasi yang berbeda sehingga analis dapat memahami karakteristik executable secara menyeluruh.

---

# 3. Hash Analysis

Hash merupakan nilai unik yang dihasilkan dari suatu file menggunakan algoritma kriptografi tertentu. Hash digunakan untuk memastikan integritas file dan mengidentifikasi apakah suatu executable pernah dianalisis sebelumnya.

Algoritma hash yang sering digunakan antara lain:

- MD5
- SHA-1
- SHA-256

Contoh hash:

```text
MD5

5d41402abc4b2a76b9719d911017c592
```

Jika satu byte saja berubah, maka nilai hash juga akan berubah. Oleh karena itu hash sering digunakan dalam malware analysis untuk mengidentifikasi sampel malware.

Tools yang digunakan:

- HashMyFiles
- PowerShell
- CertUtil
- VirusTotal

---

# 4. Strings Analysis

String Analysis merupakan teknik mencari teks yang tersimpan di dalam executable.

String sering memberikan informasi penting seperti:

- URL
- IP Address
- Nama File
- Password
- Registry Key
- Nama DLL
- Nama API

Contoh hasil String Analysis:

```text
cmd.exe

powershell.exe

kernel32.dll

CreateFileA

https://example.com
```

Melalui string tersebut seorang analis dapat memperkirakan perilaku program bahkan tanpa membaca assembly.

Tools:

- Strings (Sysinternals)
- FLOSS
- Ghidra
- IDA Free

---

# 5. Import Analysis

Import Analysis bertujuan mengetahui fungsi Windows API yang digunakan executable.

Contoh Import:

```text
KERNEL32.dll

CreateFileA

ReadFile

WriteFile

CloseHandle
```

Contoh lain:

```text
WS2_32.dll

socket()

connect()

recv()

send()
```

Dari informasi tersebut analis dapat memperkirakan bahwa program memiliki kemampuan komunikasi jaringan.

Beberapa API penting:

| API | Fungsi |
|------|---------|
| CreateFile | Membuat file |
| WriteFile | Menulis file |
| CreateProcess | Menjalankan proses baru |
| RegOpenKey | Membuka Registry |
| InternetOpen | Membuka koneksi Internet |
| VirtualAlloc | Alokasi Memory |
| LoadLibrary | Memuat DLL |

---

# 6. Export Analysis

Export Analysis dilakukan apabila file yang dianalisis merupakan Dynamic Link Library (DLL).

Export Table berisi daftar fungsi yang dapat digunakan oleh program lain.

Contoh:

```text
DllMain

EncryptData

DecryptData
```

Informasi ini membantu memahami layanan atau fungsi yang disediakan oleh DLL.

---

# 7. Entropy Analysis

Entropy digunakan untuk mengukur tingkat keacakan data pada executable.

Nilai entropy yang tinggi biasanya menunjukkan:

- File dipacking.
- File dienkripsi.
- Malware menggunakan obfuscation.

Rentang nilai entropy:

| Nilai | Interpretasi |
|--------|--------------|
| 0 - 3 | Sangat rendah |
| 4 - 6 | Normal |
| 7 - 8 | Sangat tinggi |

Tools:

- Detect It Easy
- PEStudio
- Exeinfo PE

---

# 8. Disassembly

Disassembly adalah proses mengubah machine code menjadi bahasa Assembly.

Contoh:

```assembly
push rbp

mov rbp,rsp

sub rsp,20

mov eax,1

ret
```

Disassembler membantu analis memahami instruksi yang dijalankan CPU.

Tools:

- Ghidra
- IDA Free
- Cutter
- Radare2

---

# 9. Decompiler

Decompiler mengubah assembly menjadi pseudo-code yang menyerupai bahasa C.

Contoh Assembly:

```assembly
mov eax,5

add eax,3
```

Pseudo-code:

```c
int a = 5;

a = a + 3;
```

Decompiler tidak menghasilkan source code asli, tetapi cukup membantu memahami logika program.

---

# 10. Control Flow Graph (CFG)

Control Flow Graph menggambarkan hubungan antar fungsi dan jalur eksekusi program.

Diagram sederhana:

```text
Start

↓

Login

↓

Valid?

├── Ya → Dashboard

└── Tidak → Exit
```

CFG membantu analis memahami alur program secara visual.

---

# 11. Pengenalan Assembly

Beberapa instruksi Assembly yang sering ditemui:

| Instruksi | Fungsi |
|-----------|---------|
| MOV | Memindahkan data |
| PUSH | Menyimpan data ke Stack |
| POP | Mengambil data dari Stack |
| CALL | Memanggil fungsi |
| RET | Kembali dari fungsi |
| CMP | Membandingkan data |
| JMP | Lompat |
| JE | Jump Equal |
| JNE | Jump Not Equal |

---

# 12. Tools Static Analysis

Berikut beberapa tools yang umum digunakan.

| Tools | Fungsi |
|---------|----------------|
| Detect It Easy | Deteksi Compiler dan Packer |
| PEStudio | Analisis PE |
| Ghidra | Disassembler dan Decompiler |
| IDA Free | Reverse Engineering |
| Cutter | GUI Radare2 |
| Radare2 | Binary Analysis |
| FLOSS | Strings Analysis |
| PE-bear | Analisis Section |

---

# Studi Kasus

Misalkan diperoleh file **sample.exe** yang diduga merupakan malware.

Langkah analisis:

1. Hitung nilai hash menggunakan SHA-256.
2. Buka file menggunakan Detect It Easy untuk mengetahui compiler dan packer.
3. Analisis struktur PE menggunakan PEStudio.
4. Lakukan Strings Analysis menggunakan FLOSS.
5. Periksa Import Table untuk mengetahui API yang digunakan.
6. Buka file menggunakan Ghidra.
7. Analisis fungsi utama (main).
8. Buat Control Flow Graph.
9. Dokumentasikan seluruh hasil analisis.

Dari proses tersebut, analis dapat menyimpulkan apakah executable memiliki perilaku mencurigakan sebelum dijalankan.

---

# Ringkasan

Pada minggu ketiga mahasiswa mempelajari teknik **Static Analysis**, yaitu proses menganalisis executable tanpa menjalankannya. Materi meliputi Hash Analysis, Strings Analysis, Import Analysis, Export Analysis, Entropy Analysis, Disassembly, Decompiler, Control Flow Graph, serta penggunaan tools seperti Ghidra, IDA Free, Detect It Easy, PEStudio, FLOSS, dan PE-bear. Kemampuan melakukan Static Analysis menjadi dasar penting sebelum memasuki tahap Dynamic Analysis pada minggu berikutnya.

---

# Refleksi Pembelajaran

## Apa yang Dipelajari

Pada minggu ketiga saya mempelajari konsep Static Analysis sebagai salah satu metode utama dalam Reverse Engineering. Saya mempelajari cara menganalisis executable tanpa menjalankan program menggunakan teknik Hash Analysis, Strings Analysis, Import Analysis, Entropy Analysis, Disassembly, Decompiler, dan Control Flow Graph. Saya juga mengenal berbagai tools seperti Ghidra, Detect It Easy, PEStudio, FLOSS, PE-bear, dan IDA Free untuk membantu proses analisis.

---

## Apa yang Saya Pahami

Saya memahami bahwa Static Analysis merupakan langkah awal yang sangat penting sebelum menjalankan sebuah executable, terutama jika file tersebut dicurigai sebagai malware. Saya juga memahami bahwa informasi seperti hash, string, import library, dan struktur executable dapat memberikan gambaran mengenai fungsi program tanpa harus mengeksekusinya. Selain itu, saya mulai memahami bagaimana Ghidra menerjemahkan machine code menjadi assembly dan pseudo-code sehingga logika program lebih mudah dipahami.

---

## Apa yang Masih Membingungkan

Saya masih ingin mempelajari lebih dalam mengenai cara membaca assembly yang kompleks, memahami optimasi compiler terhadap machine code, serta menganalisis Control Flow Graph pada program yang memiliki banyak fungsi. Selain itu, saya juga ingin memahami bagaimana teknik anti-disassembly dan anti-decompiler bekerja sehingga dapat menghambat proses Reverse Engineering.

---
