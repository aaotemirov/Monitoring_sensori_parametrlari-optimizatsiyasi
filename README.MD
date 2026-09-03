# Monitoring Sensor Parametrlari — Optimallashtirish

**Sensor monitoring parametrlarini tahlil qilish va optimallashtirish uchun yangi usulning Python realizatsiyasi**

[![Python](https://img.shields.io/badge/Python-3.x-blue?logo=python)](https://www.python.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter)](https://jupyter.org/)
[![GitHub](https://img.shields.io/badge/Repository-GitHub-black?logo=github)](https://github.com/)
[![Research Software](https://img.shields.io/badge/Research-Software-green)](https://github.com/)

---

## Annotatsiya

Ushbu repository sensor monitoring tizimlarida kuzatiladigan parametrlarni matematik modellashtirish, parametrlar fazosini tahlil qilish va optimal yechimni aniqlashga mo‘ljallangan optimallashtirish usulining dasturiy realizatsiyasini o‘z ichiga oladi.

Loyihaning asosiy maqsadi — ko‘p parametrli sensor tizimlarida mavjud parametrlar to‘plamidan foydalanib, belgilangan maqsad funksiyasini optimallashtiruvchi yechimni aniqlashdir.

Repository tarkibida optimallashtirish algoritmining Python realizatsiyasi va tadqiqot jarayonini bosqichma-bosqich takrorlash imkonini beruvchi Jupyter Notebook mavjud.

Ushbu repository ilmiy maqolalar, dissertatsiya ishlari, tajribaviy tadqiqotlar va reproduktiv hisoblashlar uchun dasturiy manba sifatida ishlab chiqilgan.

---

# 1. Tadqiqot muammosi

Sensor monitoring tizimlarida bir vaqtning o‘zida bir nechta fizik parametrlar kuzatiladi. Masalan:

* tok;
* kuchlanish;
* quvvat;
* harorat;
* namlik;
* bosim;
* tezlik;
* radiatsiya;
* zaryad holati;
* boshqa tizimga xos parametrlar.

Ushbu parametrlarning qiymatlari vaqt davomida o‘zgaradi va ular o‘zaro bog‘langan bo‘lishi mumkin.

Shuning uchun sensor tizimini matematik jihatdan:

$$
\mathbf{x}(t)=
[x_1(t),x_2(t),\ldots,x_n(t)]^T
$$

parametrlar vektori orqali ifodalash mumkin.

Bu yerda:

* \(x_i(t)\) — \(i\)-parametrning vaqt bo‘yicha qiymati;
* \(n\) — parametrlar soni;
* \(t\) — kuzatish vaqti;
* \(\mathbf{x}(t)\) — tizimning joriy holat vektori.

Ko‘p o‘zgaruvchili optimallashtirish masalalarida yechimni aniqlash uchun maqsad funksiyasi va ruxsat etilgan yechimlar sohasi belgilanadi [1–3].

---

# 2. Matematik model

## 2.1. Sensor parametrlar vektori

Diskret vaqt oralig‘ida sensorlardan olingan ma’lumotlar:

$$
x_i[k]=x_i(t_k)
$$

ko‘rinishida ifodalanadi.

Barcha parametrlar quyidagi vektor orqali ifodalanadi:

$$
\mathbf{x}_k=
\begin{bmatrix}
x_1[k]\\
x_2[k]\\
\vdots\\
x_n[k]
\end{bmatrix}
$$

Kuzatuvlar to‘plami esa:

$$
X=
\begin{bmatrix}
x_1[1] & x_2[1] & \cdots & x_n[1]\\
x_1[2] & x_2[2] & \cdots & x_n[2]\\
\vdots & \vdots & \ddots & \vdots\\
x_1[m] & x_2[m] & \cdots & x_n[m]
\end{bmatrix}
$$

matritsasi orqali ifodalanadi.

Bu yerda \(m\) — kuzatuvlar soni.

---

# 3. Ma’lumotlarni normallashtirish

Sensorlar turli fizik birliklarda ishlashi sababli parametrlarning qiymat diapazonlari bir-biridan sezilarli darajada farq qilishi mumkin.

Shuning uchun optimallashtirishdan oldin parametrlarni umumiy diapazonga keltirish mumkin.

Min-max normallashtirish:

$$
x_i^{norm}=
\frac{x_i-x_i^{min}}
{x_i^{max}-x_i^{min}}
$$

orqali amalga oshiriladi.

Natijada:

$$
0\leq x_i^{norm}\leq1
$$

sharti hosil bo‘ladi.

Normallashtirish optimallashtirish jarayonida parametrlar masshtabining ta’sirini kamaytirishga yordam beradi [2,3].

---

# 4. Optimallashtirish masalasining matematik qo‘yilishi

Umumiy optimallashtirish masalasi:

$$
\boxed{
\mathbf{x}^{*}
=
\arg\min_{\mathbf{x}\in\Omega}F(\mathbf{x})
}
$$

ko‘rinishida ifodalanadi.

Bu yerda:

* \(F(\mathbf{x})\) — maqsad funksiyasi;
* \(\mathbf{x}\) — optimallashtiriluvchi parametrlar vektori;
* \(\mathbf{x}^{*}\) — optimal yechim;
* \(\Omega\) — ruxsat etilgan yechimlar sohasi.

Agar masala maksimumni aniqlashga qaratilgan bo‘lsa:

$$
\boxed{
\mathbf{x}^{*}
=
\arg\max_{\mathbf{x}\in\Omega}F(\mathbf{x})
}
$$

ko‘rinishidan foydalaniladi.

---

# 5. Maqsad funksiyasi

Sensor monitoring tizimi uchun maqsad funksiyasi tizimning optimallashtirilishi kerak bo‘lgan mezonini ifodalaydi.

Umumiy holda:

$$
F(\mathbf{x})=
F(x_1,x_2,\ldots,x_n)
$$

deb olinadi.

Bir nechta mezon mavjud bo‘lsa, ko‘p mezonli optimallashtirish modeli:

$$
\mathbf{F}(\mathbf{x})=
\left[
F_1(\mathbf{x}),
F_2(\mathbf{x}),
\ldots,
F_r(\mathbf{x})
\right]^T
$$

ko‘rinishida yoziladi.

Ko‘p mezonli masalani yagona maqsad funksiyasiga keltirish uchun vaznli yig‘indi ishlatilishi mumkin:

$$
F(\mathbf{x})
=
\sum_{j=1}^{r}
w_jF_j(\mathbf{x})
$$

bu yerda:

$$
w_j\geq0,
\qquad
\sum_{j=1}^{r}w_j=1.
$$

Bunday yondashuv ko‘p mezonli optimallashtirish masalalarini yagona skalyar maqsad funksiyasi orqali yechishga imkon beradi [2,3].

---

# 6. Cheklovlar

Sensor parametrlarining fizik chegaralari mavjud bo‘lishi mumkin:

$$
x_i^{min}\leq x_i\leq x_i^{max},
\qquad i=1,\ldots,n.
$$

Umumiy cheklovli optimallashtirish masalasi:

$$
\min_{\mathbf{x}}F(\mathbf{x})
$$

quyidagi shartlarda:

$$
g_j(\mathbf{x})\leq0,
\qquad j=1,\ldots,p,
$$

$$
h_l(\mathbf{x})=0,
\qquad l=1,\ldots,q,
$$

$$
\mathbf{x}^{min}\leq
\mathbf{x}
\leq
\mathbf{x}^{max}.
$$

Bu yerda:

* \(g_j(\mathbf{x})\) — tengsizlik cheklovlari;
* \(h_l(\mathbf{x})\) — tenglik cheklovlari;
* \(\mathbf{x}^{min}\), \(\mathbf{x}^{max}\) — parametrlarning fizik chegaralari.

Cheklovlarning mavjudligi optimal yechimning faqat fizik va matematik jihatdan ruxsat etilgan sohada izlanishini ta’minlaydi [1–3].

---

# 7. Yangi optimallashtirish usulining matematik apparati

Taklif etilayotgan usul iteratsion optimallashtirish jarayoni sifatida qaraladi.

Boshlang‘ich yechim:

$$
\mathbf{x}^{(0)}
$$

orqali belgilanadi.

Har bir \(t\)-iteratsiyada yangi yechim:

$$
\boxed{
\mathbf{x}^{(t+1)}
=
\mathcal{T}
\left(
\mathbf{x}^{(t)},
F(\mathbf{x}^{(t)}),
\boldsymbol{\theta}^{(t)}
\right)
}
$$

ko‘rinishida shakllantiriladi.

Bu yerda:

* \(t\) — iteratsiya raqami;
* \(\mathbf{x}^{(t)}\) — joriy yechim;
* \(\mathbf{x}^{(t+1)}\) — yangi yechim;
* \(F(\mathbf{x}^{(t)})\) — joriy maqsad funksiyasi;
* \(\mathcal{T}\) — optimallashtirishning yangilash operatori;
* \(\boldsymbol{\theta}^{(t)}\) — algoritm parametrlarining joriy qiymatlari.

Ushbu operator aynan mazkur repositoryda amalga oshirilgan yangi usulning asosiy matematik qismini tashkil etadi.

---

# 8. Yechimni baholash

Har bir yangi yechim uchun maqsad funksiyasi hisoblanadi:

$$
F_t=F(\mathbf{x}^{(t)}).
$$

Agar minimallashtirish masalasi qaralayotgan bo‘lsa, yangi yechim avvalgi yechimdan yaxshi bo‘lganda:

$$
F_{t+1}<F_t
$$

sharti bajariladi.

Shuningdek, eng yaxshi topilgan yechim:

$$
F_{best}^{(t)}
=
\min_{0\leq k\leq t}
F(\mathbf{x}^{(k)})
$$

orqali saqlanishi mumkin.

Maksimallashtirish holatida esa:

$$
F_{best}^{(t)}
=
\max_{0\leq k\leq t}
F(\mathbf{x}^{(k)}).
$$

---

# 9. Konvergentsiya mezoni

Algoritmning konvergentsiyasi maqsad funksiyasining ketma-ket qiymatlari o‘zgarishi orqali baholanishi mumkin:

$$
\Delta F_t
=
\left|
F(\mathbf{x}^{(t+1)})
-
F(\mathbf{x}^{(t)})
\right|.
$$

Agar:

$$
\Delta F_t<\varepsilon
$$

bo‘lsa, algoritm yetarli aniqlikka erishgan deb qaralishi mumkin.

Bundan tashqari, parametrlar vektorining o‘zgarishi:

$$
\Delta x_t
=
\left\|
\mathbf{x}^{(t+1)}
-
\mathbf{x}^{(t)}
\right\|
$$

orqali ham nazorat qilinadi.

To‘xtash sharti:

$$
\boxed{
\left\|
\mathbf{x}^{(t+1)}
-
\mathbf{x}^{(t)}
\right\|
<\varepsilon
}
$$

ko‘rinishida berilishi mumkin.

---

# 10. Algoritmning umumiy matematik ketma-ketligi

Optimallashtirish jarayonini quyidagicha ifodalash mumkin:

$$
\boxed{
\mathbf{x}^{(0)}
\rightarrow
F(\mathbf{x}^{(0)})
\rightarrow
\mathcal{T}
\rightarrow
\mathbf{x}^{(1)}
\rightarrow
F(\mathbf{x}^{(1)})
\rightarrow
\mathcal{T}
\rightarrow
\cdots
\rightarrow
\mathbf{x}^{*}
}
$$

Algoritmning umumiy pseudokodi:

```text
1. Boshlang‘ich parametrlarni aniqlash
2. Boshlang‘ich yechim x(0) ni shakllantirish
3. Maqsad funksiyasini hisoblash
4. t = 0, 1, ..., T uchun:
       4.1. Yangi yechimni shakllantirish
       4.2. Cheklovlarni tekshirish
       4.3. Maqsad funksiyasini hisoblash
       4.4. Eng yaxshi yechimni yangilash
       4.5. Konvergentsiya shartini tekshirish
5. Optimal yechim x* ni qaytarish
```

---

# 11. Sensor parametrlarini optimallashtirish

Sensor tizimida optimallashtiriluvchi parametrlar:

$$
\mathbf{x}
=
[x_1,x_2,\ldots,x_n]^T
$$

bo‘lib, har bir parametrning fizik chegarasi mavjud:

$$
x_i\in[x_i^{min},x_i^{max}].
$$

Shunday qilib, sensor parametrlarini optimallashtirish masalasi:

$$
\boxed{
\min_{\mathbf{x}}
F(x_1,x_2,\ldots,x_n)
}
$$

quyidagi shartlarda:

$$
x_i^{min}\leq x_i\leq x_i^{max}.
$$

Agar sensorlarning o‘zaro bog‘liqligi mavjud bo‘lsa, qo‘shimcha:

$$
g_j(\mathbf{x})\leq0
$$

cheklovlari ham kiritiladi.

Natijada optimal parametrlar:

$$
\mathbf{x}^{*}
=
[x_1^{*},x_2^{*},\ldots,x_n^{*}]^T
$$

ko‘rinishida aniqlanadi.

---

# 12. Algoritm samaradorligini baholash

Yangi optimallashtirish usulini mavjud usullar bilan taqqoslash uchun bir nechta mezonlardan foydalanish mumkin.

## 12.1. Optimal qiymat

$$
F^{*}=F(\mathbf{x}^{*})
$$

optimal yechim sifatini ifodalaydi.

## 12.2. Hisoblash vaqti

$$
T_{comp}
=
t_{end}-t_{start}
$$

algoritmning hisoblash tezligini baholaydi.

## 12.3. Iteratsiyalar soni

$$
N_{iter}=T
$$

algoritmning optimal yechimga erishish uchun qancha iteratsiya talab qilganini ko‘rsatadi.

## 12.4. Yaxshilanish koeffitsienti

Boshlang‘ich va optimal qiymatlar asosida:

$$
I=
\frac{|F_{initial}-F_{best}|}
{|F_{initial}|}
\times100\%
$$

ko‘rsatkichi orqali yaxshilanish darajasini baholash mumkin.

## 12.5. Takroriy tajribalar

Stoxastik yoki boshlang‘ich holatga bog‘liq algoritmlar uchun tajriba \(R\) marta takrorlanib:

$$
\bar{F}
=
\frac{1}{R}
\sum_{r=1}^{R}F_r
$$

o‘rtacha qiymati hisoblanishi mumkin.

Standart og‘ish:

$$
\sigma_F
=
\sqrt{
\frac{1}{R-1}
\sum_{r=1}^{R}
(F_r-\bar{F})^2
}
$$

algoritmning barqarorligini baholashga yordam beradi.

---

# 13. Hisoblash murakkabligi

Algoritmning hisoblash murakkabligi parametrlar soni \(n\), iteratsiyalar soni \(T\) va maqsad funksiyasini hisoblash murakkabligiga bog‘liq.

Agar bitta iteratsiyada maqsad funksiyasini hisoblash:

$$
O(n)
$$

bo‘lsa, umumiy hisoblash murakkabligi taxminan:

$$
O(Tn)
$$

ko‘rinishida bo‘ladi.

Agar maqsad funksiyasining hisoblash murakkabligi:

$$
C_F(n)
$$

bo‘lsa, umumiy murakkablik:

$$
O(T\cdot C_F(n))
$$

orqali ifodalanadi.

Aniq murakkablik yangi usulning yangilash operatori va maqsad funksiyasining real implementatsiyasiga bog‘liq.

---

# 14. Tadqiqotning hisoblash arxitekturasi

Repositorydagi hisoblash jarayoni:

```text
┌─────────────────────────────┐
│ Sensor monitoring ma'lumotlari│
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│ Ma'lumotlarni tayyorlash    │
│ va normallashtirish         │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│ Matematik optimallashtirish │
│ modeli                      │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│ Yangi optimallashtirish     │
│ usuli                       │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│ Maqsad funksiyasini         │
│ baholash                    │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│ Konvergentsiyani tekshirish │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│ Optimal yechim              │
└─────────────────────────────┘
```

---

# 15. Repository tarkibi

```text
Monitoring_sensori_parametrlari-optimizatsiyasi/
│
├── NewMethodOptimizer.ipynb
├── newmethodoptimizer.py
├── README.md
└── .gitignore
```

### `NewMethodOptimizer.ipynb`

Tadqiqot tajribalarini Jupyter Notebook muhitida bajarish, parametrlarni o‘zgartirish, hisoblash natijalarini kuzatish va algoritm ishini tahlil qilish uchun foydalaniladi.

### `newmethodoptimizer.py`

Optimallashtirish usulining Python dasturiy realizatsiyasini o‘z ichiga oladi.

### `README.md`

Loyihaning ilmiy, matematik va dasturiy tavsifini beradi.

---

# 16. O‘rnatish

Repositoryni klonlash:

```bash
git clone https://github.com/aaotemirov/Monitoring_sensori_parametrlari-optimizatsiyasi.git
```

Loyiha katalogiga o‘tish:

```bash
cd Monitoring_sensori_parametrlari-optimizatsiyasi
```

Virtual muhit yaratish:

```bash
python -m venv venv
```

Virtual muhitni faollashtirish:

### Windows

```powershell
venv\Scripts\activate
```

### Linux/macOS

```bash
source venv/bin/activate
```

Zarur kutubxonalarni o‘rnatish:

```bash
pip install numpy matplotlib jupyter
```

---

# 17. Ishga tushirish

Jupyter Notebook:

```bash
jupyter notebook
```

So‘ng:

```text
NewMethodOptimizer.ipynb
```

fayli ochiladi.

Python realizatsiyasini ishga tushirish:

```bash
python newmethodoptimizer.py
```

---

# 18. Reproduktiv tadqiqot

Ilmiy natijalarni takrorlash uchun:

1. Repositoryning kerakli versiyasi olinadi.
2. Python virtual muhiti yaratiladi.
3. Zarur kutubxonalar o‘rnatiladi.
4. `NewMethodOptimizer.ipynb` ishga tushiriladi.
5. Algoritm parametrlari belgilanadi.
6. Optimallashtirish jarayoni bajariladi.
7. Optimal yechim olinadi.
8. Natijalar boshqa usullar bilan taqqoslanadi.

Tadqiqotning muayyan natijalarini maqolada ko‘rsatishda foydalanilgan repository versiyasi yoki Git tagini qayd etish tavsiya etiladi.

---

# 19. Ilmiy maqolalarda foydalanish

Ushbu repository ilmiy maqolalarda quyidagi maqsadlarda dasturiy manba sifatida ko‘rsatilishi mumkin:

* sensor parametrlarini optimallashtirish;
* optimallashtirish algoritmlarini tajribaviy taqqoslash;
* yangi algoritmning dasturiy realizatsiyasini ko‘rsatish;
* hisoblash tajribalarini reproduksiya qilish;
* dissertatsiya tadqiqotining dasturiy komponentini hujjatlashtirish.

Maqolada repositoryga quyidagicha murojaat qilish mumkin:

> The implementation of the proposed sensor-parameter optimization approach is publicly available in the GitHub repository [4].

yoki:

> The source code and computational experiments used in this study are available in the accompanying research software repository [4].

---

# 20. Citation

Agar ushbu repositorydagi kod, algoritm realizatsiyasi yoki hisoblash tajribalari ilmiy maqola, konferensiya materiali yoki dissertatsiyada ishlatilsa, repositoryga citation berish tavsiya etiladi.

### APA

Temirov, A. (2026). *Monitoring Sensor Parametrlari — Optimallashtirish* [Computer software]. GitHub.

### BibTeX

```bibtex
@software{temirov2026sensor_optimization,
  author       = {Temirov, Azizbek},
  title        = {Monitoring Sensor Parametrlari -- Optimallashtirish},
  year         = {2026},
  publisher    = {GitHub},
  url          = {https://github.com/aaotemirov/Monitoring_sensori_parametrlari-optimizatsiyasi},
  version      = {1.0.0}
}
```

---

# 21. Ilmiy adabiyotlar

Optimallashtirishning matematik asoslari va algoritmik yondashuvlarini yorituvchi asosiy manbalar:

**[1]** Nocedal, J., & Wright, S. J. (2006). *Numerical Optimization* (2nd ed.). Springer.

**[2]** Boyd, S., & Vandenberghe, L. (2004). *Convex Optimization*. Cambridge University Press.

**[3]** Bertsekas, D. P. (1999). *Nonlinear Programming* (2nd ed.). Athena Scientific.

**[4]** Temirov, A. (2026). *Monitoring Sensor Parametrlari — Optimallashtirish*. GitHub repository.

---

# 22. BibTeX — asosiy adabiyotlar

```bibtex
@book{nocedal2006numerical,
  title     = {Numerical Optimization},
  author    = {Nocedal, Jorge and Wright, Stephen J.},
  edition   = {2},
  year      = {2006},
  publisher = {Springer}
}

@book{boyd2004convex,
  title     = {Convex Optimization},
  author    = {Boyd, Stephen and Vandenberghe, Lieven},
  year      = {2004},
  publisher = {Cambridge University Press}
}

@book{bertsekas1999nonlinear,
  title     = {Nonlinear Programming},
  author    = {Bertsekas, Dimitri P.},
  edition   = {2},
  year      = {1999},
  publisher = {Athena Scientific}
}

@software{temirov2026sensor_optimization,
  author    = {Temirov, Azizbek},
  title     = {Monitoring Sensor Parametrlari -- Optimallashtirish},
  year      = {2026},
  publisher = {GitHub},
  url       = {https://github.com/aaotemirov/Monitoring_sensori_parametrlari-optimizatsiyasi},
  version   = {1.0.0}
}
```

---

# 23. DOI va ilmiy identifikatsiya

Repositoryning ilmiy maqolalarda uzoq muddatli va barqaror citation qilinishini ta’minlash uchun GitHub repositoryning relizlarini DOI bilan arxivlash tavsiya etiladi.

Tavsiya etiladigan versiyalash:

```bash
git tag v1.0.0
git push origin v1.0.0
```

Keyingi muhim versiyalar:

```text
v1.1.0
v1.2.0
v2.0.0
```

ko‘rinishida belgilanadi.

DOI mavjud bo‘lgandan keyin BibTeX yozuvi DOI bilan yangilanadi:

```bibtex
@software{temirov2026sensor_optimization,
  author    = {Temirov, Azizbek},
  title     = {Monitoring Sensor Parametrlari -- Optimallashtirish},
  year      = {2026},
  version   = {1.0.0},
  publisher = {Zenodo},
  doi       = {DOI}
}
```

**Eslatma:** DOI haqiqatan yaratilmaguncha README yoki maqolaga soxta DOI kiritilmasligi kerak.

---

# 24. Versiyalash va ilmiy reproduktivlik

Har bir ilmiy tajriba uchun ishlatilgan algoritm versiyasini qayd qilish tavsiya etiladi.

Masalan:

```text
Algorithm version: v1.0.0
Repository: Monitoring_sensori_parametrlari-optimizatsiyasi
Year: 2026
```

Bu yondashuv maqolada keltirilgan natijalarni keyinchalik aynan qaysi dasturiy versiya yordamida olinganini aniqlash imkonini beradi.

---

# 25. Muallif

**Azizbek Temirov**

Research / Dissertation Project

GitHub:

https://github.com/aaotemirov

---

# 26. Litsenziya

Ushbu repository ilmiy-tadqiqot va ta’lim maqsadlarida foydalanish uchun taqdim etilgan.

Koddan ilmiy ishda foydalanilganda repository va tegishli ilmiy manbalarga citation berish tavsiya etiladi.

---

# 27. Repository

GitHub:

https://github.com/aaotemirov/Monitoring_sensori_parametrlari-optimizatsiyasi

**Project:** Monitoring Sensor Parametrlari — Optimallashtirish

**Author:** Azizbek Temirov

**Year:** 2026
