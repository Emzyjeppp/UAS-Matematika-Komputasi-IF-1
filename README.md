# RESUME UAS MATEMATIKA KOMPUTASI (IF-1)
**Sifat:** Close Book (Open 1 Lembar Resume/Double-Sided A4)  
**Tahun Akademik:** Genap 2026  
**Konteks/Pembuat:** Ilham Rais Arvianto  

---

## 1. GRAF EULER & HAMILTON

### A. Definisi Dasar
*   **Lintasan Euler:** Lintasan yang melalui setiap **sisi (edge)** graf tepat satu kali.
*   **Sirkuit Euler:** Sirkuit (lintasan tertutup) yang melalui setiap **sisi (edge)** tepat satu kali.
*   **Graf Euler (Eulerian Graph):** Graf yang memiliki **sirkuit Euler**.
*   **Graf Semi-Euler (Semi-Eulerian Graph):** Graf yang memiliki **lintasan Euler** (tetapi tidak memiliki sirkuit Euler).

### B. Teorema Graf Euler (Tidak Berarah)
1.  **Graf Euler (Sirkuit Euler):** Graf terhubung $G$ memiliki sirkuit Euler jika dan hanya jika **setiap simpul berderajat genap**.
2.  **Graf Semi-Euler (Lintasan Euler):** Graf terhubung $G$ memiliki lintasan Euler jika dan hanya jika **tepat memiliki dua simpul berderajat ganjil** ATAU **tidak ada simpul berderajat ganjil sama sekali** (semua genap).
    *   *Catatan:* Jika ada 2 simpul ganjil, lintasan Euler harus dimulai dari salah satu simpul ganjil dan berakhir di simpul ganjil lainnya.

### C. Teorema Graf Euler (Berarah / Digraph)
Graf berarah $G$ terhubung lemah memiliki:
1.  **Sirkuit Euler:** Jika dan hanya jika untuk setiap simpul $v$, derajat-masuk sama dengan derajat-keluar ($d_{in}(v) = d_{out}(v)$).
2.  **Lintasan Euler:** Jika dan hanya jika untuk setiap simpul derajat-masuk sama dengan derajat-keluar, kecuali dua simpul:
    *   Simpul awal: $d_{out}(u) = d_{in}(u) + 1$
    *   Simpul akhir: $d_{in}(w) = d_{out}(w) + 1$

### D. Rumus & Ketidaksamaan Euler (Graf Planar)
Untuk graf planar sederhana terhubung dengan $n$ simpul, $e$ sisi, dan $f$ wilayah (muka):
1.  **Rumus Euler:** 
    $$n - e + f = 2 \implies f = e - n + 2$$
    *Lemma Jabat Tangan:* $\sum d(v) = 2e \implies e = \frac{\sum d(v)}{2}$
2.  **Ketidaksamaan Euler (Euler Inequality):**
    *   **Rumus Umum** (jika ada sirkuit panjang 3 / segitiga):
        $$e \le 3n - 6 \quad (n \ge 3)$$
    *   **Rumus Khusus** (jika bebas segitiga / tidak ada sirkuit panjang 3, misal graf bipartit seperti $K_{3,3}$):
        $$e \le 2n - 4 \quad (n \ge 3)$$
3.  **Teorema Kuratowski:** Graf bersifat planar jika dan hanya jika ia tidak memuat upagraf yang homeomorfik dengan $K_5$ (graf lengkap 5 simpul) atau $K_{3,3}$ (graf bipartit lengkap 3,3).

---

## 2. SHORTEST PATH (LINTASAN TERPENDEK) & TSP

### A. Algoritma Dijkstra (Lintasan Terpendek)
Digunakan pada graf berbobot positif untuk mencari lintasan terpendek dari simpul asal ($s$) ke semua simpul lainnya.
*   **Variabel:**
    *   $S$: Himpunan simpul yang sudah dikunjungi (terpilih).
    *   $d[v]$: Jarak terpendek sementara dari asal ke simpul $v$.
    *   $p[v]$: Simpul pendahulu (predecessor/parent) dari $v$.
*   **Langkah-langkah Praktis (Tabel):**
    1.  Inisialisasi: Jarak asal $d[s] = 0$, simpul lainnya $d[v] = \infty$. $S = \emptyset$.
    2.  Pilih simpul $u \notin S$ dengan nilai $d[u]$ terkecil. Masukkan $u$ ke dalam $S$ ($S = S \cup \{u\}$).
    3.  Lakukan **relaxing** untuk setiap tetangga $v$ dari $u$ yang belum masuk $S$:
        *   Jika $d[u] + W(u, v) < d[v]$:
            *   Perbarui $d[v] = d[u] + W(u, v)$
            *   Catat predecessor $p[v] = u$
    4.  Ulangi langkah 2 & 3 sampai semua simpul masuk ke $S$.

#### Contoh Tabel Dijkstra (Asal: A)
Misal Graf memiliki simpul A, B, C, D dengan sisi berbobot: A-B (4), A-C (2), C-B (1), B-D (3), C-D (5).

| Iterasi | Simpul Terpilih ($u$) | $S$ | $d[B], p[B]$ | $d[C], p[C]$ | $d[D], p[D]$ |
| :---: | :--- | :--- | :--- | :--- | :--- |
| Inisial | - | $\emptyset$ | $\infty, -$ | $\infty, -$ | $\infty, -$ |
| 1 | A | $\{A\}$ | $4, A$ (via AB) | $2, A$ (via AC) | $\infty, -$ |
| 2 | C (jarak 2) | $\{A, C\}$ | **$3, C$** (karena $2+1 < 4$) | $2, A$ | $7, C$ (via AC-CD) |
| 3 | B (jarak 3) | $\{A, C, B\}$ | $3, C$ | $2, A$ | **$6, B$** (karena $3+3 < 7$) |
| 4 | D (jarak 6) | $\{A, C, B, D\}$| $3, C$ | $2, A$ | $6, B$ |

*Lintasan Terpendek ke D:* $A \to C \to B \to D$ dengan bobot $6$.

### B. TSP vs. CPP
*   **Traveling Salesperson Problem (TSP):** Mencari sirkuit terpendek yang mengunjungi setiap **simpul** tepat satu kali dan kembali ke asal $\implies$ **Sirkuit Hamilton** berbobot minimum.
*   **Chinese Postman Problem (CPP):** Mencari lintasan/sirkuit terpendek yang melewati setiap **sisi (jalan)** paling sedikit sekali dan kembali ke asal $\implies$ Jika graf Euler, bobot = total bobot sisi. Jika bukan Euler, duplikat sisi-sisi berbobot minimal yang menghubungkan simpul-simpul berderajat ganjil.

---

## 3. MINIMUM SPANNING TREE (Pohon Rentang Minimum)

Diberikan graf terhubung berbobot $G$ dengan $n$ simpul. Pohon rentang memiliki $n$ simpul dan $n-1$ sisi tanpa sirkuit. MST adalah pohon rentang dengan total bobot minimal.

### A. Algoritma Prim (Pendekatan Simpul/Vertex-based)
1.  Pilih satu simpul awal secara acak (atau yang ditentukan soal), masukkan ke dalam pohon $T$.
2.  Cari sisi dengan bobot terkecil yang menghubungkan simpul di dalam $T$ dengan simpul di luar $T$, dan tidak membentuk sirkuit.
3.  Masukkan sisi dan simpul baru tersebut ke dalam $T$.
4.  Ulangi langkah 2 & 3 sebanyak $n - 1$ sisi terpilih.

### B. Algoritma Kruskal (Pendekatan Sisi/Edge-based)
1.  Urutkan semua sisi graf berdasarkan bobotnya secara menaik (kecil ke besar).
2.  Pilih sisi dengan bobot terkecil. Masukkan ke dalam $T$ asal tidak membentuk sirkuit.
3.  Ulangi langkah 2 sampai terkumpul tepat $n - 1$ sisi.

#### Contoh Perbandingan Prim & Kruskal
Misalkan graf terhubung dengan simpul A, B, C, D. Sisi diurutkan: AB(1), BC(2), CD(3), AD(4), AC(5).
*   **Kruskal:**
    1. Pilih AB(1). $T = \{AB\}$
    2. Pilih BC(2). $T = \{AB, BC\}$
    3. Pilih CD(3). $T = \{AB, BC, CD\}$ (Sudah 3 sisi, selesai). Total bobot = 6.
*   **Prim (Mulai A):**
    1. Sisi terkoneksi A: AB(1), AD(4), AC(5). Pilih AB(1). $T = \{A, B\}$, sisi $\{AB\}$.
    2. Sisi terkoneksi $T$: BC(2), AD(4), AC(5). Pilih BC(2). $T = \{A, B, C\}$, sisi $\{AB, BC\}$.
    3. Sisi terkoneksi $T$: CD(3), AD(4), AC(5). Pilih CD(3). $T = \{A, B, C, D\}$, sisi $\{AB, BC, CD\}$. Selesai. Total bobot = 6.

---

## 4. POHON m-ary (Banyak Daun & Simpul)

### A. Terminologi
*   **m-ary Tree (atau n-ary):** Pohon berakar yang setiap simpul dalamnya memiliki maksimal $m$ anak.
*   **Full m-ary Tree (Teratur/Penuh):** Setiap simpul dalam memiliki tepat $m$ anak.
*   **Daun (Leaf):** Simpul yang tidak memiliki anak (derajat-keluar = 0).
*   **Simpul Dalam (Internal Node):** Simpul yang memiliki minimal 1 anak.
*   **Tinggi (Height, $h$):** Panjang lintasan terpanjang dari akar ke daun.

### B. Rumus Pohon m-ary Penuh (Full)
1.  **Hubungan Simpul ($n$), Daun ($l$), dan Simpul Dalam ($i$):**
    *   $n = m \cdot i + 1$ (karena setiap simpul kecuali root adalah anak dari suatu simpul).
    *   $n = l + i$
    *   **Mencari Daun ($l$):**
        $$l = (m - 1)i + 1 \quad \implies \quad l = \frac{(m - 1)n + 1}{m}$$
    *   **Mencari Simpul Dalam ($i$):**
        $$i = \frac{l - 1}{m - 1} \quad \implies \quad i = \frac{n - 1}{m}$$
    *   **Mencari Total Simpul ($n$):**
        $$n = \frac{m \cdot l - 1}{m - 1}$$
2.  **Hubungan dengan Tinggi ($h$) pada Pohon m-ary Penuh Teratur:**
    *   **Jumlah Daun Maksimum:** $L = m^h$
    *   **Jumlah Simpul Maksimum:** 
        $$S = \frac{m^{h+1} - 1}{m - 1}$$

### C. Solusi Latihan Soal Slide
#### Latihan 1: Hitung Daun & Simpul jika:
1.  **Pohon 2-ary teratur dengan tinggi $h=3$:**
    *   $m = 2$, $h = 3$.
    *   Jumlah Daun: $L = 2^3 = 8$.
    *   Jumlah Simpul: $S = \frac{2^{3+1}-1}{2-1} = 15$.
2.  **Pohon 3-ary teratur dengan tinggi $h=5$:**
    *   $m = 3$, $h = 5$.
    *   Jumlah Daun: $L = 3^5 = 243$.
    *   Jumlah Simpul: $S = \frac{3^{5+1}-1}{3-1} = \frac{729-1}{2} = 364$.
3.  **Pohon 4-ary teratur dengan tinggi $h=4$:**
    *   $m = 4$, $h = 4$.
    *   Jumlah Daun: $L = 4^4 = 256$.
    *   Jumlah Simpul: $S = \frac{4^{4+1}-1}{4-1} = \frac{1024-1}{3} = 341$.

#### Latihan 2: Hapus semua anak dari salah satu simpul di aras (level) 2.
Aras 2 memiliki $m^2$ simpul. Jika kita menghapus semua anak dari salah satu simpul tersebut:
*   Subpohon di bawah simpul level 2 memiliki tinggi $h - 2$.
*   Banyak simpul di subpohon tersebut: $S_{sub} = \frac{m^{h-1}-1}{m-1}$.
*   Jika dihapus semua anaknya (berarti simpul tersebut tetap ada tapi jadi daun):
    *   **Simpul yang terhapus:** $S_{del} = S_{sub} - 1 = \frac{m^{h-1} - m}{m-1}$.
    *   **Daun yang terhapus:** $L_{del} = m^{h-2}$. Karena simpul level 2 menjadi daun baru (+1), net change daun adalah $-m^{h-2} + 1$.
*   **Hasil Perhitungan Baru:**
    1.  **Untuk 2-ary ($h=3$):**
        *   $S_{new} = 15 - 2 = 13$
        *   $L_{new} = 8 - 2 + 1 = 7$
    2.  **Untuk 3-ary ($h=5$):**
        *   $S_{sub} = \frac{3^4-1}{2} = 40 \implies S_{del} = 39 \implies S_{new} = 364 - 39 = 325$.
        *   $L_{del} = 3^{3} = 27 \implies L_{new} = 243 - 27 + 1 = 217$.
    3.  **Untuk 4-ary ($h=4$):**
        *   $S_{sub} = \frac{4^3-1}{3} = 21 \implies S_{del} = 20 \implies S_{new} = 341 - 20 = 321$.
        *   $L_{del} = 4^{2} = 16 \implies L_{new} = 256 - 16 + 1 = 241$.

#### Latihan 3: Pohon Ternary ($m=3$), $N=131$ simpul. Cari tinggi $k$ dan jumlah daun!
Pohon ini adalah **Pohon Lengkap (Complete)**, bukan penuh teratur (karena $131$ tidak cocok dengan rumus $S = \frac{3^{h+1}-1}{2}$).
*   Untuk complete ternary tree dengan tinggi $k$:
    *   Jumlah simpul level 0 s.d. $k-1$ (terisi penuh) = $\frac{3^k - 1}{2}$.
    *   Batas bawah simpul untuk tinggi $k$: $\frac{3^{k}-1}{2} + 1$
    *   Batas atas simpul untuk tinggi $k$: $\frac{3^{k+1}-1}{2}$
*   Uji nilai $k$:
    *   Jika $k=4$: batas atas = $\frac{3^5-1}{2} = 121$. (Terlalu kecil, $131 > 121$).
    *   Jika $k=5$: batas bawah = $121 + 1 = 122$, batas atas = $\frac{3^6-1}{2} = 364$.
    *   Karena $122 \le 131 \le 364$, maka **tinggi pohon $k = 5$**.
*   **Menghitung Daun ($L$):**
    *   Simpul di aras $0$ s.d. $4$ terisi penuh: $121$ simpul.
    *   Simpul di aras $5$ (daun paling bawah): $131 - 121 = 10$ simpul.
    *   Jumlah parent di aras $4$ yang memiliki anak di aras $5$: $\lceil 10 / 3 \rceil = 4$ parent.
    *   Jumlah simpul aras $4$ yang tidak memiliki anak (menjadi daun): $3^4 - 4 = 81 - 4 = 77$ daun.
    *   Total Daun: $L = 77 + 10 = 87$ daun.
    *   *Verifikasi:* $i = 121 - 81 + 4 = 44$ simpul dalam. $N = i + L = 44 + 87 = 131$ simpul. (Sesuai!).
