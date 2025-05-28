# Risk Acceptance Criteria (RAC) – Pencegahan Fraud Ganti Device & RASP Hardware

**Aplikasi Wondr by BNI**

---

## 1. Tabel Risk Acceptance Criteria

| Skenario                                            | Tingkat Risiko           | Kebijakan / Policy                              | Monitoring     |
| --------------------------------------------------- | ------------------------ | ----------------------------------------------- | -------------- |
| Tidak ganti device                                  | Acceptable               | Lanjut onboarding/transaksi                     | Monitor        |
| Ganti device ≤2x/24 jam & device lolos RASP         | Acceptable               | Lanjut onboarding/transaksi                     | Monitor        |
| Ganti device ≤2x/24 jam & device high risk (Top 20) | Unacceptable             | Block onboarding/akses, appeal manual whitelist | Audit intensif |
| Ganti device >2x/24 jam                             | Unacceptable             | Block onboarding/akses, audit trail             | Audit intensif |
| Ganti device ≤2x/24 jam, device non-risk, anomali   | Conditionally Acceptable | Allow onboarding, backend alert                 | Monitor lanjut |

---

## 2. Penjelasan Alur Langkah

1. **User mulai onboarding, login, atau transaksi.**
2. **Cek apakah device sama seperti sebelumnya:**

   * Jika **tidak ganti device** → proses lanjut (**Acceptable**)
   * Jika **ganti device** → update counter jumlah ganti device (24 jam)
3. **Jika ganti device >2x dalam 24 jam:**

   * **Block akses/transaksi** (**Unacceptable**)
4. **Jika ganti device ≤2x/24 jam:**

   * **Lakukan RASP Hardware Attestation:**

     * Jika **device termasuk Top 20 risk / flag kritikal**:
       **Block onboarding/akses, appeal hanya manual** (**Unacceptable**)
     * Jika **device lolos RASP**:

       * **Cek anomali lain** (geo, pola transaksi, dll):

         * Jika **ada anomali** → allow onboarding + backend alert (**Conditionally Acceptable**)
         * Jika **tidak ada anomali** → allow onboarding (**Acceptable**)

---

## 3. Flow Diagram (Gambar Visual & Mermaid)

### **Versi Gambar (PNG/SVG)**

Jika markdown Anda **tidak support Mermaid**, gunakan diagram visual seperti ini (bisa digambar manual di Lucidchart, draw\.io, atau tools lain):

```mermaid
flowchart TD
    Start([User onboarding/login/transaksi])
    Start --> Cek{Device sama seperti sebelumnya?}
    Cek -- Ya --> Lanjut[Lanjut onboarding/transaksi]
    Cek -- Tidak --> Cnt[Update counter ganti device (24 jam)]
    Cnt --> MoreThan2{Ganti device >2x/24 jam?}
    MoreThan2 -- Ya --> Block1[Block akses/transaksi]
    MoreThan2 -- Tidak --> RASP[RASP Hardware Attestation]
    RASP --> Risky{Device Top 20 risk/flag kritikal?}
    Risky -- Ya --> Block2[Block onboarding/akses\nAppeal manual]
    Risky -- Tidak --> Anomali{Ada anomali lain?}
    Anomali -- Ya --> Alert[Allow onboarding + backend alert]
    Anomali -- Tidak --> Allow[Lanjut onboarding/transaksi]

```

---

## 4. Narasi Kebijakan

* **Blokir otomatis** berlaku untuk perilaku ganti device berlebihan atau device high risk (Top 20/flag RASP).
* **User legitimate** tetap bisa akses aplikasi tanpa hambatan berarti, appeal hanya untuk device valid (manual).
* Semua proses tercatat sebagai audit trail untuk compliance dan investigasi.

---

> **RAC ini menjamin multilayered defense untuk fraud prevention pada onboarding dan akses aplikasi Wondr.**

---
