### **Resume Analisa dan Rekomendasi Perbaikan RASP Hardware**

1. **Identifikasi Permasalahan oleh Divisi ERM**

   * Divisi Enterprise Risk Management (ERM) melalui thematic review telah menemukan adanya kelemahan deteksi root pada aplikasi Wondr versi 1.3.2.
   * Meskipun aplikasi telah mampu memblokir root tools seperti Magisk Kitsune, perangkat dengan KernelSU masih dapat melakukan root bypass tanpa terdeteksi sistem keamanan yang ada.
   * Kondisi ini menimbulkan risiko fraud, potensi manipulasi data, serta penyalahgunaan fitur digital banking.

2. **Analisa Data dan Justifikasi Perbaikan RASP Hardware**

   * Berdasarkan hasil simulasi backdate yang dilakukan oleh Guardsquare/Threatcast, diperoleh data berikut:

     * Rata-rata user aktif harian: 1.110.000 pengguna.
     * Device high risk yang terdeteksi per hari: 6.479 perangkat (0,58% dari user aktif harian).
     * Dari total 627 model device yang digunakan, Top 20 model device menyumbang 4.890 threat (72,7%), sedangkan 607 model lainnya hanya 1.833 threat (27,3%).
   * Fakta tersebut menunjukkan bahwa meski proporsi perangkat berisiko sangat kecil dibandingkan total pengguna, konsentrasi ancaman sangat tinggi pada kelompok kecil device.
   * Implementasi RASP Hardware dinilai krusial untuk mendeteksi dan melakukan pemblokiran otomatis terhadap perangkat berisiko tinggi (termasuk varian root tools terbaru) tanpa mengganggu kenyamanan mayoritas pengguna.

3. **Risk Acceptance Criteria (RAC) untuk Top Device**

   * Risk Acceptance Criteria (RAC) difokuskan pada pencegahan fraud akibat perpindahan perangkat berulang dan mitigasi pada Top 20 perangkat paling berisiko.
   * Setiap perangkat dalam kelompok Top 20 yang terdeteksi sebagai risk (root/custom ROM/KernelSU) akan secara otomatis diblokir pada proses onboarding dan akses fitur kritikal, dengan peluang appeal melalui whitelist manual bagi user legitimate.
   * RAC mengintegrasikan deteksi teknis melalui RASP Hardware, monitoring perilaku pengguna, serta pencatatan audit untuk memastikan efektivitas kontrol risiko.

4. **Solusi Jangka Panjang: Arsitektur Dua Arah Threatcast & Enforcement Otomatis**

   * Direkomendasikan implementasi arsitektur keamanan dua arah, di mana aplikasi, backend, dan Threatcast saling terintegrasi secara real-time.
   * Setiap event ancaman yang terdeteksi oleh aplikasi atau RASP akan langsung memicu enforcement otomatis (pemblokiran, force logout, atau pembatasan akses) pada backend, dan status risiko perangkat atau pengguna akan tersimpan secara persist di database.
   * Threatcast akan berperan sebagai command center aktif yang dapat meng-update status risiko dan men-trigger tindakan mitigasi secara real-time melalui integrasi API backend.
   * Dengan skema ini, seluruh proses pengendalian risiko menjadi otomatis, berkelanjutan, dan dapat diaudit secara transparan sehingga mendukung keamanan, kepatuhan, serta inovasi layanan digital banking BNI.

---
