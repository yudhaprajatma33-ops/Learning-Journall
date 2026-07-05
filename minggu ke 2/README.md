# Reverse Engineering
## Week 2 - Binary dan Executable

---

## Capaian Pembelajaran

Mahasiswa mampu memahami struktur binary, executable, format PE, ELF, Mach-O, serta mampu melakukan analisis awal executable menggunakan tools static analysis.

---

# 1. Pendahuluan

Binary merupakan representasi data dalam bentuk angka 0 dan 1.

Dalam Reverse Engineering, objek utama analisis adalah executable yang telah dikompilasi.

Executable terdiri dari machine code yang dijalankan langsung oleh CPU.

---

# 2. Binary

Binary adalah data digital yang hanya memiliki dua keadaan.

Contoh:

```text
10010110
01100100
11001011
```

Machine Code merupakan binary yang dipahami CPU.

---

# 3. Proses Kompilasi

```text
Source Code

↓

Compiler

↓

Assembly

↓

Assembler

↓

Object File

↓

Linker

↓

Executable
```

Tahapan:

- Preprocessing
- Compilation
- Assembling
- Linking

---

# 4. Machine Code

Machine Code merupakan instruksi CPU.

Contoh Assembly:

```assembly
MOV EAX,1
ADD EAX,5
RET
```

Opcode disimpan dalam bentuk Hexadecimal.

---

# 5. Format Executable

## Windows

Portable Executable (PE)

Ekstensi:

- .exe
- .dll
- .sys

---

## Linux

Executable and Linkable Format (ELF)

Digunakan pada:

- Binary Linux
- Shared Object

---

## macOS

Mach-O

Digunakan oleh:

- macOS
- iOS

---

# 6. Struktur Portable Executable

```
+-------------------+
| DOS Header        |
+-------------------+
| PE Header         |
+-------------------+
| Optional Header   |
+-------------------+
| Section Table     |
+-------------------+
| .text             |
| .data             |
| .rdata            |
| .idata            |
| .rsrc             |
| .reloc            |
+-------------------+
```

---

# 7. Section

## .text

Machine Code

## .data

Global Variable

## .rdata

Read Only Data

## .idata

Import Table

## .edata

Export Table

## .rsrc

Resource

## .reloc

Relocation

---

# 8. Import Table

Executable menggunakan DLL.

Contoh:

```text
KERNEL32.dll

CreateFile()

CreateProcess()

WriteFile()
```

DLL lain:

- USER32.dll
- ADVAPI32.dll
- WS2_32.dll

---

# 9. Export Table

Digunakan pada DLL.

Berisi fungsi yang dapat dipanggil executable lain.

---

# 10. Packing

Packing digunakan untuk:

- Mengurangi ukuran file
- Menyembunyikan malware

Contoh:

- UPX
- MPRESS
- ASPack

---

# 11. Obfuscation

Teknik menyamarkan program.

Contoh:

- Rename Function
- Encrypt String
- Junk Code
- Control Flow Flattening

---

# 12. Tools

Static Analysis:

- Detect It Easy
- PEStudio
- PE-bear
- CFF Explorer
- Ghidra
- IDA Free

---

# Studi Kasus

Misalnya terdapat file malware.exe.

Langkah analisis:

1. Detect It Easy
2. PEStudio
3. PE-bear
4. Ghidra

Informasi yang dicari:

- Compiler
- Architecture
- Import Table
- Export Table
- Packer

---

# Praktikum

1. Install Detect It Easy.
2. Install PEStudio.
3. Install PE-bear.
4. Analisis Notepad.exe.
5. Screenshot seluruh hasil.

---

# Ringkasan

Mahasiswa memahami struktur executable dan mampu melakukan analisis awal terhadap file binary.

---

# Latihan

1. Apa itu Binary?
2. Apa itu Machine Code?
3. Jelaskan PE Header.
4. Apa fungsi Import Table?
5. Apa fungsi Section .text?
6. Apa itu UPX?
7. Apa perbedaan PE dan ELF?

---
---

# Refleksi Pembelajaran

## Apa yang Dipelajari

Pada minggu kedua saya mempelajari konsep binary dan executable sebagai objek utama dalam Reverse Engineering. Materi yang dipelajari meliputi pengertian binary, machine code, opcode, proses kompilasi source code menjadi executable, format executable pada berbagai sistem operasi seperti Portable Executable (PE), ELF, dan Mach-O, serta struktur internal Portable Executable yang terdiri atas DOS Header, PE Header, Optional Header, Section Table, dan berbagai section seperti .text, .data, .rdata, .idata, .rsrc, dan .reloc.

Selain itu, saya juga mempelajari fungsi Import Table dan Export Table, konsep Dynamic Link Library (DLL), teknik packing dan obfuscation yang sering digunakan untuk menyembunyikan malware, serta berbagai tools yang digunakan dalam analisis executable seperti Detect It Easy (DIE), PEStudio, PE-bear, CFF Explorer, Ghidra, dan IDA Free.

---

## Apa yang Saya Pahami

Setelah mempelajari materi minggu kedua, saya memahami bahwa file executable sebenarnya merupakan kumpulan instruksi machine code yang dapat dijalankan langsung oleh CPU. Saya memahami bahwa sebelum menjadi executable, sebuah program harus melalui proses preprocessing, compilation, assembling, dan linking.

Saya juga memahami bahwa setiap executable memiliki struktur tertentu yang memberikan informasi penting kepada sistem operasi ketika program dijalankan. Import Table membantu mengetahui library dan fungsi API yang digunakan suatu program, sedangkan section seperti .text menyimpan machine code dan .idata menyimpan daftar fungsi yang diimpor dari DLL.

Selain itu, saya memahami bahwa teknik packing dan obfuscation sering digunakan untuk menyulitkan proses analisis, terutama pada malware. Oleh karena itu, langkah pertama dalam Reverse Engineering adalah melakukan identifikasi terhadap executable menggunakan tools analisis statis.

---

## Apa yang Masih Membingungkan

Beberapa materi yang masih ingin saya pelajari lebih lanjut adalah bagaimana proses loader Windows memuat Portable Executable ke dalam memori serta bagaimana alamat virtual pada executable diterjemahkan menjadi alamat fisik ketika program dijalankan.

Saya juga masih ingin memahami lebih dalam mengenai cara kerja Import Address Table (IAT), Export Address Table (EAT), relocation, serta bagaimana packer seperti UPX melakukan proses unpacking di dalam memori. Selain itu, saya ingin lebih memahami bagaimana Ghidra dan IDA Pro menerjemahkan machine code menjadi assembly dan pseudo-code sehingga lebih mudah dianalisis.

