# 🐧 Linux Debian — Command Fundamentals

<div align="center">

![Debian](https://img.shields.io/badge/Debian-Linux-A81D33?style=for-the-badge&logo=debian&logoColor=white)
![Shell](https://img.shields.io/badge/Shell-Bash-4EAA25?style=for-the-badge&logo=gnubash&logoColor=white)
![Level](https://img.shields.io/badge/Level-Beginner%20→%20Intermediate-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Active-brightgreen?style=for-the-badge)

<br/>

> *"The command line is the single most important tool for a Linux user — master it, and the system is yours."*

<br/>

Panduan lengkap perintah-perintah dasar hingga menengah pada sistem operasi **Debian Linux**, disusun secara terstruktur untuk membangun fondasi yang kuat dalam penggunaan terminal.

</div>

---

## 📋 Table of Contents

- [Pengenalan Debian Linux](#-pengenalan-debian-linux)
- [Struktur Filesystem Linux](#-struktur-filesystem-linux)
- [Navigasi Direktori](#-navigasi-direktori)
- [Manajemen File & Direktori](#-manajemen-file--direktori)
- [Melihat & Mengedit File](#-melihat--mengedit-file)
- [User & Group Management](#-user--group-management)
- [Permission & Ownership](#-permission--ownership)
- [Process Management](#-process-management)
- [Package Management (APT)](#-package-management-apt)
- [Networking Commands](#-networking-commands)
- [Disk & Storage Management](#-disk--storage-management)
- [System Information & Monitoring](#-system-information--monitoring)
- [Archiving & Compression](#-archiving--compression)
- [Searching & Filtering](#-searching--filtering)
- [Shell & Environment](#-shell--environment)
- [Systemd & Service Management](#-systemd--service-management)
- [Firewall (UFW & iptables)](#-firewall-ufw--iptables)
- [SSH & Remote Access](#-ssh--remote-access)
- [Shell Scripting Basics](#-shell-scripting-basics)
- [Useful Shortcuts & Tips](#-useful-shortcuts--tips)

---

## 🔍 Pengenalan Debian Linux

**Debian** adalah salah satu distribusi Linux tertua dan paling stabil, pertama kali dirilis tahun 1993 oleh Ian Murdock. Debian menjadi basis dari banyak distro populer seperti Ubuntu, Kali Linux, dan Parrot OS.

**Keunggulan Debian:**
- Sangat stabil dan andal (ideal untuk server)
- Repositori paket terbesar (~59.000+ paket)
- Manajemen paket APT yang powerful
- Dukungan komunitas yang luas dan dokumentasi lengkap
- Cocok untuk server production, desktop, dan embedded systems

**Versi Debian:**

| Codename | Status | Keterangan |
|----------|--------|------------|
| Bookworm (12) | Stable | Rilis stabil terkini |
| Bullseye (11) | Oldstable | Masih didukung |
| Trixie (13) | Testing | Akan menjadi stable berikutnya |
| Sid | Unstable | Rolling release, untuk developer |

---

## 📁 Struktur Filesystem Linux

```
/  (root — akar dari seluruh filesystem)
│
├── bin/        → Perintah esensial (ls, cp, mv, cat)
├── boot/       → File bootloader (GRUB, kernel)
├── dev/        → File perangkat keras (disk, USB, terminal)
├── etc/        → Konfigurasi sistem (hosts, fstab, apt)
│   ├── apt/        → Konfigurasi APT package manager
│   ├── network/    → Konfigurasi jaringan
│   └── ssh/        → Konfigurasi SSH server/client
├── home/       → Direktori home tiap user (/home/username)
├── lib/        → Library sistem yang dibutuhkan binary
├── media/      → Mount otomatis perangkat removable
├── mnt/        → Mount manual sementara
├── opt/        → Aplikasi pihak ketiga opsional
├── proc/       → Filesystem virtual (info proses & kernel)
├── root/       → Home direktori user root
├── run/        → Data runtime sejak boot terakhir
├── sbin/       → Binary administrasi sistem
├── srv/        → Data untuk layanan (web, ftp)
├── sys/        → Filesystem virtual info hardware
├── tmp/        → File sementara (terhapus saat reboot)
├── usr/        → Program & data pengguna
│   ├── bin/        → Binary pengguna (python3, vim, git)
│   ├── lib/        → Library untuk program di usr/bin
│   ├── local/      → Program yang dikompilasi secara lokal
│   └── share/      → Data statis (dokumentasi, icons)
└── var/        → Data variabel (log, database, cache)
    ├── log/        → File log sistem
    ├── www/        → Direktori web server default
    └── cache/      → Cache aplikasi
```

---

## 🧭 Navigasi Direktori

```bash
# Menampilkan direktori saat ini
pwd
# Output: /home/user

# Berpindah direktori
cd /var/log            # Pindah ke path absolut
cd Documents           # Pindah ke subdirektori relatif
cd ..                  # Naik satu level
cd ../..               # Naik dua level
cd ~                   # Kembali ke home directory
cd -                   # Kembali ke direktori sebelumnya

# Menampilkan isi direktori
ls                     # Daftar file & folder
ls -l                  # Format panjang (detail)
ls -a                  # Tampilkan file tersembunyi (dot files)
ls -la                 # Gabungan: detail + tersembunyi
ls -lh                 # Ukuran file dalam format human-readable
ls -lt                 # Urutkan berdasarkan waktu modifikasi
ls -lR                 # Rekursif (tampilkan semua subdirektori)
ls /etc                # Tampilkan isi direktori tertentu

# Melihat struktur direktori (tree)
tree                   # Tampilkan tree direktori saat ini
tree -L 2              # Batasi kedalaman 2 level
tree -a                # Tampilkan file tersembunyi
# Install: apt install tree
```

---

## 📂 Manajemen File & Direktori

### Membuat File & Direktori

```bash
# Membuat file kosong
touch namafile.txt
touch file1.txt file2.txt file3.txt    # Buat banyak file sekaligus

# Membuat direktori
mkdir namadirektori
mkdir -p /path/to/nested/dir           # Buat nested directory sekaligus
mkdir -m 755 namadirektori             # Buat dengan permission tertentu

# Membuat file dengan konten langsung
echo "Hello, Debian!" > file.txt       # Tulis/timpa isi file
echo "Tambahan baris" >> file.txt      # Tambahkan ke akhir file
cat > file.txt << EOF
Baris pertama
Baris kedua
Baris ketiga
EOF
```

### Menyalin, Memindahkan, Mengganti Nama

```bash
# Menyalin (copy)
cp source.txt destination.txt          # Salin file
cp -r source_dir/ destination_dir/    # Salin direktori (rekursif)
cp -i file.txt /path/                  # Konfirmasi jika ada overwrite
cp -v file.txt /path/                  # Verbose (tampilkan proses)
cp -p file.txt /backup/                # Pertahankan atribut (timestamp, permission)
cp -u source dest                      # Salin hanya jika source lebih baru

# Memindahkan / Mengganti Nama (move)
mv namalama.txt namabaru.txt           # Ganti nama file
mv file.txt /path/to/destination/      # Pindah file
mv -i source dest                      # Konfirmasi overwrite
mv -v source dest                      # Verbose

# Menghapus (remove)
rm namafile.txt                        # Hapus file
rm -i namafile.txt                     # Konfirmasi sebelum hapus
rm -f namafile.txt                     # Force hapus tanpa konfirmasi
rm -r namadirektori/                   # Hapus direktori beserta isinya
rm -rf namadirektori/                  # Force hapus direktori (hati-hati!)
rmdir namadirektori/                   # Hapus direktori kosong saja

# Membuat symlink (symbolic link)
ln -s /path/to/original /path/to/link # Buat symlink
ln /path/to/original /path/to/link    # Buat hard link
```

---

## 📄 Melihat & Mengedit File

### Menampilkan Isi File

```bash
# Tampilkan seluruh isi file
cat namafile.txt
cat -n namafile.txt                    # Dengan nomor baris
cat -A namafile.txt                    # Tampilkan karakter khusus

# Paginasi (untuk file panjang)
less namafile.txt                      # Navigasi: ↑↓, q untuk keluar
more namafile.txt                      # Sederhana, hanya scroll ke bawah

# Tampilkan sebagian file
head namafile.txt                      # 10 baris pertama (default)
head -n 20 namafile.txt                # 20 baris pertama
tail namafile.txt                      # 10 baris terakhir
tail -n 20 namafile.txt                # 20 baris terakhir
tail -f /var/log/syslog                # Pantau log secara real-time

# Tampilkan info file
file namafile.txt                      # Identifikasi tipe file
wc namafile.txt                        # Hitung baris, kata, karakter
wc -l namafile.txt                     # Hitung baris saja
wc -w namafile.txt                     # Hitung kata saja
stat namafile.txt                      # Informasi lengkap file (metadata)

# Membandingkan file
diff file1.txt file2.txt               # Tampilkan perbedaan
diff -u file1.txt file2.txt            # Format unified (lebih readable)
```

### Mengedit File (Text Editors)

```bash
# nano — editor sederhana, cocok untuk pemula
nano namafile.txt
# Shortcut nano:
#   Ctrl+O  → Simpan
#   Ctrl+X  → Keluar
#   Ctrl+K  → Cut baris
#   Ctrl+U  → Paste
#   Ctrl+W  → Cari teks

# vim — editor powerful untuk advanced user
vim namafile.txt
# Mode vim:
#   i       → Insert mode (mulai mengetik)
#   Esc     → Kembali ke Normal mode
#   :w      → Simpan
#   :q      → Keluar
#   :wq     → Simpan dan keluar
#   :q!     → Keluar tanpa menyimpan
#   /kata   → Cari teks

# Mengedit file dengan sed (stream editor)
sed -i 's/kata_lama/kata_baru/g' file.txt   # Replace teks
sed -n '5,10p' file.txt                      # Tampilkan baris 5-10
sed '/^#/d' file.txt                         # Hapus baris komentar
```

---

## 👥 User & Group Management

```bash
# ── INFORMASI USER ──────────────────────────────────────────
whoami                          # Tampilkan user yang sedang login
id                              # UID, GID, dan group membership
id username                     # Info user tertentu
who                             # Siapa saja yang sedang login
w                               # Login aktif + aktivitas
last                            # Riwayat login
finger username                 # Info detail user (jika terinstall)
cat /etc/passwd                 # Daftar semua user sistem

# ── MEMBUAT & MENGELOLA USER ────────────────────────────────
sudo adduser namauser           # Buat user baru (interactive, direkomendasikan)
sudo useradd namauser           # Buat user (non-interactive, manual setup)
sudo useradd -m -s /bin/bash -G sudo namauser  # Buat user dengan home dir + shell + group

sudo passwd namauser            # Set atau ubah password user
sudo passwd -l namauser         # Lock (nonaktifkan) akun user
sudo passwd -u namauser         # Unlock akun user
sudo passwd -e namauser         # Paksa ganti password saat login berikutnya

sudo usermod -aG sudo namauser  # Tambah user ke group sudo
sudo usermod -aG group1,group2 user  # Tambah ke beberapa group
sudo usermod -s /bin/zsh user   # Ubah default shell user
sudo usermod -l newname oldname # Ubah username
sudo usermod -d /new/home user  # Ubah home directory

sudo deluser namauser           # Hapus user (pertahankan home dir)
sudo deluser --remove-home namauser  # Hapus user beserta home dir
sudo userdel -r namauser        # Hapus user + home dir (alternatif)

# ── MANAJEMEN GROUP ─────────────────────────────────────────
cat /etc/group                  # Daftar semua group
groups namauser                 # Tampilkan group user tertentu
sudo groupadd namagroup         # Buat group baru
sudo groupdel namagroup         # Hapus group
sudo gpasswd -d user group      # Keluarkan user dari group

# ── SWITCH USER ─────────────────────────────────────────────
su - namauser                   # Login sebagai user lain
sudo su -                       # Login sebagai root
sudo -i                         # Buka shell interaktif root
sudo command                    # Jalankan perintah sebagai root
sudo -u namauser command        # Jalankan perintah sebagai user tertentu
exit / logout                   # Keluar dari sesi user
```

---

## 🔐 Permission & Ownership

### Memahami Permission Linux

```
Contoh output: -rwxr-xr--  1  user  group  4096  Jan 01  file.txt

Karakter 1   : Tipe (-=file, d=direktori, l=symlink, b=block, c=char)
Karakter 2-4 : Permission Owner  (rwx = read+write+execute)
Karakter 5-7 : Permission Group  (r-x = read+execute)
Karakter 8-10: Permission Others (r-- = read only)

Nilai Oktal:
  r (read)    = 4
  w (write)   = 2
  x (execute) = 1
  - (none)    = 0

Contoh kombinasi:
  7 = rwx (4+2+1) → Full permission
  6 = rw- (4+2+0) → Read & Write
  5 = r-x (4+0+1) → Read & Execute
  4 = r-- (4+0+0) → Read only
  0 = --- (0+0+0) → No permission
```

### Mengubah Permission (chmod)

```bash
# Metode Oktal (Numerik)
chmod 755 namafile      # rwxr-xr-x  (owner=7, group=5, others=5)
chmod 644 namafile      # rw-r--r--  (file biasa)
chmod 600 namafile      # rw-------  (private file)
chmod 777 namafile      # rwxrwxrwx  (semua akses — hindari!)
chmod 400 namafile      # r--------  (read-only, hanya owner)
chmod -R 755 direktori/ # Terapkan rekursif ke seluruh isi direktori

# Metode Simbolik
chmod u+x namafile      # Tambah execute untuk owner (user)
chmod g-w namafile      # Hapus write untuk group
chmod o+r namafile      # Tambah read untuk others
chmod a+x namafile      # Tambah execute untuk semua (all)
chmod u=rwx,g=rx,o=r namafile  # Set eksplisit

# Permission Khusus
chmod +t direktori/     # Sticky bit (hanya owner bisa hapus file-nya)
chmod u+s namafile      # SUID (file executable berjalan sebagai owner)
chmod g+s direktori/    # SGID (file baru mewarisi group direktori)
chmod 1755 direktori/   # Sticky bit dengan notasi oktal
```

### Mengubah Kepemilikan (chown & chgrp)

```bash
# Mengubah owner
chown namauser namafile                 # Ubah owner file
chown namauser:namagroup namafile       # Ubah owner dan group sekaligus
chown -R namauser:namagroup direktori/  # Rekursif untuk direktori
chown :namagroup namafile               # Ubah hanya group

# Mengubah group saja
chgrp namagroup namafile
chgrp -R namagroup direktori/

# Melihat permission secara detail
ls -la                  # Tampilkan permission semua file
stat namafile           # Info lengkap termasuk permission oktal
getfacl namafile        # Tampilkan ACL (Access Control List)
setfacl -m u:user:rwx file  # Set ACL untuk user tertentu
```

---

## ⚙️ Process Management

```bash
# ── MELIHAT PROSES ──────────────────────────────────────────
ps                              # Proses milik terminal saat ini
ps aux                          # Semua proses semua user (format BSD)
ps -ef                          # Semua proses (format UNIX)
ps -ef | grep nginx             # Cari proses tertentu
ps -u namauser                  # Proses milik user tertentu
pstree                          # Tampilkan proses dalam bentuk pohon
top                             # Monitor proses real-time (interaktif)
htop                            # Monitor proses versi enhanced
                                # (apt install htop)

# ── INFORMASI PROSES ────────────────────────────────────────
# Di dalam top/htop:
#   q → Keluar
#   k → Kill proses (masukkan PID)
#   r → Renice (ubah prioritas)
#   P → Urutkan CPU
#   M → Urutkan Memory
#   / → Cari proses

# ── SINYAL & KONTROL PROSES ─────────────────────────────────
kill PID                        # Kirim SIGTERM (15) — minta berhenti
kill -9 PID                     # Kirim SIGKILL (9) — paksa berhenti
kill -15 PID                    # SIGTERM (default)
kill -HUP PID                   # SIGHUP (1) — reload konfigurasi
killall nama_proses             # Kill semua proses dengan nama tsb
pkill -f "nama_proses"          # Kill proses berdasarkan pattern
pkill -u namauser               # Kill semua proses user tertentu

# ── BACKGROUND & FOREGROUND ─────────────────────────────────
perintah &                      # Jalankan di background
jobs                            # Tampilkan daftar job background
fg                              # Bawa job terakhir ke foreground
fg %1                           # Bawa job nomor 1 ke foreground
bg %1                           # Kirim job nomor 1 ke background
Ctrl+Z                          # Suspend job (pause)
Ctrl+C                          # Hentikan job yang sedang berjalan

# ── MENJALANKAN PROSES PERMANEN ─────────────────────────────
nohup perintah &                # Jalankan meski terminal ditutup
nohup perintah > output.log &   # + redirect output ke file
screen                          # Terminal multiplexer (apt install screen)
tmux                            # Terminal multiplexer modern (apt install tmux)

# ── PRIORITAS PROSES ────────────────────────────────────────
nice -n 10 perintah             # Jalankan dengan prioritas rendah (10)
nice -n -5 perintah             # Prioritas lebih tinggi (butuh sudo)
renice 10 -p PID                # Ubah prioritas proses yang berjalan
```

---

## 📦 Package Management (APT)

APT (Advanced Package Tool) adalah sistem manajemen paket resmi Debian dan turunannya.

```bash
# ── UPDATE & UPGRADE ────────────────────────────────────────
sudo apt update                     # Update daftar paket dari repositori
sudo apt upgrade                    # Upgrade semua paket yang ada update
sudo apt full-upgrade               # Upgrade + tangani dependency yang berubah
sudo apt dist-upgrade               # Upgrade ke versi distro baru
sudo apt-get update && sudo apt-get upgrade -y  # Update otomatis (non-interactive)

# ── INSTALASI ───────────────────────────────────────────────
sudo apt install namapaket          # Install paket
sudo apt install paket1 paket2      # Install beberapa paket sekaligus
sudo apt install -y namapaket       # Auto-yes (tanpa konfirmasi)
sudo apt install --no-install-recommends namapaket  # Tanpa paket rekomendasi
sudo apt install ./namapaket.deb    # Install dari file .deb lokal
sudo dpkg -i namapaket.deb          # Install .deb dengan dpkg langsung
sudo apt install -f                 # Perbaiki dependency yang rusak

# ── MENGHAPUS PAKET ─────────────────────────────────────────
sudo apt remove namapaket           # Hapus paket (simpan konfigurasi)
sudo apt purge namapaket            # Hapus paket + file konfigurasi
sudo apt autoremove                 # Hapus dependency yang tidak dipakai
sudo apt autoclean                  # Hapus cache paket yang kadaluarsa
sudo apt clean                      # Hapus seluruh cache paket lokal

# ── MENCARI & INFO PAKET ────────────────────────────────────
apt search namapaket                # Cari paket di repositori
apt show namapaket                  # Tampilkan info detail paket
apt list --installed                # Daftar semua paket terinstall
apt list --upgradable               # Daftar paket yang bisa diupgrade
dpkg -l                             # Daftar paket terinstall (dpkg)
dpkg -l | grep namapaket            # Cek apakah paket terinstall
dpkg -L namapaket                   # Daftar file yang diinstall oleh paket
dpkg -S /path/to/file               # Cari paket yang memiliki file tertentu
which namaprogram                   # Lokasi binary program

# ── REPOSITORI ──────────────────────────────────────────────
cat /etc/apt/sources.list           # Lihat daftar repositori
ls /etc/apt/sources.list.d/         # Repositori tambahan
sudo add-apt-repository ppa:nama/ppa  # Tambah PPA (Ubuntu)
sudo apt-key adv --keyserver ...    # Tambah GPG key repositori
```

---

## 🌐 Networking Commands

```bash
# ── INFORMASI JARINGAN ──────────────────────────────────────
ip addr                         # Tampilkan semua interface dan IP
ip addr show eth0               # Info interface eth0 saja
ifconfig                        # Cara lama (apt install net-tools)
ip link show                    # Tampilkan status interface
ip route                        # Tampilkan routing table
ip route show default           # Gateway default
hostname                        # Tampilkan hostname
hostname -I                     # Tampilkan semua IP address
cat /etc/hosts                  # File hosts lokal
cat /etc/resolv.conf            # Konfigurasi DNS
cat /etc/network/interfaces     # Konfigurasi jaringan (Debian classic)

# ── KONEKTIVITAS & DIAGNOSTIK ───────────────────────────────
ping google.com                 # Test konektivitas (terus-menerus)
ping -c 4 google.com            # Kirim 4 paket ICMP
ping -i 2 google.com            # Interval 2 detik antar paket
traceroute google.com           # Trace rute jaringan (apt install traceroute)
tracepath google.com            # Alternatif tanpa root
mtr google.com                  # Kombinasi ping + traceroute (apt install mtr)

# ── DNS LOOKUP ──────────────────────────────────────────────
nslookup domain.com             # Query DNS sederhana
dig domain.com                  # Query DNS detail
dig domain.com MX               # Cari record MX (mail server)
dig +short domain.com           # Output singkat IP saja
host domain.com                 # Resolusi DNS cepat
whois domain.com                # Info registrasi domain

# ── PORT & KONEKSI ──────────────────────────────────────────
ss -tulnp                       # Port yang terbuka + proses (modern)
netstat -tulnp                  # Port yang terbuka (legacy, apt install net-tools)
ss -s                           # Statistik socket
lsof -i :80                     # Proses yang menggunakan port 80
lsof -i TCP                     # Semua koneksi TCP
nmap localhost                  # Scan port lokal (apt install nmap)
nmap -p 22,80,443 target_ip     # Scan port tertentu

# ── TRANSFER FILE ───────────────────────────────────────────
wget https://url/file           # Download file
wget -O output.zip https://url  # Download dengan nama file tertentu
wget -c https://url             # Lanjutkan download yang terputus
wget -r https://website         # Download website rekursif
curl https://url                # HTTP request / download
curl -O https://url/file        # Download ke nama file asli
curl -L https://url             # Ikuti redirect
curl -u user:pass https://url   # HTTP basic auth
curl -X POST -d "data" https://url  # HTTP POST request

# SCP (Secure Copy via SSH)
scp file.txt user@host:/path/             # Upload file ke remote
scp user@host:/path/file.txt ./           # Download dari remote
scp -r direktori/ user@host:/path/        # Upload direktori
scp -P 2222 file.txt user@host:/path/     # Port SSH berbeda

# rsync (sinkronisasi file efisien)
rsync -avz source/ dest/                  # Sync lokal
rsync -avz -e ssh source/ user@host:dest/ # Sync ke remote via SSH
rsync -avz --delete source/ dest/         # Sync + hapus yang tidak ada di source
rsync --progress source dest              # Tampilkan progress
```

---

## 💾 Disk & Storage Management

```bash
# ── PENGGUNAAN DISK ─────────────────────────────────────────
df -h                           # Penggunaan disk semua filesystem (human-readable)
df -hT                          # + tampilkan tipe filesystem
du -sh /path/                   # Ukuran total direktori
du -sh *                        # Ukuran setiap item di direktori saat ini
du -sh /* | sort -rh | head -10 # 10 direktori terbesar di /
ncdu /                          # Disk usage interaktif (apt install ncdu)

# ── INFORMASI DISK ──────────────────────────────────────────
lsblk                           # Tampilkan blok device (disk, partisi)
lsblk -f                        # + info filesystem dan UUID
fdisk -l                        # Info partisi semua disk (butuh root)
sudo fdisk -l /dev/sda          # Info partisi disk tertentu
blkid                           # UUID dan tipe filesystem
cat /proc/partitions            # Info partisi dari kernel

# ── PARTISI DISK ────────────────────────────────────────────
sudo fdisk /dev/sdb             # Tool partisi interaktif (MBR/GPT)
sudo parted /dev/sdb            # Tool partisi modern
sudo cfdisk /dev/sdb            # Tool partisi berbasis menu (user-friendly)

# ── FORMAT FILESYSTEM ───────────────────────────────────────
sudo mkfs.ext4 /dev/sdb1        # Format dengan ext4
sudo mkfs.xfs /dev/sdb1         # Format dengan XFS
sudo mkswap /dev/sdb2           # Buat swap partition

# ── MOUNT & UNMOUNT ─────────────────────────────────────────
sudo mount /dev/sdb1 /mnt/data         # Mount partisi ke direktori
sudo mount -t ext4 /dev/sdb1 /mnt/     # Dengan tipe filesystem eksplisit
sudo umount /mnt/data                  # Unmount
sudo umount -l /mnt/data               # Lazy unmount (jika sedang dipakai)
mount                                  # Tampilkan semua yang sedang di-mount
cat /etc/fstab                         # Konfigurasi mount otomatis saat boot

# ── SWAP MANAGEMENT ─────────────────────────────────────────
free -h                         # Tampilkan penggunaan RAM dan swap
swapon --show                   # Tampilkan swap yang aktif
sudo swapon /dev/sdb2           # Aktifkan swap partition
sudo swapoff /dev/sdb2          # Nonaktifkan swap partition

# Buat swap file
sudo fallocate -l 2G /swapfile  # Buat file 2GB
sudo chmod 600 /swapfile        # Set permission
sudo mkswap /swapfile           # Format sebagai swap
sudo swapon /swapfile           # Aktifkan
```

---

## 📊 System Information & Monitoring

```bash
# ── INFO SISTEM ─────────────────────────────────────────────
uname -a                        # Info kernel lengkap
uname -r                        # Versi kernel
cat /etc/os-release             # Info distribusi OS
lsb_release -a                  # Info distribusi (apt install lsb-release)
hostnamectl                     # Info hostname dan OS
uptime                          # Lama sistem berjalan + load average
uptime -p                       # Format lebih readable
date                            # Tanggal dan waktu saat ini
timedatectl                     # Timezone dan NTP status

# ── HARDWARE INFO ───────────────────────────────────────────
lscpu                           # Info CPU detail
lsmem                           # Info memori
lspci                           # Daftar perangkat PCI (VGA, NIC, dll)
lsusb                           # Daftar perangkat USB
lshw                            # Info hardware lengkap (apt install lshw)
lshw -short                     # Format ringkas
dmidecode                       # Info dari DMI/BIOS (butuh root)
cat /proc/cpuinfo               # Info CPU dari kernel
cat /proc/meminfo               # Info memori dari kernel

# ── MONITORING REAL-TIME ────────────────────────────────────
top                             # Monitor proses + CPU + RAM
htop                            # Versi enhanced top
vmstat 1                        # Statistik virtual memory per detik
iostat 1                        # Statistik I/O disk
iotop                           # Monitor I/O per proses (apt install iotop)
iftop                           # Monitor bandwidth jaringan (apt install iftop)
nload                           # Monitor traffic jaringan (apt install nload)
glances                         # Dashboard monitoring all-in-one (apt install glances)
watch -n 2 'df -h'              # Jalankan perintah setiap 2 detik

# ── LOG SISTEM ──────────────────────────────────────────────
journalctl                      # Semua log systemd
journalctl -b                   # Log sejak boot terakhir
journalctl -f                   # Follow log real-time
journalctl -u nginx             # Log service tertentu
journalctl --since "1 hour ago"
journalctl -p err               # Filter berdasarkan priority (err, warning, info)
tail -f /var/log/syslog         # Pantau syslog real-time
tail -f /var/log/auth.log       # Log autentikasi
less /var/log/dpkg.log          # Log instalasi paket
```

---

## 🗜️ Archiving & Compression

```bash
# ── TAR (Tape Archive) ──────────────────────────────────────
# Membuat arsip
tar -cvf arsip.tar direktori/          # Buat arsip tanpa kompresi
tar -czvf arsip.tar.gz direktori/      # Buat arsip + kompresi gzip
tar -cjvf arsip.tar.bz2 direktori/    # Buat arsip + kompresi bzip2
tar -cJvf arsip.tar.xz direktori/     # Buat arsip + kompresi xz

# Mengekstrak arsip
tar -xvf arsip.tar                     # Ekstrak arsip
tar -xzvf arsip.tar.gz                 # Ekstrak arsip gzip
tar -xjvf arsip.tar.bz2               # Ekstrak arsip bzip2
tar -xJvf arsip.tar.xz                # Ekstrak arsip xz
tar -xvf arsip.tar -C /path/tujuan/   # Ekstrak ke direktori tertentu

# Melihat isi arsip (tanpa ekstrak)
tar -tvf arsip.tar                     # Daftar isi arsip
tar -tzvf arsip.tar.gz

# Opsi tar yang sering dipakai:
#   -c → Create (buat arsip)
#   -x → Extract (ekstrak)
#   -t → List (tampilkan isi)
#   -v → Verbose (tampilkan proses)
#   -f → File (nama file arsip)
#   -z → gzip compression
#   -j → bzip2 compression
#   -J → xz compression
#   -C → Change to directory

# ── ZIP ─────────────────────────────────────────────────────
zip -r arsip.zip direktori/            # Buat zip dari direktori
zip arsip.zip file1 file2             # Zip beberapa file
unzip arsip.zip                        # Ekstrak zip
unzip arsip.zip -d /path/tujuan/       # Ekstrak ke direktori tertentu
unzip -l arsip.zip                     # Lihat isi zip tanpa ekstrak
unzip -p arsip.zip file.txt            # Ekstrak satu file ke stdout

# ── GZIP & BZIP2 ────────────────────────────────────────────
gzip file.txt                          # Kompres menjadi file.txt.gz
gzip -d file.txt.gz                    # Dekompresi (hapus .gz)
gunzip file.txt.gz                     # Sama dengan gzip -d
gzip -k file.txt                       # Kompres (pertahankan file asli)
bzip2 file.txt                         # Kompres menjadi file.txt.bz2
bunzip2 file.txt.bz2                   # Dekompresi bzip2
```

---

## 🔍 Searching & Filtering

```bash
# ── FIND (Mencari File) ─────────────────────────────────────
find /path -name "namafile"            # Cari berdasarkan nama (case-sensitive)
find /path -iname "namafile"           # Case-insensitive
find /path -name "*.log"              # Cari berdasarkan ekstensi
find /path -type f                     # Hanya file
find /path -type d                     # Hanya direktori
find /path -type l                     # Hanya symlink
find /path -size +100M                 # File lebih besar dari 100MB
find /path -size -1k                   # File lebih kecil dari 1KB
find /path -mtime -7                   # Dimodifikasi dalam 7 hari terakhir
find /path -mtime +30                  # Dimodifikasi lebih dari 30 hari lalu
find /path -user namauser              # Milik user tertentu
find /path -group namagroup            # Milik group tertentu
find /path -perm 777                   # Permission persis 777
find /path -perm -o+w                  # Others memiliki write permission
find /path -empty                      # File/direktori kosong

# Find + Aksi
find /path -name "*.log" -delete       # Temukan dan hapus
find /path -name "*.txt" -exec chmod 644 {} \;  # Temukan dan jalankan perintah
find /tmp -mtime +7 -exec rm -f {} \; # Hapus file tmp lebih dari 7 hari

# ── GREP (Mencari dalam Konten File) ────────────────────────
grep "kata" namafile.txt               # Cari kata dalam file
grep -i "kata" namafile.txt            # Case-insensitive
grep -r "kata" /path/                  # Rekursif dalam direktori
grep -n "kata" namafile.txt            # Tampilkan nomor baris
grep -v "kata" namafile.txt            # Tampilkan baris yang TIDAK cocok
grep -c "kata" namafile.txt            # Hitung jumlah kemunculan
grep -l "kata" /path/*                 # Hanya tampilkan nama file yang cocok
grep -A 3 "kata" namafile.txt          # 3 baris setelah match
grep -B 3 "kata" namafile.txt          # 3 baris sebelum match
grep -E "pola1|pola2" namafile.txt     # Extended regex (OR)
grep -w "kata" namafile.txt            # Match whole word saja
grep "^kata" namafile.txt              # Baris yang dimulai dengan "kata"
grep "kata$" namafile.txt              # Baris yang diakhiri "kata"

# Kombinasi grep dengan pipe
ps aux | grep nginx                    # Filter output ps
cat /var/log/auth.log | grep "Failed"  # Cari login gagal
dmesg | grep -i error                  # Cari error di dmesg

# ── SORT, UNIQ, CUT, AWK ────────────────────────────────────
sort file.txt                          # Urutkan baris secara alfabetis
sort -r file.txt                       # Urutan terbalik
sort -n file.txt                       # Urutan numerik
sort -k 2 file.txt                     # Urutkan berdasarkan kolom 2
uniq file.txt                          # Hapus baris duplikat berurutan
sort file.txt | uniq                   # Hapus semua duplikat
sort file.txt | uniq -c                # Hitung kemunculan tiap baris
cut -d':' -f1 /etc/passwd              # Ambil field 1, delimiter ':'
cut -c1-10 file.txt                    # Ambil karakter 1-10 tiap baris
awk '{print $1}' file.txt              # Print kolom pertama
awk -F':' '{print $1,$3}' /etc/passwd  # Print kolom 1 dan 3, delimiter ':'
awk 'NR==5' file.txt                   # Print baris ke-5
```

---

## 🖥️ Shell & Environment

```bash
# ── VARIABEL ENVIRONMENT ────────────────────────────────────
env                             # Tampilkan semua variabel environment
printenv                        # Sama dengan env
echo $PATH                      # Tampilkan nilai variabel PATH
echo $HOME                      # Direktori home user
echo $USER                      # Username saat ini
echo $SHELL                     # Shell yang dipakai
echo $HOSTNAME                  # Nama hostname

# Set variabel (hanya berlaku di sesi ini)
NAMA="Debian"
echo $NAMA

# Export variabel (tersedia untuk proses anak)
export NAMA="Debian"
export PATH=$PATH:/usr/local/myapp/bin    # Tambah path baru

# Variabel permanen → tambahkan ke ~/.bashrc atau ~/.profile
echo 'export MYVAR="value"' >> ~/.bashrc
source ~/.bashrc                          # Reload konfigurasi

# ── ALIAS ───────────────────────────────────────────────────
alias ll='ls -la'              # Buat alias sementara
alias update='sudo apt update && sudo apt upgrade'
unalias ll                     # Hapus alias
alias                          # Tampilkan semua alias aktif

# Alias permanen → tambahkan ke ~/.bashrc
echo "alias ll='ls -la'" >> ~/.bashrc

# ── HISTORY ─────────────────────────────────────────────────
history                         # Tampilkan riwayat perintah
history 20                      # 20 perintah terakhir
!n                              # Jalankan ulang perintah ke-n
!!                              # Jalankan ulang perintah terakhir
!string                         # Jalankan ulang perintah yang diawali "string"
Ctrl+R                          # Cari perintah di history (reverse search)
history -c                      # Hapus seluruh history

# ── REDIRECT & PIPE ─────────────────────────────────────────
perintah > file.txt             # Redirect stdout ke file (timpa)
perintah >> file.txt            # Redirect stdout (tambah/append)
perintah 2> error.txt           # Redirect stderr ke file
perintah &> semua.txt           # Redirect stdout + stderr
perintah < input.txt            # Ambil stdin dari file
perintah1 | perintah2           # Pipe: output cmd1 → input cmd2

# Contoh kombinasi
ls -la | grep ".txt" | sort     # List → filter → sort
cat file | sort | uniq | wc -l  # Hitung baris unik
cat /var/log/auth.log | grep "Failed" | tail -20
```

---

## 🔧 Systemd & Service Management

```bash
# ── STATUS & INFORMASI ──────────────────────────────────────
systemctl status                        # Status semua service aktif
systemctl status nginx                  # Status service tertentu
systemctl status nginx.service          # Nama lengkap dengan .service
systemctl list-units --type=service     # Daftar semua service
systemctl list-units --state=failed     # Service yang gagal
systemctl list-unit-files               # Semua unit file + status enable

# ── KONTROL SERVICE ─────────────────────────────────────────
sudo systemctl start nginx              # Mulai service
sudo systemctl stop nginx               # Hentikan service
sudo systemctl restart nginx            # Restart service
sudo systemctl reload nginx             # Reload konfigurasi (tanpa restart)
sudo systemctl enable nginx             # Aktifkan saat boot
sudo systemctl disable nginx            # Nonaktifkan saat boot
sudo systemctl enable --now nginx       # Enable + langsung start
sudo systemctl mask nginx               # Blokir total (tidak bisa distart)
sudo systemctl unmask nginx             # Buka blokir

# ── REBOOT & SHUTDOWN ───────────────────────────────────────
sudo systemctl reboot                   # Reboot sistem
sudo systemctl poweroff                 # Matikan sistem
sudo systemctl halt                     # Halt sistem
sudo shutdown -h now                    # Matikan sekarang
sudo shutdown -r now                    # Reboot sekarang
sudo shutdown -h +10                    # Matikan dalam 10 menit
sudo shutdown -c                        # Batalkan shutdown terjadwal

# ── BOOT TARGET ─────────────────────────────────────────────
systemctl get-default                   # Tampilkan default target
sudo systemctl set-default multi-user.target  # Set ke mode console (tanpa GUI)
sudo systemctl set-default graphical.target   # Set ke mode GUI
sudo systemctl isolate rescue.target    # Pindah ke mode rescue

# ── LOG SERVICE ─────────────────────────────────────────────
journalctl -u nginx                     # Log service nginx
journalctl -u nginx -f                  # Follow log nginx
journalctl -u nginx --since "1 hour ago"
journalctl -xe                          # Log terbaru + detail error
```

---

## 🛡️ Firewall (UFW & iptables)

```bash
# ── UFW (Uncomplicated Firewall) ────────────────────────────
# Install
sudo apt install ufw

# Status & Enable/Disable
sudo ufw status                 # Cek status firewall
sudo ufw status verbose         # Status detail dengan rules
sudo ufw enable                 # Aktifkan firewall
sudo ufw disable                # Nonaktifkan firewall
sudo ufw reset                  # Reset ke default (hapus semua rules)

# Allow & Deny Rules
sudo ufw allow 22               # Izinkan port 22 (TCP & UDP)
sudo ufw allow 22/tcp           # Izinkan port 22 TCP saja
sudo ufw allow 80/tcp           # HTTP
sudo ufw allow 443/tcp          # HTTPS
sudo ufw allow ssh              # Izinkan berdasarkan nama service
sudo ufw allow http
sudo ufw allow https
sudo ufw deny 23                # Blokir port 23 (Telnet)
sudo ufw deny from 192.168.1.100  # Blokir IP tertentu

# Rules yang Lebih Spesifik
sudo ufw allow from 192.168.1.0/24         # Izinkan seluruh subnet
sudo ufw allow from 10.0.0.1 to any port 22  # Izinkan IP tertentu ke port 22
sudo ufw allow in on eth0 to any port 80   # Izinkan hanya dari interface eth0

# Menghapus Rules
sudo ufw delete allow 80        # Hapus rule allow port 80
sudo ufw delete deny 23         # Hapus rule deny port 23
sudo ufw status numbered        # Tampilkan rules dengan nomor
sudo ufw delete 3               # Hapus rule berdasarkan nomor

# Default Policy
sudo ufw default deny incoming  # Tolak semua koneksi masuk (default aman)
sudo ufw default allow outgoing # Izinkan semua koneksi keluar

# ── IPTABLES (Dasar) ────────────────────────────────────────
sudo iptables -L                         # Tampilkan semua rules
sudo iptables -L -n -v                   # Detail dengan angka
sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT   # Izinkan SSH
sudo iptables -A INPUT -p tcp --dport 80 -j ACCEPT   # Izinkan HTTP
sudo iptables -A INPUT -j DROP           # Drop semua sisanya
sudo iptables -D INPUT -j DROP           # Hapus rule DROP
sudo iptables-save > /etc/iptables/rules.v4  # Simpan rules
sudo iptables-restore < /etc/iptables/rules.v4  # Restore rules
```

---

## 🔑 SSH & Remote Access

```bash
# ── KONEKSI SSH ─────────────────────────────────────────────
ssh user@hostname                       # Koneksi SSH dasar
ssh user@192.168.1.100                  # Koneksi ke IP
ssh -p 2222 user@hostname               # Port SSH berbeda
ssh -i ~/.ssh/keyfile.pem user@host     # Gunakan SSH key tertentu
ssh -v user@host                        # Verbose (debug mode)
ssh -X user@host                        # Enable X11 forwarding (GUI)

# ── SSH KEY MANAGEMENT ──────────────────────────────────────
# Generate SSH key pair
ssh-keygen -t rsa -b 4096               # Generate RSA 4096-bit
ssh-keygen -t ed25519                   # Generate Ed25519 (lebih modern)
ssh-keygen -t ed25519 -C "email@example.com"  # Dengan komentar

# Salin public key ke server remote
ssh-copy-id user@hostname               # Metode otomatis
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@host  # Key tertentu

# Atau manual:
cat ~/.ssh/id_rsa.pub | ssh user@host "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"

# File-file SSH
~/.ssh/id_rsa                   # Private key (RAHASIAKAN!)
~/.ssh/id_rsa.pub               # Public key (aman dibagikan)
~/.ssh/authorized_keys          # Public key yang diizinkan login
~/.ssh/known_hosts              # Fingerprint host yang dikenal
~/.ssh/config                   # Konfigurasi SSH client

# ── SSH CONFIG (~/.ssh/config) ──────────────────────────────
# Tambahkan ke ~/.ssh/config:
# Host myserver
#     HostName 192.168.1.100
#     User admin
#     Port 2222
#     IdentityFile ~/.ssh/mykey
#
# Setelah konfigurasi, cukup ketik:
# ssh myserver

# ── KONFIGURASI SSH SERVER (/etc/ssh/sshd_config) ───────────
# Rekomendasi pengaturan keamanan:
# Port 2222                       # Ubah dari port default 22
# PermitRootLogin no              # Larang login langsung sebagai root
# PasswordAuthentication no       # Hanya izinkan key-based auth
# PubkeyAuthentication yes        # Aktifkan autentikasi kunci
# MaxAuthTries 3                  # Batasi percobaan login
# AllowUsers namauser             # Hanya izinkan user tertentu

sudo systemctl restart ssh        # Terapkan perubahan konfigurasi

# ── SSH TUNNELING ────────────────────────────────────────────
# Local port forwarding (akses service remote dari lokal)
ssh -L 8080:localhost:80 user@host      # localhost:8080 → remote:80

# Remote port forwarding (expose lokal ke remote)
ssh -R 8080:localhost:3000 user@host    # remote:8080 → localhost:3000

# Dynamic SOCKS proxy
ssh -D 1080 user@host                   # Buat SOCKS5 proxy di port 1080
```

---

## 📝 Shell Scripting Basics

```bash
#!/bin/bash
# ═══════════════════════════════════════════════════════════
#  Script   : contoh_script.sh
#  Deskripsi: Contoh dasar shell scripting Bash
#  Penggunaan: chmod +x script.sh && ./script.sh
# ═══════════════════════════════════════════════════════════

# ── VARIABEL ────────────────────────────────────────────────
NAMA="Debian"
VERSI=12
PESAN="Selamat datang di $NAMA $VERSI"
echo $PESAN

# Variabel spesial
echo "Nama script : $0"
echo "Argumen ke-1: $1"
echo "Argumen ke-2: $2"
echo "Jumlah arg  : $#"
echo "Semua arg   : $@"
echo "PID script  : $$"
echo "Exit code   : $?"

# ── INPUT PENGGUNA ──────────────────────────────────────────
read -p "Masukkan nama Anda: " USER_INPUT
echo "Halo, $USER_INPUT!"
read -s -p "Masukkan password: " PASS    # -s = tidak ditampilkan
echo ""

# ── KONDISIONAL ─────────────────────────────────────────────
ANGKA=10

if [ $ANGKA -gt 5 ]; then
    echo "Angka lebih besar dari 5"
elif [ $ANGKA -eq 5 ]; then
    echo "Angka sama dengan 5"
else
    echo "Angka lebih kecil dari 5"
fi

# Operator perbandingan angka: -eq -ne -lt -le -gt -ge
# Operator string: == != -z (kosong) -n (tidak kosong)
# Operator file: -f (file) -d (dir) -e (exists) -r -w -x

# Cek apakah file ada
if [ -f "/etc/passwd" ]; then
    echo "File /etc/passwd ditemukan"
fi

# ── CASE ────────────────────────────────────────────────────
read -p "Pilih menu (a/b/c): " PILIHAN
case $PILIHAN in
    a) echo "Anda memilih A" ;;
    b) echo "Anda memilih B" ;;
    c) echo "Anda memilih C" ;;
    *) echo "Pilihan tidak valid" ;;
esac

# ── PERULANGAN ──────────────────────────────────────────────
# For loop
for i in 1 2 3 4 5; do
    echo "Iterasi ke-$i"
done

for i in {1..10}; do
    echo -n "$i "
done
echo ""

for file in /etc/*.conf; do
    echo "Config file: $file"
done

# While loop
COUNTER=0
while [ $COUNTER -lt 5 ]; do
    echo "Counter: $COUNTER"
    ((COUNTER++))
done

# Until loop (kebalikan while)
COUNTER=0
until [ $COUNTER -ge 5 ]; do
    echo "Until: $COUNTER"
    ((COUNTER++))
done

# ── FUNGSI ──────────────────────────────────────────────────
greet() {
    local NAMA=$1           # Variabel lokal
    echo "Halo, $NAMA!"
    return 0                # Return exit code
}

greet "World"
greet "Debian"

hitung_luas() {
    local PANJANG=$1
    local LEBAR=$2
    echo $((PANJANG * LEBAR))  # Arithmetic
}

LUAS=$(hitung_luas 5 3)
echo "Luas: $LUAS"

# ── ERROR HANDLING ──────────────────────────────────────────
set -e          # Exit script jika ada perintah yang gagal
set -u          # Error jika variabel tidak terdefinisi
set -o pipefail # Error jika ada perintah di pipe yang gagal

perintah || echo "Perintah gagal, tapi script lanjut"
perintah && echo "Perintah berhasil"

# Trap untuk cleanup
cleanup() {
    echo "Membersihkan..."
    rm -f /tmp/tempfile
}
trap cleanup EXIT    # Jalankan cleanup saat script selesai
trap cleanup INT     # Jalankan cleanup saat Ctrl+C
```

---

## ⌨️ Useful Shortcuts & Tips

### Keyboard Shortcuts (Bash)

| Shortcut | Fungsi |
|----------|--------|
| `Ctrl+C` | Hentikan proses yang berjalan |
| `Ctrl+Z` | Suspend proses (kirim ke background) |
| `Ctrl+D` | Logout / EOF |
| `Ctrl+L` | Clear terminal (sama dengan `clear`) |
| `Ctrl+A` | Pindah ke awal baris |
| `Ctrl+E` | Pindah ke akhir baris |
| `Ctrl+U` | Hapus dari kursor ke awal baris |
| `Ctrl+K` | Hapus dari kursor ke akhir baris |
| `Ctrl+W` | Hapus satu kata ke kiri |
| `Ctrl+R` | Cari di history (reverse search) |
| `Ctrl+G` | Keluar dari reverse search |
| `Tab` | Auto-complete perintah/nama file |
| `Tab Tab` | Tampilkan semua kemungkinan |
| `↑ / ↓` | Navigasi history perintah |
| `!!` | Ulangi perintah terakhir |
| `!$` | Argumen terakhir dari perintah sebelumnya |
| `Alt+.` | Sisipkan argumen terakhir |

### Tips & Trik Produktivitas

```bash
# Jalankan perintah terakhir sebagai root
sudo !!

# Buat direktori dan langsung masuk ke dalamnya
mkdir -p /path/to/dir && cd $_

# Salin output ke clipboard (jika ada xclip)
perintah | xclip -selection clipboard

# Tampilkan perintah tanpa menjalankannya
echo rm -rf /path/

# Hitung waktu eksekusi perintah
time perintah

# Jalankan beberapa perintah
cmd1 ; cmd2 ; cmd3          # Jalankan berurutan, abaikan error
cmd1 && cmd2                # Jalankan cmd2 hanya jika cmd1 sukses
cmd1 || cmd2                # Jalankan cmd2 hanya jika cmd1 gagal

# Cari dan buka manual
man perintah                # Buka manual page
man -k kata_kunci           # Cari manual berdasarkan keyword
tldr perintah               # Contoh penggunaan singkat (apt install tldr)
perintah --help             # Bantuan singkat

# Alias berguna yang bisa ditambahkan ke ~/.bashrc
alias ll='ls -lah'
alias la='ls -A'
alias grep='grep --color=auto'
alias df='df -h'
alias du='du -h'
alias ..='cd ..'
alias ...='cd ../..'
alias update='sudo apt update && sudo apt upgrade'
alias ports='ss -tulnp'
alias myip='curl -s https://ipecho.net/plain; echo'
```

---

<div align="center">

![Debian](https://img.shields.io/badge/Debian-Linux-A81D33?style=flat-square&logo=debian&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-Scripting-4EAA25?style=flat-square&logo=gnubash&logoColor=white)

**Hopefully this documentation is helpful!**
⭐ Star this repo if it helps your learning process!

*"Practice makes perfect — open the terminal and start practicing!"*

</div>
