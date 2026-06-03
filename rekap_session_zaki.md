# Rekap Sesi Belajar — Muhammad Zaki Zein
**Network Engineer Roadmap — Linux Fundamentals**
Tujuan: Politeknik Negeri Jakarta — Teknik Multimedia & Jaringan
github.com/zkizen · zakizen415@gmail.com

---

## 1. Profil & Background

| Info | Detail |
|---|---|
| Nama | Muhammad Zaki Zein (@zkizen) |
| Sekolah | SMK Al-Muhtadin Depok — Jurusan TJKT |
| PKL | PT Intikom Berlian Mustika (Jul-Des 2025) — Project Technician |
| Tujuan | Politeknik Negeri Jakarta — Teknik Multimedia & Jaringan |
| GitHub | github.com/zkizen |
| Email | zakizen415@gmail.com |

### Skill yang Sudah Dimiliki
- Cisco IOS / GNS3 — OSPF multiarea lab sudah live
- Mikrotik RouterOS
- Linux CLI (Ubuntu/WSL) — diperdalam di sesi ini
- OSPF, BGP, VLAN, Firewall
- Python (basic) — network monitor + Telegram alert
- Ansible (basic) — backup config router
- Git & GitHub

### Tools yang Terinstall
- GNS3 + Cisco IOS image
- WSL Ubuntu + Ansible 2.16.3
- Python 3.14.3 (Windows)
- Git for Windows + SSH key setup
- VSCode

---

## 2. Progress Network Engineer Roadmap

### Fase 1 — Fundamentals ✅ SELESAI
- [x] LAN / MAN / WAN / PAN / VPN
- [x] OSI 7 Layers
- [x] TCP/IP Model
- [x] IPv4 vs IPv6
- [x] Subnetting & CIDR / VLSM
- [x] Basic terminology (IP, MAC, port, socket)

### Fase 2 — Network Devices & Protocols ✅ SELESAI
- [x] Routers, Switches, Hub, AP, Modems
- [x] MAC Address & ARP
- [x] DNS, DHCP
- [x] HTTP/HTTPS, FTP/SFTP, SSH

### Fase 3 — Routing & Switching ⚡ SEBAGIAN
- [x] Static vs Dynamic Routing
- [x] OSPF (multiarea lab live di GitHub)
- [x] BGP
- [x] EIGRP / RIP
- [x] VLAN & STP
- [ ] Link Aggregation
- [ ] MPLS

### Fase 4 — Linux for Networking ✅ SELESAI (sesi ini)
- [x] Navigasi filesystem (pwd, ls, cd, ~)
- [x] Buat/hapus/edit file (touch, mkdir, rm, cp, mv)
- [x] File Permissions (chmod, chain permission)
- [x] chown — ganti kepemilikan file
- [x] Service Management (systemctl, journalctl)
- [x] Linux Networking Commands (ip, ss, ping, traceroute)
- [x] SSH & File Transfer (scp, rsync, SSH config)

### Fase 5 — Network Security ⚡ SEDANG JALAN
- [x] Firewalls (Packet Filtering, Stateful, NGFW)
- [x] DoS & DDoS Attacks
- [ ] IDS / IPS (Snort/Suricata) — next!
- [ ] Encryption Basics
- [ ] Zero Trust Architecture
- [ ] IPSec vs SSL VPN — next!
- [ ] Site-to-Site vs Remote Access VPN

### Fase 6 — Monitoring & Observability ⚡ SEBAGIAN
- [x] Python monitoring script (Telegram alert) — live di GitHub
- [ ] Wireshark
- [ ] Nmap
- [ ] SNMP / SNTP
- [ ] NetFlow / sFlow
- [ ] Grafana + InfluxDB

### Fase 7 — Automation & Cloud ⏳ BELUM MULAI
- [ ] Ansible lanjut (Cisco/Mikrotik playbook)
- [ ] Docker networking
- [ ] AWS/GCP VPC basics
- [ ] QoS / Traffic Shaping
- [ ] Load Balancer (Round Robin, Failover)
- [ ] Scapy dasar

---

## 3. Projects Live di GitHub

| Project | Teknologi | Status |
|---|---|---|
| ospf-multiarea-lab | GNS3, Cisco IOS, OSPF | ✅ Live |
| network-monitor-python | Python 3, Telegram Bot API | ✅ Live |
| netsec-automation-toolkit | Ansible, Python, WSL Ubuntu | ✅ Live |

### Next Projects (Rekomendasi)
| Project | Teknologi | Prioritas |
|---|---|---|
| VPN Lab (IPSec / OpenVPN) | OpenVPN, Linux, IPSec | Tinggi |
| IDS/IPS Lab | Snort/Suricata, Linux | Tinggi |
| SNMP + Grafana Dashboard | SNMP, Grafana, InfluxDB | Sedang |

---

## 4. Materi yang Dipelajari Sesi Ini

### Bab 1 — Navigasi Filesystem
```bash
pwd              # Lihat posisi sekarang
ls -la           # Lihat isi folder + detail + hidden files
cd ~             # Balik ke home (/home/zaki)
cd ..            # Naik satu level
cd /etc          # Pindah ke path absolut
```
> `~` = `/home/zaki` · `.` = folder saat ini · `..` = folder di atas

---

### Bab 2 — File Permissions
**Rumus:** r=4, w=2, x=1 — dijumlah per kelompok (owner/group/others)

```
-  rw-  r--  r--    zaki  zaki   file1.txt
^   ^    ^    ^
|  owner group other
- = file | d = directory | l = symlink
```

| chmod | Permission | Kapan dipakai |
|---|---|---|
| 600 | rw------- | SSH key, file rahasia |
| 644 | rw-r--r-- | Config file biasa |
| 755 | rwxr-xr-x | Script publik |
| 000 | ---------- | Blok total |

```bash
chmod u+x script.py      # Kasih execute ke owner
chmod 600 ~/.ssh/id_rsa  # SSH key wajib 600
chmod 755 ~              # Buka akses home ke others
```

> **Chain Permission:** Linux cek permission SEMUA folder di jalurnya.
> Satu folder diblok = gagal total meski file-nya boleh diakses.
> Contoh: `/home/zaki` permission 750 (others=---) → tamu tidak bisa masuk ke `latihan-permissions/` meski file-nya accessible.

---

### Bab 3 — chown
```bash
sudo chown tamu file.txt           # Ganti owner ke tamu
sudo chown tamu:tamu file.txt      # Ganti owner + group
sudo chown zaki:zaki file.txt      # Kembaliin ke zaki
sudo chown -R zaki:zaki folder/    # Rekursif seluruh folder
```

> **chmod vs chown:**
> - `chmod` = ganti IZIN (siapa boleh ngapain)
> - `chown` = ganti PEMILIK (siapa yang punya)

---

### Bab 4 — Service Management (systemctl)

```bash
systemctl start X          # Nyalain sekarang
systemctl stop X           # Matiin sekarang
systemctl restart X        # Restart
systemctl enable X         # Otomatis nyala saat boot
systemctl disable X        # Matiin autostart
systemctl status X         # Cek kondisi + info
systemctl is-enabled X     # Cek enabled/disabled
journalctl -u X -n 20      # Lihat 20 log terakhir
journalctl -u X -f         # Lihat log realtime
```

> **Penting:** `start/stop` = kondisi SEKARANG. `enable/disable` = kondisi saat BOOT. Keduanya **independent!**

| Active | Enabled | Artinya |
|---|---|---|
| running | enabled | Jalan sekarang + otomatis boot ✅ |
| inactive | enabled | Mati sekarang, nyala kalau reboot |
| running | disabled | Jalan sekarang, mati kalau reboot |
| inactive | disabled | Mati total |

> **Signal 15 (SIGTERM)** = dikirim oleh `systemctl stop` → matiin dengan bersih
> **Signal 9 (SIGKILL)** = paksa mati, tidak ada cleanup

---

### Bab 5 — Linux Networking Commands

```bash
ip addr              # Lihat IP semua interface
ip route             # Lihat routing table + gateway
ss -tulnp            # Lihat port yang listening
ping -c 4 8.8.8.8    # Test koneksi + latency
traceroute 8.8.8.8   # Trace jalur paket hop per hop
curl ifconfig.me     # Cek public IP
```

**Flag ss:** `-t`=TCP · `-u`=UDP · `-l`=listening · `-n`=numeric · `-p`=process

**Dari praktek (traceroute ke 8.8.8.8):**
```
hop 1 → 172.18.240.1   = Gateway WSL
hop 2 → 192.168.18.1   = Router rumah
hop 3 → 10.23.0.1      = Router ISP
hop 5 → 72.14.216.48   = Jaringan Google
hop 7 → 8.8.8.8        = Google DNS ✅
```

> `* * *` di traceroute = router sengaja blokir ICMP, bukan berarti putus.
> `172.18.243.187` = IP private WSL · `103.121.17.90` = public IP (hasil NAT)

---

### Bab 6 — SSH & File Transfer

```bash
# SSH Login
ssh zaki@localhost               # Login dengan password
ssh-copy-id zaki@localhost       # Copy public key ke server
ssh localhost                    # Login tanpa password (key auth)
ssh localhost "ls -la /tmp/"     # Jalanin command di remote langsung

# SCP — copy file
scp file.txt zaki@localhost:/tmp/         # Kirim file ke server
scp -r ~/folder/ zaki@localhost:/tmp/     # Kirim folder
scp zaki@localhost:/tmp/file.txt ~/       # Ambil file dari server

# rsync — sync folder (lebih efisien)
rsync -avz ~/src/ zaki@localhost:/dst/    # Hanya kirim yang berubah
```

**scp vs rsync:**
| | scp | rsync |
|---|---|---|
| Yang dikirim | Semua file | Hanya yang berubah |
| Efisiensi | Boros bandwidth | Hemat bandwidth |
| Cocok untuk | Transfer sekali | Backup & sync rutin |

**SSH Config (`~/.ssh/config`):**
```
Host local
    HostName localhost
    User zaki
    IdentityFile ~/.ssh/id_ed25519
```
Setelah setup: `ssh local` = `ssh zaki@localhost` ✅

> **File SSH penting:**
> - `id_ed25519` → private key, permission **600**, JANGAN dibagikan
> - `id_ed25519.pub` → public key, permission 644, boleh dibagikan
> - `authorized_keys` → daftar public key yang boleh login
> - `known_hosts` → daftar server yang pernah dikonek

> **Ansible** pakai SSH key di balik layar — itulah kenapa `netsec-automation-toolkit` lo bisa konek ke router tanpa password manual.

---

## 5. PR yang Perlu Diperdalam

| No | Topik | Fokus |
|---|---|---|
| 1 | Kenapa OSPF butuh Area 0? | Backbone area, ABR, LSA flooding |
| 2 | DR vs BDR di OSPF | Election process, multi-access network |
| 3 | IPSec vs SSL VPN | Mekanisme berbeda, use case berbeda |
| 4 | Encryption basics (AES, RSA, DH) | Dasar semua security — VPN, SSH, HTTPS |
| 5 | Git merge conflict | Simulasikan scenario, 3-way merge vs rebase |
| 6 | Cara kerja Ansible di balik layar | SSH → command → collect output |

---

## 6. Next Steps

1. **VPN: IPSec vs SSL** — setup OpenVPN di Linux (WSL Ubuntu)
2. **IDS/IPS** — Snort/Suricata, buat custom rules
3. **Scapy dasar** — packet crafting & analysis
4. **SNMP + NetFlow** — monitoring protocol
5. **Grafana + InfluxDB** — visualisasi metrics jaringan

---

## 7. Dosen TMJ PNJ yang Relevan

| Dosen | Bidang | Relevansi |
|---|---|---|
| Deflana Arnaidy, S.Tp., M.SI | Cyber Security, Network Security | ⭐ Sangat relevan |
| Ayu Roryjda Zain, S.ST., M.T | ICT, Jaringan Komputer, Keamanan Jaringan | ⭐ Sangat relevan |
| Asep Kurniawan, S.Pd., M.Kom | Keamanan Jaringan dan IoT | ⭐ Sangat relevan |
| Ik Muhamad Malik Matin, S.Kom., M.T | Cyber Security, Intelligence System | ⭐ Sangat relevan |
| Dr. Prihatini Oktaviyarti | IoT, Machine Learning | Relevan |
| Maria Agustin, S.Kom., M.Kom | Internet of Things | Relevan |
| Chandra Wirawan, S.Kom., M.Kom | Cryptography, IoT, Data Mining | Relevan |

---

*Rekap ini dibuat di akhir sesi belajar. Paste ke chat baru untuk lanjut dari titik ini.*
*github.com/zkizen · zakizen415@gmail.com · PNJ TMJ 2026*
