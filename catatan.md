jenkins
1. Introduction to CI/CD
Dokumen fokus pada penggunaan Jenkins untuk membangun pipeline CI/CD modern: 

k
Pipeline as Code: Menulis definisi pipeline langsung di file teks (Jenkinsfile) yang dikelola bersama kode sumber.

Declarative vs Scripted:

Declarative: Sintaks terstruktur, mudah dibaca pemula, validasi otomatis.

Scripted: Fleksibel (looping, dynamic stages), cocok untuk logika sangat kompleks.

Shared Libraries: Memusatkan fungsi umum (build, linting, deploy) agar dapat digunakan ulang lintas proyek.

Parallel & Matrix Builds:

Parallel stages: Jalankan beberapa tahap (unit, integration, security scan) bersamaan.

Matrix builds: strategi dengan Kombinasi variabel (OS, versi Java, arsitektur) untuk menguji kompatibilitas.

Credential Management: Penyimpanan aman untuk password, token, SSH key—gunakan scope terbatas dan plugin seperti Vault.

Triggers: Berbagai cara memicu pipeline secara otomatis (SCM polling, webhooks, cron, approval manual, remote triggers).

2. Automating Testing in CI/CD
Menjelaskan pendekatan utama untuk mengotomasi pengujian dalam pipeline: 

Testing Pyramid: Prioritaskan unit test, kemudian integration test, dan sedikit end-to-end test.

Unit Testing:

Isolasi kode terkecil (fungsi/method) menggunakan mock/stub.

Cepat, konsisten, dan otomatis di CI.

Tools populer: JUnit/TestNG (Java), Jest/Mocha (JS), PyTest (Python).

Integration Testing:

Verifikasi kerja sama antar modul (service ↔ database, API ↔ service).

Lebih lambat, tergantung resource eksternal.

Pendekatan: top-down, bottom-up, big-bang, incremental.

Security Testing (biasanya): Static code analysis, dependency scanning, dynamic application security testing—integrasi di pipeline.

3. Deploying to Production
Pembahasan strategi deploy tanpa downtime dan cara rollback cepat: 


Zero Downtime: Aplikasi tetap melayani request meski sedang update.

Canary Deployment:

Rilis versi baru ke sebagian kecil pengguna (misal 5%), pantau log/metric.

Bertahap tingkatkan trafik (20%, 50%, 100%) jika stabil; rollback cepat jika gagal.

Blue-Green Deployment:

Dua environment identik: Blue (v1) & Green (v2).

Deploy & testing di Green, lalu alihkan trafik ke Green secara seketika.

Blue standby untuk rollback instan.

Perbandingan:

Aspek	Canary	Blue-Green
Rollout	Bertahap (%, %)	Sekaligus (100%)
Deteksi risk	Lebih dini pada subset	Risiko saat switch
Infrastruktur	Satu cluster	Dua environment penuh

4. Observability & Incident Management
Langkah-langkah memonitor dan menanggapi insiden production: 


Definisi Insiden: Gangguan layanan (timeout, 500 error, service crash) yang memengaruhi pengguna.

Deteksi & Observability:

Logging: ELK Stack, Loki

Metrics: Prometheus + Grafana

Tracing: Jaeger, OpenTelemetry

Uptime: Uptime Kuma, Pingdom

Alerting & Notification: Threshold alert (CPU >90% selama 5 menit) ke Slack/PagerDuty, channel khusus (#ops-alerts).

Initial Triage:

Cek status pod/container, log error, resource usage.

Mitigasi cepat: rollback, restart pod, scale up, bersihkan disk.

Root Cause Analysis (RCA):

Dokumentasi insiden, review tim, perbarui playbook/SOP, jadikan bahan pembelajaran agar tidak terulang.

