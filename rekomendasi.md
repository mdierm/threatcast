# Laporan Analisa Efektivitas Perbaikan RASP Hardware
_Aplikasi Wondr by BNI – Mei 2025_

---

## 1. Latar Belakang & Tujuan Analisa

Aplikasi Wondr by BNI menghadapi tantangan fraud device berbahaya (root, custom ROM, dan device modifikasi) yang dapat mem-bypass kontrol keamanan.  
Perbaikan melalui implementasi RASP Hardware bertujuan untuk menurunkan risiko fraud, meningkatkan kepercayaan, dan menjaga pertumbuhan digital banking secara berkelanjutan.

---

## 2. Data Utama Hasil Monitoring

| Data                                 | Nilai                   |
|---------------------------------------|-------------------------|
| **User aktif harian**                 | 1.110.000               |
| **Device high risk per hari**         | 6.479 (0,58%)           |
| **Top 20 model device high risk**     | 4.890 (73%)             |
| **607 model device lain**             | 1.833 (27%)             |
| **Total model device**                | 627                     |

---

## 3. Perhitungan Distribusi Threat

- **Persentase device high risk:**  
  \[
  \frac{6.479}{1.110.000} \times 100\% \approx 0,58\%
  \]
- **Kontribusi Top 20 model:**  
  \[
  \frac{4.890}{6.723} \times 100\% \approx 73\%
  \]
- **Kontribusi 607 model lain:**  
  \[
  \frac{1.833}{6.723} \times 100\% \approx 27\%
  \]

---

## 4. Visualisasi Distribusi Threat

```mermaid
pie
    title Distribusi Device High Risk
    "Top 20 High Risk Device (73%)" : 4890
    "607 Device Lain (27%)" : 1833
````

---

## 5. Analisa & Implikasi Bisnis

* **Distribusi threat sangat terkonsentrasi:**

  * 73% device high risk hanya berasal dari 20 model device (3,2% dari total model)
  * 607 model lain (96,8%) hanya menyumbang 27% threat device
* **Implementasi RASP Hardware:**

  * Semua device high risk otomatis diblokir pada onboarding dan akses fitur sensitif
  * 99%+ user legitimate tetap onboarding, login, dan transaksi tanpa hambatan
  * Fraud dan loss finansial turun signifikan, pengalaman user tetap optimal

---

## 6. Kesiapan & Strategi Penanganan False Positive

* Disediakan **mekanisme appeal dan manual whitelist** bagi user legitimate yang terdampak agar tetap bisa difasilitasi cepat.
* **Tim CS dan risk** siap melakukan verifikasi manual dan edukasi agar risk policy tidak merugikan user loyal.
* Monitoring false positive secara periodik untuk evaluasi policy berkelanjutan.

---

## 7. Korelasi dengan Digital Growth & Inovasi

* **User experience mayoritas tetap terjaga:** Enforcement risk device tidak menghambat pertumbuhan user baru maupun adopsi fitur digital.
* **Kebijakan ini mendukung inovasi digital banking yang aman dan berkelanjutan,** serta menjadi nilai tambah dalam promosi keamanan aplikasi ke nasabah.
* **Risiko stagnasi growth dan retensi user sangat minimal.**

---

## 8. Kesimpulan Eksekutif

* **Jumlah device high risk sangat kecil dibandingkan populasi user harian, namun berkontribusi besar pada risiko fraud digital.**
* **Kebijakan sangat targeted dan evidence-based, dampaknya sangat kecil ke mayoritas user.**
* **Perbaikan RASP Hardware sangat layak segera dijalankan demi keamanan, compliance, akselerasi digital growth, dan keberlanjutan bisnis.**
* **Solusi ini menutup risiko fraud device secara efektif tanpa mengorbankan kenyamanan user maupun inovasi bisnis.**

---
