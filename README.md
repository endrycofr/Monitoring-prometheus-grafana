

# Monitoring dengan Prometheus & Grafana

Project ini bertujuan menyediakan solusi pemantauan (monitoring) menggunakan **Prometheus** dan **Grafana**. Cocok untuk memonitor aplikasi, infrastruktur, dan metrik custom.

## Tabel Isi

1. [Deskripsi](#deskripsi)  
2. [Fitur](#fitur)  
3. [Arsitektur & Komponen](#arsitektur--komponen)  
4. [Prasyarat](#prasyarat)  
5. [Instalasi](#instalasi)  
6. [Konfigurasi](#konfigurasi)  
7. [Penggunaan](#penggunaan)  
8. [Pengembangan](#pengembangan)  
9. [Troubleshooting](#troubleshooting)  
10. [Lisensi](#lisensi)  


## Deskripsi

Repository ini menyediakan setup dasar monitoring menggunakan:

- **Prometheus** sebagai sistem pengoleksi metrik  
- **Grafana** sebagai dashboard visualisasi  
- **Docker / Docker Compose** untuk deployment lokal maupun lingkungan development  

Tujuan utama:  

- Memantau kesehatan sistem (CPU, memori, disk, jaringan)  
- Menampilkan metrik aplikasi (latensi, throughput, error rate)  
- Menyajikan dashboard yang informatif dan mudah digunakan  



## Fitur

- Deployment cepat menggunakan `docker-compose`  
- Dashboard Grafana sudah terkonfigurasi dengan panel utama  
- Kemampuan untuk menambah *exporter* metrik tambahan (mis. `node_exporter`, `application exporter`)  
- Alerting (bisa dikembangkan lebih lanjut dengan Alertmanager)  



## Arsitektur & Komponen

| Komponen      | Fungsi |
|---------------|--------|
| **Prometheus** | Mengambil / mengumpulkan metrik dari target / exporter, menyimpan dalam time series database |
| **Exporters**  | Contoh: `node_exporter`, `blackbox_exporter`. Mengumpulkan metrik lingkungan, sistem, dan aplikasi |
| **Grafana**    | Membuat dashboard visualisasi berdasarkan data dari Prometheus |
| **Docker & Docker Compose** | Membantu orkestrasi dan memudahkan setup lingkungan |



## Prasyarat

Pastikan kamu sudah menginstal:

- **Docker** dan **Docker Compose**  
- OS yang mendukung Docker (Linux, macOS, atau Windows)  
- Port yang diperlukan tidak konflik (default: Prometheus `9090`, Grafana `3000`)  
- Izin akses ke file & jaringan (untuk exporter tertentu)  



## Instalasi

1. Clone repo ini:

   ```bash
   git clone https://github.com/endrycofr/Monitoring-prometheus-grafana.git
   cd Monitoring-prometheus-grafana
````

2. Jalankan dengan Docker Compose:

   ```bash
   docker-compose up -d
   ```

   Ini akan menjalankan container untuk Prometheus, Grafana, dan exporter (jika ada).

---

## Konfigurasi

* **`prometheus/prometheus.yml`** → daftar target exporter, scrape interval, dsb.
* **`grafana/`** → dashboard, provisioning datasource, dsb.
* **`docker-compose.yml`** → konfigurasi container, volume mounting, dan port mapping.

Jika ingin menambah exporter baru:

1. Tambahkan service di `docker-compose.yml`
2. Tambahkan target di `prometheus/prometheus.yml`
3. (Opsional) Tambahkan panel dashboard di Grafana

---

## Penggunaan

* Akses Prometheus UI di: [http://localhost:9090](http://localhost:9090)
* Akses Grafana di: [http://localhost:3000](http://localhost:3000)

Default login Grafana:

* **Username:** `admin`
* **Password:** `admin` (bisa diminta ganti saat login pertama)

Setelah login:

1. Tambahkan datasource Prometheus (jika belum otomatis).
2. Import atau buat dashboard sesuai kebutuhan.

Contoh query di Prometheus:

```promql
node_cpu_seconds_total
rate(http_requests_total[5m])
```

---

## Pengembangan

Kamu bisa mengembangkan lebih lanjut dengan:

* Menulis *custom exporter* untuk aplikasi tertentu
* Menambahkan panel baru di Grafana
* Setup alerting dengan Alertmanager
* Men-deploy di server / cloud (misalnya dengan Kubernetes)

---

## Troubleshooting

| Masalah                                  | Solusi                                                                    |
| ---------------------------------------- | ------------------------------------------------------------------------- |
| Docker container tidak jalan             | Cek log dengan `docker-compose logs <nama_service>`                       |
| Grafana tidak bisa connect ke Prometheus | Pastikan URL datasource benar dan container Prometheus sudah berjalan     |
| Metrik tidak muncul                      | Periksa apakah exporter aktif dan sudah ditambahkan di `prometheus.yml`   |
| Port sudah dipakai                       | Ubah port di `docker-compose.yml` atau hentikan service lain yang konflik |

---

## Lisensi

Lisensi mengikuti [MIT License](LICENSE) atau sesuai ketentuan repo ini.

```

Mau saya tambahkan **diagram arsitektur** dalam bentuk ASCII/mermaid supaya README lebih visual, atau cukup tabel saja?
```
