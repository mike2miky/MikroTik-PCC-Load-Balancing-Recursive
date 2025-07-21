📚 Panduan Lengkap Penggunaan
🔧 Persiapan Awal
Identifikasi ISP Anda:
Catat nama interface untuk setiap ISP (misal: ether1, ether2, pppoe-out1, dll)
Catat IP gateway dari setiap ISP
Catat kecepatan bandwidth setiap ISP (jika menggunakan bandwidth ratio)
Pastikan Koneksi:
Semua ISP sudah terhubung dan bisa akses internet
Gateway setiap ISP sudah dapat ping
Interface sudah dikonfigurasi dengan IP yang benar
⚙️ Langkah-langkah Konfigurasi
Pilih Jumlah ISP (2-10):
Sesuaikan dengan jumlah koneksi internet yang Anda miliki

Pilih Versi RouterOS:
v6: Untuk RouterOS versi 6.x (menggunakan routing-mark)
v7: Untuk RouterOS versi 7.x (menggunakan routing-table)
Konfigurasi Setiap ISP:
Interface: Nama interface yang terhubung ke ISP (contoh: ether1, pppoe-out1)
Gateway: IP gateway dari ISP tersebut
Fitur Advanced (Opsional):
Recursive ON:
Menggunakan DNS server untuk gateway checking
Lebih stabil untuk deteksi koneksi yang down
Masukkan DNS server yang berbeda untuk setiap ISP
Bandwidth Ratio ON:
Distribusi traffic berdasarkan kecepatan ISP
ISP dengan bandwidth lebih besar akan mendapat traffic lebih banyak
Masukkan bandwidth dalam Mbps untuk setiap ISP
Generate dan Preview:
Klik "Preview Ratio" untuk melihat pembagian traffic (jika menggunakan bandwidth ratio)
Klik "Generate Script" untuk membuat konfigurasi
💻 Implementasi ke MikroTik
Backup Konfigurasi:
/system backup save name=backup-before-pcc
Hapus Konfigurasi Lama (Jika Ada):
/ip firewall mangle remove [find comment~"PCC"]
/ip route remove [find comment~"Load"]
Paste Script:
Copy script yang dihasilkan
Paste ke terminal MikroTik atau WinBox
Tekan Enter untuk menjalankan
Verifikasi:
Cek route: /ip route print
Cek mangle: /ip firewall mangle print
Test koneksi dari client
📋 Tips dan Troubleshooting
Jika koneksi tidak seimbang:
Pastikan semua ISP aktif dan gateway bisa ping
Cek apakah ada rule firewall yang memblokir
Gunakan bandwidth ratio jika ISP memiliki kecepatan berbeda
Jika ISP sering disconnect:
Aktifkan fitur Recursive
Gunakan DNS server yang reliable (1.1.1.1, 8.8.8.8)
Adjust timeout dan interval di gateway checking
Untuk gaming atau streaming:
Buat rule khusus untuk aplikasi tertentu
Gunakan connection marking manual jika diperlukan
Pertimbangkan menggunakan satu ISP khusus untuk aplikasi sensitif
📈 Monitoring dan Maintenance
Monitor Traffic: /tool bandwidth-test
Cek Gateway Status: /ip route print detail
Monitor Connection: /ip firewall connection print
Log Checking: /log print where topics~"route"
⚠️ Catatan Penting:
Selalu backup konfigurasi sebelum implementasi
Uji menyeluruh di environment non-production dulu
Sesuaikan dengan topologi jaringan Anda
Script ini adalah base config, jika ada rule lain di mangle mungkin perlu penyesuaian
Jika butuh jasa menggunakan script ini, bisa hubungi Admin
