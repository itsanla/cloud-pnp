# PNP Student Cloud

Self-service Private IaaS / VMaaS berbasis server kampus TI-PNP  
Mahasiswa bisa membuat, mengelola, dan mengakses VM/VPS sendiri melalui web portal tanpa harus minta izin admin setiap kali.

![PNP Student Cloud Banner](https://via.placeholder.com/800x300/0d47a1/ffffff?text=PNP+Student+Cloud)  
*(Ganti dengan screenshot dashboard atau diagram arsitektur nanti)*

## Tujuan Proyek

Memberikan kemudahan bagi mahasiswa Teknik Informatika Politeknik Negeri Padang untuk:
- Membuat VM dengan template OS pilihan (Ubuntu, Debian, dll)
- Mengakses console via browser (noVNC)
- Preview aplikasi web secara publik melalui subdomain otomatis (misal: nama.preview.cloud.pnp.ac.id)
- Mengatur quota resource, auto-shutdown, dan monitoring penggunaan

Semua berjalan **100% on-premise** di server kampus, tanpa biaya cloud.

## Fitur Utama

- Login mahasiswa → Launch VM (pilih OS, CPU, RAM, Disk)
- Web console langsung di browser
- Subdomain preview otomatis untuk web app (HTTPS via Cloudflare)
- Quota resource per user + auto-shutdown VM idle
- Monitoring penggunaan CPU/RAM/Disk
- Akses aman tanpa IP public per VM (menggunakan Cloudflare Tunnel)

## Teknologi Stack

| Layer              | Teknologi                          | Keterangan                              |
|--------------------|------------------------------------|-----------------------------------------|
| Hypervisor         | Proxmox VE                         | KVM + LXC, API matang                   |
| Frontend           | Next.js 15 (App Router)            | Dashboard & portal mahasiswa            |
| Backend            | NestJS 11                          | API orchestration & business logic      |
| Database           | PostgreSQL                         | Data user, VM, quota                    |
| Reverse Proxy      | Caddy                              | Dynamic routing untuk preview VM        |
| Public Access      | Cloudflare Tunnel                  | Tanpa IP public, HTTPS otomatis         |
| Storage            | ZFS                                | Snapshot cepat & thin provisioning      |
| Networking         | Internal bridge + NAT              | Semua VM di jaringan privat kampus      |

## Arsitektur Singkat
