# Nextcloud + OnlyOffice (Docker Compose)

Repository ini berisi konfigurasi **Docker Compose** untuk menjalankan **Nextcloud** terintegrasi dengan **OnlyOffice Document Server** dalam satu network Docker yang sama, dengan penyimpanan data persisten di host.

---

## Arsitektur

Komponen:
- Nextcloud (Apache)
- PostgreSQL (database Nextcloud)
- OnlyOffice Document Server
- Docker bridge network bersama

Komunikasi internal:
- Nextcloud → OnlyOffice melalui hostname container (`onlyoffice-documentserver`)
- Nextcloud → PostgreSQL melalui service name (`postgres`)

---

## Prasyarat

- Linux host
- Docker Engine
- Docker Compose v2
- Port host tersedia:
  - `8050` → Nextcloud
  - `8051` → OnlyOffice

---

## Struktur Direktori Host

/mnt/sdd1/
├── nextcloud/
│ ├── app/ # Data Nextcloud
│ └── db/ # Database PostgreSQL
├── onlyoffice/
│ ├── data/ # Data OnlyOffice
│ ├── logs/ # Log OnlyOffice
│ ├── lib/ # Library OnlyOffice
│ └── db/ # Database internal OnlyOffice
└── docker/
└── nextcloud-onlyoffice/
└── docker-compose.yaml

yaml
Salin kode

---

## docker-compose.yaml

File utama berisi tiga service:
- `postgres`
- `nextcloud`
- `onlyoffice`

Network:
- `nextcloud_net` (bridge)

Deployment bersifat stateful, seluruh data disimpan di luar container.

---

