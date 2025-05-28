### **Resume Analisa dan Rekomendasi Perbaikan RASP Hardware**

1. **Temuan Divisi ERM**
   Divisi Enterprise Risk Management (ERM) menemukan adanya kelemahan pada deteksi root pada aplikasi Wondr versi 1.3.2.
   Walaupun aplikasi telah dapat memblokir root tools seperti Magisk Kitsune, perangkat dengan KernelSU masih dapat melakukan root bypass tanpa terdeteksi oleh sistem keamanan saat ini.

2. **Perhitungan dan Usulan Perbaikan RASP Hardware**
   Hasil simulasi backdate Guardsquare/Threatcast terhadap traffic riil aplikasi menunjukkan:

   * User aktif harian rata-rata: 1.110.000
   * Device high risk terdeteksi per hari: 6.479 (0,58% dari user aktif)
   * Top 20 model device menyumbang 4.890 threat (72,7%)
   * 607 model device lain menyumbang 1.833 threat (27,3%)
     Data ini menegaskan pentingnya implementasi RASP Hardware untuk mendeteksi dan memblokir device high risk—including varian root tools terbaru—tanpa mengganggu >99% pengguna legitimate.

3. **Risk Acceptance Criteria (RAC) pada Top Device**
   RAC difokuskan pada mitigasi fraud akibat perpindahan perangkat tidak wajar dan pada Top 20 model device berisiko tinggi.

   * Device pada Top 20 yang terdeteksi risk (root/custom ROM/KernelSU) akan diblokir onboarding/akses secara otomatis.
   * Appeal hanya dapat dilakukan melalui proses whitelist manual bagi user legitimate.
   * RAC menggabungkan deteksi teknis (RASP Hardware), monitoring perilaku, dan proses audit.

4. **Solusi Jangka Panjang: Integrasi Dua Arah Threatcast dan Enforcement Otomatis**
   Direkomendasikan pengembangan arsitektur keamanan dua arah, di mana event ancaman dari aplikasi atau RASP secara otomatis memicu enforcement pada backend,
   status risiko perangkat/pengguna disimpan secara permanen,
   dan Threatcast berperan sebagai command center aktif yang dapat men-trigger tindakan mitigasi real-time.
   Arsitektur ini memastikan setiap ancaman ditangani otomatis, persisten, dan dapat diaudit—menjamin keamanan aplikasi, kepatuhan, serta akselerasi inovasi digital banking BNI.

