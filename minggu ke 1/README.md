# Reverse Engineering
## Week 1 - Arsitektur Sistem Komputer Modern

---

## Capaian Pembelajaran

Setelah mengikuti perkuliahan pada minggu pertama, mahasiswa diharapkan mampu memahami konsep dasar arsitektur komputer modern, menjelaskan hubungan antara perangkat keras dan perangkat lunak, memahami cara CPU mengeksekusi instruksi, mengenali fungsi register dan memori, memahami Instruction Set Architecture (ISA), serta menjelaskan bagaimana sistem operasi memuat sebuah executable ke dalam memori.

---

# 1. Pendahuluan

Reverse Engineering merupakan proses menganalisis suatu perangkat lunak maupun perangkat keras untuk memahami cara kerjanya tanpa memiliki akses terhadap source code. Dalam proses ini, seorang analis bekerja langsung terhadap file executable yang berisi machine code.

Agar mampu memahami machine code tersebut, diperlukan pengetahuan mengenai bagaimana komputer bekerja. Arsitektur komputer menjelaskan bagaimana CPU, RAM, storage, serta sistem operasi saling berinteraksi dalam menjalankan sebuah program.

Seluruh proses reverse engineering, baik static analysis maupun dynamic analysis, selalu berkaitan dengan arsitektur komputer.

---

# 2. Arsitektur Sistem Komputer

Arsitektur komputer merupakan rancangan konseptual mengenai cara perangkat keras menjalankan instruksi program.

Komponen utama sistem komputer terdiri atas:

- CPU
- RAM
- Storage
- Input Device
- Output Device
- Motherboard
- Bus

Hubungan antar komponen dapat digambarkan sebagai berikut.

```text
Input Device
      │
      ▼
+-------------+
|     CPU     |
+-------------+
      │
      ▼
+-------------+
|     RAM     |
+-------------+
      │
      ▼
Storage Device
```

---

# 3. Model Von Neumann

Model Von Neumann merupakan dasar dari hampir seluruh komputer modern.

Karakteristik utama:

- Data dan program berada pada memori yang sama.
- CPU mengambil instruksi satu per satu.
- Instruksi diproses menggunakan Fetch-Decode-Execute Cycle.

Komponen:

- CPU
- Memory
- Input
- Output
- Storage

Diagram:

```text
Program

↓

Memory

↓

CPU

↓

Execute
```

---

# 4. Struktur CPU

CPU terdiri atas beberapa komponen utama.

## Arithmetic Logic Unit (ALU)

Melakukan operasi matematika dan logika.

Contoh:

- Penjumlahan
- Pengurangan
- Perbandingan
- XOR
- AND
- OR

---

## Control Unit

Mengatur seluruh jalannya instruksi.

Tugasnya:

- Fetch
- Decode
- Execute
- Kontrol Bus

---

## Register

Merupakan memori tercepat pada CPU.

Register penting:

- RAX
- RBX
- RCX
- RDX
- RIP
- RSP
- RBP

---

# 5. Cache Memory

Cache mempercepat akses data.

Jenis cache:

| Level | Kecepatan | Kapasitas |
|--------|----------|-----------|
| L1 | Sangat Cepat | Sangat Kecil |
| L2 | Cepat | Sedang |
| L3 | Lebih Lambat | Besar |

---

# 6. Instruction Set Architecture (ISA)

ISA merupakan bahasa yang dipahami CPU.

Jenis ISA:

| ISA | Digunakan Pada |
|------|----------------|
| x86 | Windows 32-bit |
| x64 | Windows Modern |
| ARM | Smartphone |
| RISC-V | Embedded System |

---

# 7. Manajemen Memori

Ketika program dijalankan, sistem operasi membuat Virtual Memory.

Layout memori:

```text
+----------------+
|     Stack      |
+----------------+
|      Heap      |
+----------------+
|      BSS       |
+----------------+
|      Data      |
+----------------+
|      Text      |
+----------------+
```

Keterangan:

- Text → Machine Code
- Data → Variabel Global
- BSS → Variabel Belum Diinisialisasi
- Heap → Dynamic Memory
- Stack → Variabel Lokal

---

# 8. Siklus Eksekusi Program

CPU bekerja menggunakan Fetch Decode Execute.

```text
Program

↓

RAM

↓

CPU

↓

Fetch

↓

Decode

↓

Execute

↓

Result
```

---

# 9. Hubungan dengan Reverse Engineering

Reverse Engineering memanfaatkan seluruh konsep di atas.

Contohnya:

- Debugger membaca Register.
- Disassembler membaca Machine Code.
- Malware berjalan di Memory.
- Buffer Overflow menyerang Stack.

---

# Praktikum

## Tujuan

Mengenal struktur executable.

### Langkah

1. Install VirtualBox.
2. Install Windows VM.
3. Install PEStudio.
4. Install Detect It Easy.
5. Install Process Hacker.
6. Analisis file Notepad.exe.
7. Screenshot hasil.

---

# Ringkasan

Pada minggu pertama mahasiswa mempelajari dasar arsitektur komputer modern sebagai fondasi Reverse Engineering.

---
---

# Refleksi Pembelajaran

## Apa yang Dipelajari

Pada minggu pertama saya mempelajari dasar-dasar arsitektur sistem komputer modern sebagai fondasi dalam memahami Reverse Engineering. Materi yang dipelajari meliputi konsep arsitektur komputer, model Von Neumann, struktur CPU, fungsi Arithmetic Logic Unit (ALU), Control Unit (CU), register, cache memory, Instruction Set Architecture (ISA), manajemen memori, serta siklus eksekusi instruksi (Fetch-Decode-Execute). Selain itu, saya juga mempelajari bagaimana hubungan antara perangkat keras dan perangkat lunak ketika sebuah program dijalankan hingga akhirnya dapat dieksekusi oleh CPU.

Saya juga mengenal bagaimana sistem operasi memuat sebuah executable ke dalam memori serta memahami struktur dasar virtual memory yang terdiri dari Text Section, Data Section, BSS, Heap, dan Stack. Materi ini menjadi dasar untuk memahami proses analisis program pada pertemuan-pertemuan berikutnya.

---

## Apa yang Saya Pahami

Setelah mempelajari materi ini, saya memahami bahwa Reverse Engineering tidak hanya berfokus pada membaca kode program, tetapi juga membutuhkan pemahaman mengenai cara kerja komputer secara keseluruhan. Saya memahami bahwa CPU mengeksekusi program melalui proses Fetch, Decode, dan Execute secara berulang. Saya juga memahami fungsi masing-masing komponen CPU seperti register, cache, dan ALU dalam menjalankan instruksi.

Selain itu, saya memahami bahwa setiap program yang dijalankan akan ditempatkan ke dalam beberapa area memori yang memiliki fungsi berbeda, seperti Stack untuk variabel lokal, Heap untuk alokasi memori dinamis, serta Text Section sebagai tempat penyimpanan machine code. Pengetahuan ini sangat penting ketika melakukan analisis malware maupun debugging.

---

## Apa yang Masih Membingungkan

Beberapa materi yang masih perlu saya pelajari lebih dalam adalah bagaimana register berubah secara real-time ketika program sedang berjalan serta bagaimana CPU menerjemahkan opcode menjadi instruksi assembly. Saya juga masih ingin memahami lebih mendalam mengenai mekanisme virtual memory, paging, dan bagaimana sistem operasi mengatur alamat memori fisik dan virtual.

Selain itu, saya masih ingin mempelajari hubungan antara register, stack, dan instruction pointer ketika melakukan debugging menggunakan aplikasi seperti x64dbg atau Ghidra agar lebih memahami alur eksekusi program secara langsung.
