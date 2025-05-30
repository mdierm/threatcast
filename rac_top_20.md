# 📋 **Tabel Risk Acceptance Criteria (RAC) Validasi Device Wondr**

| Skenario                                             | Tingkat Risiko | Penjelasan                                       | Kebijakan / Policy                              | Monitoring/Audit |
| ---------------------------------------------------- | -------------- | ------------------------------------------------ | ----------------------------------------------- | ---------------- |
| Device **tidak ganti**, model bukan Top 20           | Low            | Device user tetap, bukan model rawan fraud       | Lanjut onboarding/transaksi                     | Monitor rutin    |
| Ganti device ≤2x/24 jam, model bukan Top 20          | Low            | Device berganti wajar, model tidak rawan         | Lanjut onboarding/transaksi                     | Monitor rutin    |
| Ganti device ≤2x/24 jam, **model masuk Top 20**      | High           | Model terbukti sering fraud (Top 20 Threatcast)  | Block onboarding/akses, appeal manual whitelist | Audit intensif   |
| Ganti device >2x/24 jam                              | High           | Device sering berganti dalam waktu singkat       | Block onboarding/akses, audit trail             | Audit intensif   |
| Ganti device ≤2x/24 jam, model bukan Top 20, anomali | Medium         | Device aman, tapi deteksi pola/geolokasi anomali | Allow onboarding, backend alert                 | Monitor khusus   |

---

# 🔄 **Deskripsi Alur Langkah Validasi**

1. **User melakukan onboarding atau transaksi di aplikasi.**
2. **Cek: Apakah device sama dengan sebelumnya?**

   * **Jika tidak ganti device:**

     * Cek apakah model device termasuk Top 20 risk?

       * **Tidak:**
         ➔ **Low Risk** → Lanjut onboarding/transaksi (monitor rutin)
       * **Ya:**
         *(Opsional, flag High Risk/alert khusus untuk risk aversion maksimal)*
   * **Jika ganti device:**

     * Hitung jumlah ganti device dalam 24 jam terakhir.

       * **Jika >2x/24 jam:**
         ➔ **High Risk** → Block onboarding/akses (audit intensif, audit trail)
       * **Jika ≤2x/24 jam:**

         * Cek apakah model device termasuk Top 20 risk?

           * **Ya:**
             ➔ **High Risk** → Block onboarding/akses, appeal manual whitelist (audit intensif)
           * **Tidak:**

             * Cek anomali behavior (geo, fingerprint, pola transaksi)

               * **Ada anomali:**
                 ➔ **Medium Risk** → Allow onboarding, backend alert (monitor khusus)
               * **Tidak ada anomali:**
                 ➔ **Low Risk** → Lanjut onboarding/transaksi (monitor rutin)

---

# 🗺️ **Flow Diagram (Mermaid)**

```mermaid
flowchart TD
    START([User onboarding/transaksi])
    START --> D1{Device sama?}
    D1 -- Ya --> D2{Model Top 20?}
    D2 -- No --> OK1[Low Risk: Lanjut]
    D2 -- Yes --> HR1[High Risk: Alert]
    D1 -- Tidak --> D3[Hitung ganti device]
    D3 --> D4{Ganti >2x?}
    D4 -- Yes --> HR2[High Risk: Block]
    D4 -- No --> D5{Model Top 20?}
    D5 -- Yes --> HR3[High Risk: Block+Manual]
    D5 -- No --> D6{Anomali?}
    D6 -- Yes --> MR1[Medium Risk: Alert]
    D6 -- No --> OK2[Low Risk: Lanjut]

```

# ✍️ **Narasi Ringkas & Penjelasan Setiap Jalur**

* **Low Risk:**

  * Device tidak ganti **dan** bukan model Top 20 risk
  * Device ganti ≤2x/24 jam **dan** bukan model Top 20 risk **dan** tidak ada anomali
    → **Aksi:** lanjut onboarding/transaksi, monitoring rutin.

* **Medium Risk:**

  * Device ganti ≤2x/24 jam, bukan model Top 20 risk, **tapi** ada anomali behavior
    → **Aksi:** onboarding/transaksi diizinkan, backend alert, monitoring lebih ketat.

* **High Risk:**

  * Device ganti >2x/24 jam
  * Device ganti ≤2x/24 jam, **tapi** model device masuk Top 20 risk
  * *(Opsional: device tidak ganti, model device Top 20 risk)*
    → **Aksi:** block onboarding/akses, audit intensif, appeal manual whitelist jika applicable.

---

# 🚦 **Tabel Reaksi Kebijakan**

| Tingkat Risiko | Aksi Sistem                         | Audit/Monitoring       | Contoh Notifikasi                 |
| -------------- | ----------------------------------- | ---------------------- | --------------------------------- |
| Low            | Lanjut onboarding/transaksi         | Monitor rutin          | -                                 |
| Medium         | Allow onboarding, backend alert     | Monitor khusus         | "Device anomali"                  |
| High           | Block onboarding/akses, audit trail | Audit intensif, manual | "Access blocked, contact support" |

---

# 💡 **Catatan Implementasi**

* Dataset **Top 20 risk** diupdate manual dari Threatcast, disimpan di backend Wondr.
* Proses audit dan monitoring harus terekam jelas untuk compliance.
* Flow siap diotomasi via backend rule engine maupun dijadikan dasar SOP manual.

