# Penerapan Turing Machine: The Busy Beaver Problem

---

## Pengantar
**The Busy Beaver Problem** adalah masalah menarik dalam ilmu komputer teoretis yang berhubungan erat dengan **Turing Machine (Mesin Turing)**. Diperkenalkan oleh Tibor Rado pada tahun 1962, masalah ini menyelami batas-batas komputasi, memberikan wawasan mendalam tentang algoritma, dan konsep **ketidakmampuan untuk memutuskan (undecidability)**.

---

## The Busy Beaver Problem
The Busy Beaver Problem berfokus pada pencarian Mesin Turing paling "sibuk" atau "produktif" untuk sejumlah keadaan (state) tertentu. Secara spesifik, masalah ini mencari Mesin Turing dengan $n$ state yang:
1.  **Berhenti (halt)** setelah sejumlah langkah.
2.  Mencetak **jumlah simbol '1' terbanyak** pada pita (tape) awal yang kosong, sebelum berhenti.

Mesin Turing yang memenuhi kriteria ini disebut **Busy Beaver** untuk $n$ state tersebut.

### Premis Dasar dan Konsep
Untuk memahami The Busy Beaver Problem, kita perlu memahami dasar Mesin Turing:
* **Pita (Tape):** Pita tak terbatas yang terbagi menjadi sel, berisi simbol '0' (kosong) atau '1'.
* **Kepala Baca/Tulis (Read/Write Head):** Membaca/menulis simbol dan bergerak ke kiri/kanan.
* **Keadaan (State):** Kondisi internal Mesin Turing (contoh: A, B, C, ...). Ada juga **keadaan berhenti (Halt State)**.
* **Fungsi Transisi:** Aturan `(state_saat_ini, simbol_dibaca) -> (simbol_ditulis, arah_gerak, state_berikutnya)`.

Tujuan The Busy Beaver Problem adalah menemukan dua nilai untuk setiap $n$:
1.  $\Sigma(n)$: Jumlah maksimum simbol '1' yang dicetak.
2.  $S(n)$: Jumlah maksimum langkah yang diambil.

$\Sigma(n)$ dikenal sebagai **fungsi Busy Beaver**. Ini seperti kompetisi di mana mesin yang berhenti dengan '1' terbanyak adalah pemenangnya.

---

## Contoh dan Implementasi Pemenang (hingga 3 State)

Menemukan Busy Beaver sangat sulit karena jumlah kemungkinan Mesin Turing meningkat secara eksponensial. Ini juga terkait dengan **halting problem** (masalah berhenti) yang tidak dapat diputuskan.

* `0`: Sel kosong
* `1`: Sel berisi '1'
* `R`: Gerak ke kanan
* `L`: Gerak ke kiri
* `A, B, C`: State kerja
* `H`: State Berhenti

### Busy Beaver untuk $n=1$ State
Mesin Turing 1-state hanya punya satu state kerja (A) dan satu state berhenti (H).

**Tabel Transisi:**

| Keadaan Saat Ini | Simbol Dibaca | Simbol Ditulis | Arah Gerak | Keadaan Berikutnya |
| :--------------: | :------------: | :-------------: | :----------: | :----------------: |
|        A         |       0        |        1        |      R       |          H         |
|        A         |       1        |        1        |      R       |          H         |

**Hasil:**
* $\Sigma(1) = 1$
* $S(1) = 1$

### Busy Beaver untuk $n=2$ States
Mesin Turing 2-state memiliki dua state kerja (A, B) dan satu state berhenti (H).

**Tabel Transisi (Pemenang):**

| Keadaan Saat Ini | Simbol Dibaca | Simbol Ditulis | Arah Gerak | Keadaan Berikutnya |
| :--------------: | :------------: | :-------------: | :----------: | :----------------: |
|        A         |       0        |        1        |      R       |          B         |
|        A         |       1        |        1        |      L       |          A         |
|        B         |       0        |        1        |      L       |          A         |
|        B         |       1        |        1        |      R       |          H         |

**Hasil:**
* $\Sigma(2) = 4$
* $S(2) = 6$

*(Catatan: Simulasi detail untuk 2-state ini cukup panjang. Pemenang 2-state yang paling terkenal menghasilkan 4 '1' dalam 6 langkah. Perlu diverifikasi ulang jika ingin menambahkan simulasi langkah demi langkah.)*

### Busy Beaver untuk $n=3$ States
Mesin Turing 3-state memiliki tiga state kerja (A, B, C) dan satu state berhenti (H).

**Tabel Transisi (Pemenang):**

| Keadaan Saat Ini | Simbol Dibaca | Simbol Ditulis | Arah Gerak | Keadaan Berikutnya |
| :--------------: | :------------: | :-------------: | :----------: | :----------------: |
|        A         |       0        |        1        |      R       |          B         |
|        A         |       1        |        1        |      L       |          B         |
|        B         |       0        |        1        |      L       |          A         |
|        B         |       1        |        1        |      L       |          C         |
|        C         |       0        |        1        |      R       |          H         |
|        C         |       1        |        0        |      R       |          A         |

**Hasil:**
* $\Sigma(3) = 6$
* $S(3) = 21$

*(Simulasi untuk 3-state sangat kompleks dan panjang untuk ditulis secara detail di sini.)*

Nilai $\Sigma(n)$ dan $S(n)$ tumbuh sangat cepat dan bersifat **tidak rekursif**, artinya tidak ada algoritma umum untuk menghitungnya untuk semua $n$. Untuk $n \ge 4$, nilai-nilai ini sebagian besar masih menjadi subjek penelitian.

---

## Ilustrasi
Berikut adalah beberapa ilustrasi untuk memperjelas konsep:

### Diagram State Mesin Turing (Contoh: 2 State)
```mermaid
graph TD
    A[State A] -->|0/1, R| B(State B)
    A -->|1/1, L| A
    B -->|0/1, L| A
    B -->|1/1, H| H((Halt))
