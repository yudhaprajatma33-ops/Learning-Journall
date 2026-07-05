# Reverse Engineering
## Week 6 - Reverse Engineering Hardware dan Firmware Analysis

---

# Capaian Pembelajaran

Setelah mengikuti perkuliahan pada minggu keenam, mahasiswa diharapkan mampu memahami konsep **Hardware Reverse Engineering**, mengenali komponen utama perangkat keras, memahami proses analisis firmware, mengenal berbagai antarmuka komunikasi (UART, SPI, I2C, dan JTAG), serta menggunakan tools untuk melakukan ekstraksi dan analisis firmware. Mahasiswa juga diharapkan mampu menjelaskan proses reverse engineering pada perangkat embedded dan Internet of Things (IoT).

---

# Pendahuluan

Reverse Engineering tidak hanya diterapkan pada perangkat lunak (software), tetapi juga pada perangkat keras (hardware). Dalam dunia keamanan siber, analisis perangkat keras menjadi semakin penting karena banyak perangkat modern, seperti router, kamera CCTV, smart TV, printer, dan perangkat Internet of Things (IoT), menggunakan firmware yang dapat menjadi target serangan.

Hardware Reverse Engineering merupakan proses memahami cara kerja suatu perangkat elektronik tanpa memiliki dokumentasi atau desain aslinya. Seorang analis akan mempelajari rangkaian elektronik, antarmuka komunikasi, firmware, hingga protokol yang digunakan oleh perangkat tersebut.

Firmware sendiri merupakan perangkat lunak tingkat rendah yang tersimpan di dalam memori non-volatile seperti EEPROM atau Flash Memory. Firmware mengendalikan fungsi dasar perangkat sehingga analisis firmware dapat membantu menemukan kerentanan keamanan, mekanisme autentikasi, maupun perilaku tersembunyi suatu perangkat.

Pada minggu ini mahasiswa akan mempelajari teknik dasar Reverse Engineering Hardware, mengenali komponen elektronik, memahami antarmuka komunikasi perangkat embedded, serta melakukan analisis firmware menggunakan berbagai tools open source.

---

# 1. Pengertian Hardware Reverse Engineering

Hardware Reverse Engineering adalah proses menganalisis perangkat keras untuk memahami desain, fungsi, dan cara kerjanya tanpa memiliki dokumentasi resmi dari pembuatnya.

Tujuan Hardware Reverse Engineering antara lain:

- Memahami arsitektur perangkat.
- Menemukan kerentanan keamanan.
- Menganalisis firmware.
- Memperbaiki perangkat yang rusak.
- Mengembangkan kompatibilitas perangkat.
- Melakukan penelitian keamanan perangkat IoT.

Contoh perangkat yang sering dianalisis:

- Router
- Smart TV
- Kamera CCTV
- Smart Lock
- Drone
- Smartwatch
- Printer
- Mikrokontroler

---

# 2. Embedded System

Embedded System adalah sistem komputer yang dirancang untuk menjalankan fungsi tertentu dalam suatu perangkat elektronik.

Komponen utama Embedded System:

- Mikrokontroler (MCU)
- Memori Flash
- RAM
- Sensor
- Aktuator
- Antarmuka Komunikasi

Contoh perangkat embedded:

- Mesin cuci otomatis
- ATM
- Mobil modern
- Kamera digital
- Router Wi-Fi
- Sistem alarm
- Smart Home

Embedded System umumnya menggunakan firmware sebagai sistem operasinya.

---

# 3. Komponen Hardware yang Sering Dianalisis

Dalam Hardware Reverse Engineering, beberapa komponen utama yang perlu dikenali adalah:

## Printed Circuit Board (PCB)

PCB merupakan papan sirkuit tempat seluruh komponen elektronik dipasang dan saling terhubung melalui jalur konduktor.

Fungsi PCB:

- Menghubungkan komponen elektronik.
- Menyediakan jalur listrik.
- Menjadi dasar pemasangan komponen.

---

## Integrated Circuit (IC)

IC merupakan komponen utama yang berfungsi sebagai pusat pemrosesan atau pengendali perangkat.

Jenis IC:

- Mikrokontroler
- Mikroprosesor
- EEPROM
- Flash Memory
- Power Management IC

---

## EEPROM

EEPROM adalah memori non-volatile yang dapat dihapus dan ditulis ulang secara elektronik.

Fungsi:

- Menyimpan konfigurasi perangkat.
- Menyimpan firmware sederhana.
- Menyimpan data kalibrasi.

---

## Flash Memory

Flash Memory digunakan untuk menyimpan firmware perangkat.

Jenis Flash:

- NAND Flash
- NOR Flash

Flash Memory dapat diekstraksi untuk dianalisis menggunakan software Reverse Engineering.

---

# 4. Firmware

Firmware adalah perangkat lunak yang tertanam pada perangkat keras dan bertanggung jawab mengendalikan fungsi dasar perangkat.

Firmware biasanya berisi:

- Bootloader
- Driver
- Sistem operasi embedded
- Konfigurasi perangkat
- Library

Reverse Engineering terhadap firmware dilakukan untuk:

- Menemukan password default.
- Menemukan backdoor.
- Menganalisis algoritma enkripsi.
- Menemukan kerentanan keamanan.

---

# 5. Firmware Extraction

Firmware dapat diperoleh melalui beberapa metode.

### Download dari Vendor

Beberapa produsen menyediakan firmware melalui situs resmi.

### Dump Flash Memory

Firmware diambil langsung dari chip Flash menggunakan programmer.

### UART Console

Mengakses firmware melalui terminal serial.

### JTAG Interface

Mengakses memori internal perangkat.

Firmware hasil ekstraksi biasanya memiliki ekstensi:

- .bin
- .img
- .rom
- .fw

---

# 6. Interface Komunikasi

Perangkat embedded memiliki beberapa antarmuka komunikasi yang sering digunakan dalam Reverse Engineering.

---

## UART (Universal Asynchronous Receiver Transmitter)

UART merupakan komunikasi serial sederhana.

Karakteristik:

- TX
- RX
- GND
- Baud Rate

Digunakan untuk:

- Debugging
- Console Login
- Firmware Recovery

Tools:

- USB to TTL
- PuTTY
- Tera Term

---

## SPI (Serial Peripheral Interface)

SPI merupakan komunikasi serial berkecepatan tinggi.

Pin:

- MOSI
- MISO
- CLK
- CS

Digunakan untuk:

- Flash Memory
- Sensor
- LCD

---

## I2C (Inter Integrated Circuit)

I2C menggunakan dua jalur komunikasi.

Pin:

- SDA
- SCL

Digunakan pada:

- Sensor
- RTC
- EEPROM
- LCD

---

## JTAG (Joint Test Action Group)

JTAG digunakan untuk debugging perangkat keras.

Fungsi:

- Membaca memori.
- Menulis memori.
- Debug firmware.
- Mengontrol CPU.

Tools:

- OpenOCD
- J-Link
- Bus Pirate

---

# 7. Tools Reverse Engineering Hardware

Beberapa tools yang sering digunakan:

| Tools | Fungsi |
|--------|---------|
| Binwalk | Ekstraksi Firmware |
| Firmware Mod Kit | Modifikasi Firmware |
| Ghidra | Analisis Binary |
| IDA Free | Reverse Engineering |
| OpenOCD | Debug JTAG |
| Flashrom | Membaca Flash Memory |
| Bus Pirate | Analisis Hardware |
| Logic Analyzer | Analisis Sinyal Digital |
| USB to TTL | UART Communication |

---

# 8. Binwalk

Binwalk merupakan tools open-source yang digunakan untuk menganalisis firmware.

Fungsi:

- Mendeteksi filesystem.
- Mengekstraksi firmware.
- Mencari file tersembunyi.
- Mengidentifikasi sistem operasi.

Contoh penggunaan:

```bash
binwalk firmware.bin
```

Ekstraksi firmware:

```bash
binwalk -e firmware.bin
```

---

# 9. Firmware Analysis

Setelah firmware berhasil diekstraksi, analis dapat melakukan beberapa analisis.

Langkah-langkah:

1. Ekstraksi firmware.
2. Identifikasi filesystem.
3. Analisis file konfigurasi.
4. Analisis password.
5. Analisis script startup.
6. Analisis binary.
7. Analisis web interface.
8. Identifikasi vulnerability.

---

# 10. Reverse Engineering IoT

Perangkat IoT menjadi target utama analisis keamanan karena sering terhubung ke internet.

Contoh perangkat:

- Smart Camera
- Smart Door Lock
- Smart Plug
- Smart TV
- Router
- Smart Speaker

Kerentanan umum:

- Password default.
- Firmware tidak terenkripsi.
- Backdoor.
- Komunikasi tidak aman.
- Update firmware tanpa verifikasi.

---

# 11. Studi Kasus

Misalkan seorang analis memperoleh sebuah router Wi-Fi yang diduga memiliki celah keamanan.

Langkah analisis:

1. Identifikasi model perangkat.
2. Cari firmware resmi dari vendor.
3. Ekstraksi firmware menggunakan Binwalk.
4. Analisis filesystem.
5. Cari file konfigurasi.
6. Analisis binary menggunakan Ghidra.
7. Cari akun administrator bawaan.
8. Identifikasi password default.
9. Dokumentasikan seluruh hasil analisis.

Melalui proses ini, analis dapat memahami cara kerja perangkat dan menemukan potensi kerentanan.

---

# Ringkasan

Pada minggu keenam mahasiswa mempelajari konsep Hardware Reverse Engineering dan Firmware Analysis. Materi mencakup pengenalan perangkat embedded, komponen hardware, firmware, teknik ekstraksi firmware, antarmuka komunikasi seperti UART, SPI, I2C, dan JTAG, serta penggunaan tools seperti Binwalk, Flashrom, OpenOCD, dan Ghidra. Mahasiswa juga mempraktikkan proses analisis firmware sebagai langkah awal dalam mengidentifikasi kerentanan pada perangkat embedded dan IoT.

---

# Refleksi Pembelajaran

## Apa yang Dipelajari

Pada minggu keenam saya mempelajari konsep Hardware Reverse Engineering dan Firmware Analysis. Saya mengenal komponen utama perangkat embedded seperti PCB, IC, EEPROM, dan Flash Memory, serta memahami cara memperoleh firmware dan menganalisis isinya menggunakan tools seperti Binwalk dan Ghidra. Selain itu, saya mempelajari antarmuka komunikasi UART, SPI, I2C, dan JTAG yang sering digunakan untuk mengakses perangkat keras.

---

## Apa yang Saya Pahami

Saya memahami bahwa keamanan suatu perangkat tidak hanya bergantung pada perangkat lunak, tetapi juga pada firmware dan desain perangkat kerasnya. Saya juga memahami proses dasar ekstraksi firmware, analisis struktur file, serta penggunaan Binwalk untuk mengidentifikasi filesystem di dalam firmware. Pengetahuan tentang antarmuka komunikasi membantu saya memahami bagaimana seorang analis dapat berinteraksi langsung dengan perangkat embedded.

---

## Apa yang Masih Membingungkan

Saya masih ingin mempelajari lebih dalam mengenai teknik membaca firmware langsung dari chip menggunakan programmer, penggunaan JTAG untuk debugging tingkat lanjut, serta proses modifikasi firmware dan pemasangannya kembali ke perangkat. Selain itu, saya ingin memahami teknik bypass secure boot dan mekanisme proteksi firmware yang digunakan pada perangkat modern.

---
trol Systems (ICS) Security*.
