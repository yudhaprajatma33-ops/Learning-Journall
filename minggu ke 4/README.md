# Reverse Engineering
## Week 4 - Virtual Machine dan Dynamic Analysis Environment

---

# Capaian Pembelajaran

Setelah mengikuti perkuliahan pada minggu keempat, mahasiswa diharapkan mampu memahami pentingnya penggunaan Virtual Machine (VM) sebagai lingkungan analisis yang aman, membangun laboratorium (lab) Reverse Engineering, memahami konsep sandboxing, snapshot, cloning, serta menginstal dan mengonfigurasi berbagai tools yang digunakan dalam analisis malware. Mahasiswa juga diharapkan mampu menyiapkan lingkungan kerja yang aman sebelum melakukan proses Dynamic Analysis pada minggu berikutnya.

---

# Pendahuluan

Dalam Reverse Engineering, khususnya pada analisis malware, menjalankan file executable secara langsung pada sistem operasi utama (host) merupakan tindakan yang sangat berisiko. Malware dapat mencuri data, mengenkripsi file, merusak sistem operasi, bahkan menyebar melalui jaringan komputer. Oleh karena itu, seorang reverse engineer harus memiliki lingkungan analisis yang aman (Analysis Environment) sebelum melakukan pengujian terhadap suatu program.

Salah satu solusi yang paling umum digunakan adalah Virtual Machine (VM). Virtual Machine memungkinkan pengguna menjalankan sistem operasi lain di dalam komputer tanpa memengaruhi sistem operasi utama. Dengan VM, seorang analis dapat menguji malware, melakukan debugging, memonitor aktivitas program, serta mengembalikan kondisi sistem ke keadaan semula menggunakan fitur snapshot apabila terjadi kerusakan.

Lingkungan analisis yang baik tidak hanya terdiri atas Virtual Machine, tetapi juga mencakup konfigurasi jaringan, tools monitoring, debugger, serta sistem operasi yang telah disiapkan khusus untuk kebutuhan Reverse Engineering. Pada minggu ini mahasiswa akan mempelajari cara membangun laboratorium analisis malware yang aman dan profesional.

---

# 1. Pengertian Virtual Machine

Virtual Machine (VM) adalah sebuah komputer virtual yang berjalan di atas komputer fisik menggunakan perangkat lunak yang disebut **Hypervisor**. VM memiliki sistem operasi, memori, penyimpanan, serta perangkat keras virtual yang bekerja secara terpisah dari sistem operasi utama (Host).

Dengan menggunakan VM, pengguna dapat menjalankan beberapa sistem operasi secara bersamaan dalam satu komputer tanpa harus melakukan dual boot. Misalnya, pengguna dapat menjalankan Windows 11 sebagai Host dan Windows 10 atau Linux sebagai Guest Operating System.

Dalam Reverse Engineering, VM berfungsi sebagai lingkungan yang aman untuk menganalisis malware karena segala aktivitas yang terjadi di dalam VM tidak langsung memengaruhi sistem operasi host.

---

# 2. Jenis Hypervisor

Hypervisor merupakan perangkat lunak yang bertugas membuat dan mengelola Virtual Machine.

Terdapat dua jenis Hypervisor.

## Type 1 Hypervisor (Bare Metal)

Hypervisor berjalan langsung di atas perangkat keras tanpa sistem operasi.

Contoh:

- VMware ESXi
- Microsoft Hyper-V Server
- Xen Server
- Proxmox VE

Kelebihan:

- Performa tinggi.
- Stabil.
- Banyak digunakan pada server.

---

## Type 2 Hypervisor

Hypervisor berjalan di atas sistem operasi.

Contoh:

- Oracle VirtualBox
- VMware Workstation
- VMware Player
- Parallels Desktop

Kelebihan:

- Mudah digunakan.
- Cocok untuk pembelajaran.
- Instalasi sederhana.

---

# 3. Oracle VirtualBox

Oracle VirtualBox merupakan salah satu hypervisor yang paling banyak digunakan dalam pembelajaran Reverse Engineering karena bersifat gratis (open source) dan mendukung berbagai sistem operasi.

Fitur utama VirtualBox meliputi:

- Snapshot
- Clone VM
- Shared Folder
- USB Passthrough
- Network Adapter
- Guest Additions

Keuntungan menggunakan VirtualBox antara lain mudah dikonfigurasi, ringan, dan kompatibel dengan Windows, Linux, serta macOS.

---

# 4. VMware Workstation

VMware Workstation merupakan hypervisor komersial yang memiliki performa tinggi dan banyak digunakan oleh profesional keamanan siber.

Keunggulan VMware antara lain:

- Performa lebih baik.
- Snapshot lebih cepat.
- Dukungan debugging kernel.
- Kompatibilitas tinggi.
- Integrasi jaringan lebih lengkap.

VMware sering digunakan dalam laboratorium analisis malware profesional karena stabilitasnya.

---

# 5. Snapshot

Snapshot adalah fitur yang memungkinkan pengguna menyimpan kondisi Virtual Machine pada waktu tertentu.

Diagram Snapshot:

```text
Install Windows

↓

Install Tools

↓

Create Snapshot

↓

Analisis Malware

↓

Virus Menginfeksi VM

↓

Restore Snapshot

↓

VM Kembali Bersih
```

Manfaat Snapshot:

- Menghemat waktu instalasi ulang.
- Mengembalikan kondisi VM.
- Aman untuk analisis malware.
- Memudahkan eksperimen.

---

# 6. Clone Virtual Machine

Clone adalah proses menggandakan sebuah Virtual Machine.

Jenis Clone:

### Full Clone

- Seluruh file VM disalin.
- Berdiri sendiri.
- Membutuhkan ruang penyimpanan lebih besar.

### Linked Clone

- Berbagi file dengan VM utama.
- Lebih hemat ruang.
- Bergantung pada VM induk.

Clone memudahkan pembuatan beberapa lingkungan analisis dengan konfigurasi yang sama.

---

# 7. Konfigurasi Jaringan pada Virtual Machine

Konfigurasi jaringan sangat penting agar malware tidak menyebar ke jaringan utama.

Jenis Network Adapter:

## NAT (Network Address Translation)

VM dapat mengakses internet tetapi sulit diakses dari luar.

Cocok untuk:

- Download tools
- Update Windows
- Instal software

---

## Bridged Adapter

VM terhubung langsung ke jaringan fisik.

Kelebihan:

- IP sendiri.
- Dapat berkomunikasi dengan komputer lain.

Kekurangan:

- Berbahaya untuk malware.

---

## Host-Only Adapter

VM hanya dapat berkomunikasi dengan Host.

Sangat direkomendasikan untuk malware analysis.

---

## Internal Network

VM hanya dapat berkomunikasi dengan VM lain.

Digunakan pada laboratorium malware.

---

# 8. Sandbox

Sandbox merupakan lingkungan yang terisolasi untuk menjalankan aplikasi secara aman.

Contoh Sandbox:

- Windows Sandbox
- Any.Run
- Cuckoo Sandbox
- Hybrid Analysis

Keuntungan Sandbox:

- Aman.
- Cepat.
- Otomatis.
- Memantau perilaku malware.

---

# 9. Flare VM

Flare VM adalah distribusi Windows yang dikembangkan oleh Mandiant untuk kebutuhan Reverse Engineering dan Malware Analysis.

Berisi tools seperti:

- Ghidra
- x64dbg
- Wireshark
- PEStudio
- Detect It Easy
- Cutter
- Procmon
- Autoruns
- TCPView

Flare VM sangat direkomendasikan untuk membangun laboratorium Reverse Engineering.

---

# 10. REMnux

REMnux merupakan distribusi Linux yang dirancang khusus untuk Malware Analysis.

Fitur:

- Binwalk
- Radare2
- YARA
- Volatility
- INetSim
- FakeDNS
- FakeNet

REMnux digunakan untuk menganalisis malware berbasis Linux maupun firmware.

---

# 11. Tools Monitoring

Sebelum malware dijalankan, analis harus menyiapkan berbagai tools monitoring.

## Process Hacker

Digunakan untuk:

- Melihat Process
- Thread
- DLL
- Memory

---

## Process Monitor (Procmon)

Memonitor:

- Registry
- File System
- Process
- Thread

---

## Autoruns

Menampilkan:

- Startup Program
- Service
- Scheduled Task

---

## TCPView

Menampilkan:

- Port
- Connection
- IP Address

---

## Wireshark

Digunakan untuk:

- Capture Packet
- Analisis Jaringan
- Monitoring Traffic

---

# 12. Struktur Laboratorium Reverse Engineering

Contoh laboratorium:

```text
Host Computer

│

├── VirtualBox

│      │

│      ├── Windows 10 VM

│      │      ├── Ghidra

│      │      ├── x64dbg

│      │      ├── Procmon

│      │      ├── Wireshark

│      │      └── Process Hacker

│      │

│      └── REMnux VM

│             ├── Binwalk

│             ├── Radare2

│             ├── YARA

│             └── Volatility

│

└── Host Only Network
```

---

# Studi Kasus

Seorang analis memperoleh file **sample.exe** yang diduga merupakan ransomware. Sebelum menjalankan file tersebut, analis membuat sebuah Virtual Machine Windows 10 menggunakan Oracle VirtualBox. Setelah instalasi selesai, analis memasang tools seperti Process Hacker, Procmon, Wireshark, Detect It Easy, PEStudio, Ghidra, dan x64dbg.

Analis kemudian membuat snapshot dengan nama **Clean Installation**. VM dikonfigurasi menggunakan Host-Only Network agar malware tidak dapat mengakses jaringan luar. Selanjutnya, Process Monitor dan Wireshark dijalankan untuk memantau aktivitas file, registry, dan jaringan. Setelah malware selesai dianalisis, VM dikembalikan ke kondisi awal menggunakan snapshot sehingga tidak diperlukan instalasi ulang.

---

# Ringkasan

Pada minggu keempat mahasiswa mempelajari cara membangun lingkungan analisis yang aman menggunakan Virtual Machine. Materi meliputi konsep Hypervisor, VirtualBox, VMware, Snapshot, Clone, konfigurasi jaringan, Sandbox, Flare VM, REMnux, serta berbagai tools monitoring seperti Process Hacker, Procmon, Wireshark, Autoruns, dan TCPView. Pemahaman mengenai lingkungan analisis ini menjadi dasar sebelum melakukan Dynamic Analysis terhadap malware pada minggu berikutnya.

---

# Refleksi Pembelajaran

## Apa yang Dipelajari

Pada minggu keempat saya mempelajari cara membangun lingkungan analisis yang aman menggunakan Virtual Machine. Saya memahami konsep Hypervisor, Snapshot, Clone, konfigurasi jaringan, Sandbox, serta penggunaan Flare VM dan REMnux sebagai sistem operasi yang telah dipersiapkan untuk kebutuhan Reverse Engineering. Selain itu, saya juga mempelajari penggunaan tools monitoring seperti Process Hacker, Procmon, Wireshark, TCPView, dan Autoruns.

---

## Apa yang Saya Pahami

Saya memahami bahwa penggunaan Virtual Machine merupakan langkah penting dalam Reverse Engineering karena dapat melindungi sistem operasi utama dari ancaman malware. Saya juga memahami manfaat Snapshot untuk mengembalikan kondisi sistem setelah proses analisis, serta pentingnya konfigurasi jaringan Host-Only agar malware tidak menyebar ke jaringan lain. Selain itu, saya mulai memahami fungsi berbagai tools monitoring dalam mengamati aktivitas file, registry, proses, dan lalu lintas jaringan.

---

## Apa yang Masih Membingungkan

Saya masih ingin mempelajari lebih dalam mengenai konfigurasi jaringan virtual yang lebih kompleks, seperti penggunaan Internal Network dan simulasi jaringan malware menggunakan FakeNet atau INetSim. Selain itu, saya juga ingin memahami teknik deteksi Virtual Machine oleh malware (VM Detection) dan bagaimana cara mengatasinya agar hasil analisis lebih akurat.

---
6. Oracle. *Oracle VM VirtualBox User Manual*.
7. VMware. *VMware Workstation Pro Documentation*.
8. Microsoft. *Windows Sandbox Documentation*.
