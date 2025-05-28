# Risk Acceptance Criteria (RAC) – Pencegahan Fraud Ganti Device & RASP Hardware

**Aplikasi Wondr by BNI**

---

## 1. Tabel Risk Acceptance Criteria

| Skenario                                             | Tingkat Risiko | Penjelasan                                     | Kebijakan / Policy                              | Monitoring/Audit |
| ---------------------------------------------------- | -------------- | ---------------------------------------------- | ----------------------------------------------- | ---------------- |
| Device **tidak ganti**, model bukan Top 20           | Low            | Aman, tidak masuk high risk & tidak anomali    | Lanjut onboarding/transaksi                     | Monitor rutin    |
| Ganti device ≤2x/24 jam, model bukan Top 20          | Low            | Device berganti wajar, model tidak rawan       | Lanjut onboarding/transaksi                     | Monitor rutin    |
| Ganti device ≤2x/24 jam, **model masuk Top 20**      | High           | Model terbukti sering fraud, sesuai Threatcast | Block onboarding/akses, appeal manual whitelist | Audit intensif   |
| Ganti device >2x/24 jam                              | High           | Ganti device berlebihan                        | Block onboarding/akses, audit trail             | Audit intensif   |
| Ganti device ≤2x/24 jam, model bukan Top 20, anomali | Medium         | Device aman, ada pola/geolokasi anomali        | Allow onboarding, backend alert                 | Monitor khusus   |

---

## **Alur Langkah Validasi Device**

1. **User melakukan onboarding/transaksi.**
2. **Cek apakah device yang digunakan sama dengan sebelumnya (device tidak ganti atau ganti):**

   * **Tidak ganti:**

     * Cek apakah model device **masuk Top 20** risk?

       * **Tidak masuk:**
         → **Low Risk**
         → Lanjut onboarding/transaksi (**monitor rutin**)
       * **Masuk:**
         (kasus ini tidak ada di tabel, asumsikan tidak terjadi, atau bisa diberi notasi khusus)
   * **Ganti device:**

     * Hitung jumlah ganti device dalam **24 jam terakhir**
     * Jika **>2x**:
       → **High Risk**
       → **Block** onboarding/akses (**audit intensif**)
     * Jika **≤2x**:

       * Cek apakah **model device masuk Top 20** risk?

         * **Masuk:**
           → **High Risk**
           → **Block** onboarding/akses, appeal manual whitelist (**audit intensif**)
         * **Tidak masuk:**

           * Cek **apakah ada anomali behavior** (geo, pola transaksi, dsb)

             * **Ada anomali:**
               → **Medium Risk**
               → Allow onboarding, backend alert (**monitor khusus**)
             * **Tidak ada anomali:**
               → **Low Risk**
               → Lanjut onboarding/transaksi (**monitor rutin**)

---

## **Flow Diagram (Mermaid)**

```mermaid
flowchart TD
    A([Mulai: User onboarding/transaksi])
    A --> B{Device sama dengan sebelumnya?}
    B -- Yes --> C{Model device masuk Top 20 risk?}
    C -- No --> D[Low Risk: Lanjut onboarding/transaksi (Monitor rutin)]
    C -- Yes --> Z[Tambahan: (Kasus ini tidak ada di tabel, bisa flag High Risk)]
    B -- No --> E[Hitung ganti device dalam 24 jam]
    E --> F{Ganti device >2x/24 jam?}
    F -- Yes --> G[High Risk: Block onboarding/akses (Audit intensif)]
    F -- No --> H{Model device masuk Top 20 risk?}
    H -- Yes --> I[High Risk: Block onboarding/akses, appeal manual whitelist (Audit intensif)]
    H -- No --> J{Ada anomali behavior?}
    J -- Yes --> K[Medium Risk: Allow onboarding, backend alert (Monitor khusus)]
    J -- No --> L[Low Risk: Lanjut onboarding/transaksi (Monitor rutin)]
```

---

### **Penjelasan Flow**

* **Low Risk:**
  User menggunakan device yang sama atau ganti device ≤2x/24 jam, model device bukan Top 20, dan tidak ada anomali.
* **Medium Risk:**
  Device tidak masuk Top 20, ganti device ≤2x/24 jam, **tapi** terdeteksi anomali behavior (misal: geolokasi tidak biasa, pola transaksi janggal).
* **High Risk:**

  * Device model masuk Top 20 risk (berdasarkan Threatcast dataset) meski baru ≤2x ganti device.
  * Atau, ganti device sudah >2x dalam 24 jam (indikasi abuse/fraud).
  * Di kedua skenario, onboarding/akses **diblock** dan harus melalui appeal/manual review.

---

## 4. Narasi Kebijakan

* **Blokir otomatis** berlaku untuk perilaku ganti device berlebihan atau device high risk (Top 20/flag RASP).
* **User legitimate** tetap bisa akses aplikasi tanpa hambatan berarti, appeal hanya untuk device valid (manual).
* Semua proses tercatat sebagai audit trail untuk compliance dan investigasi.

---

> **RAC ini menjamin multilayered defense untuk fraud prevention pada onboarding dan akses aplikasi Wondr.**

---
