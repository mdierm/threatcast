Penjelasan **perhitungan dan perbedaan angka 32.347 vs 4.890** adalah sebagai berikut:

---

### **1. 32.347 = Jumlah Total Risk Event pada Top 20 Device**

* **32.347** adalah **jumlah seluruh kejadian risk event** (semua flag yang terdeteksi, baik pada device yang sama berulang kali maupun pada device berbeda) yang tercatat pada **20 model device teratas** selama periode monitoring.
* **Cara menghitung:**
  Jumlahkan kolom **Grand Total** pada tabel Top 20 device.
  Nilai Grand Total ini mewakili **jumlah risk event** yang terjadi pada tiap device, termasuk jika satu device terdeteksi beberapa kali di hari yang berbeda atau dalam kondisi flag berbeda.

---

### **2. 4.890 = Jumlah Unique Device (Unique Identifier) pada Top 20 Device**

* **4.890** adalah **jumlah perangkat unik** (unique device ID/app\_user\_id) pada Top 20 model device yang **pernah terdeteksi risk** selama periode monitoring.
* Satu device bisa muncul berkali-kali sebagai risk event (misal: root tetap, device login ulang, flag di hari berbeda), namun **hanya dihitung sekali dalam data unique device**.

---

### **Perbedaan Utama:**

* **32.347** = **Total risk event** (bisa lebih dari satu event pada device yang sama, akumulasi semua kasus/event/flag)
* **4.890** = **Unique device** (hanya menghitung satu kali setiap perangkat, walaupun muncul berkali-kali di event risk)

---

#### **Contoh:**

* Jika **Device A** terdeteksi risk pada 5 hari berbeda, akan dihitung **5 kali** pada Grand Total risk event (**32.347**).
* Namun pada perhitungan unique device, **Device A** tetap hanya dihitung **1 kali** dalam total unique device (**4.890**).

---

### **Kesimpulan:**

* **Angka 32.347** menggambarkan **frekuensi terjadinya ancaman risk** di Top 20 device (banyaknya “kejadian”/event).
* **Angka 4.890** menggambarkan **jumlah perangkat unik yang berisiko** di Top 20 device (banyaknya “identitas device”).

Keduanya sama-sama penting:

* **Event-based** (32.347) untuk melihat beban/pola ancaman (seringnya terjadi).
* **Unique device** (4.890) untuk strategi mitigasi yang efektif (berapa device harus benar-benar diblokir).

---

Jika butuh contoh tabel atau breakdown visual dari perhitungan ini, silakan minta!
