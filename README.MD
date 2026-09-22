# Hall Effectli Havo Oralig‘idagi Tok Sensorini Optimallashtirish
## Loyiha haqida
Ushbu loyiha **Hall effectli, havo oralig‘iga ega tok sensorining parametrlarini optimallashtirish** uchun ishlab chiqilgan matematik va dasturiy modelni ifodalaydi.

Loyihaning asosiy maqsadi — turli qiymatlardagi birlamchi tok uchun sensorning chiqish kuchlanishini belgilangan qiymatga, ya'ni **5 V** ga moslashtirish hamda buning uchun sensorning asosiy konstruktiv va elektromagnit parametrlarini optimal tanlashdir.

Loyihada quyidagi asosiy parametrlar o‘rganiladi:

- birlamchi tok — `I`;
- o‘ramlar soni — `w`;
- magnit o‘zakning ko‘ndalang kesim yuzasi — `S`;
- havo oralig‘i — `c`;
- magnit o‘tkazuvchanlik — `μ`;
- magnit o‘zak uzunligi — `l`;
- chastota — `f`;
- chiqish kuchlanishi — `U`.

Optimallashtirish natijasida har bir tok qiymati uchun mos keluvchi **optimal o‘ramlar soni, ko‘ndalang kesim yuzasi va havo oralig‘i** aniqlanadi.

---

# 1. Tadqiqotning maqsadi

Loyihaning asosiy maqsadi Hall effectli/havo oralig‘idagi tok sensorining parametrlarini o‘lchanayotgan tokka bog‘liq holda optimallashtirishdan iborat.

Asosiy masala quyidagicha ifodalanadi:

\[
I \rightarrow \{w,S,c\} \rightarrow U
\]

ya'ni berilgan tok qiymati uchun:

- o‘ramlar soni `w`;
- ko‘ndalang kesim yuzasi `S`;
- havo oralig‘i `c`

parametrlari tanlanadi va natijada chiqish kuchlanishi `U` aniqlanadi.

Optimallashtirishning asosiy maqsadi:

\[
U \rightarrow U_{target}
\]

bu yerda:

\[
U_{target}=5V
\]

---

# 2. Sensorning matematik modeli

Loyihada chiqish kuchlanishini hisoblash uchun quyidagi matematik ifodadan foydalaniladi:

\[
U_{E2} =
\frac{4.44 f I w \mu \mu_0 S}
{l+\mu c}
\]

bu yerda:

| Belgilanish | Nomi | Birligi |
|---|---|---|
| \(U_{E2}\) | Chiqish kuchlanishi | V |
| \(f\) | Chastota | Hz |
| \(I\) | Birlamchi tok | A |
| \(w\) | O‘ramlar soni | dona |
| \(\mu\) | Nisbiy magnit o‘tkazuvchanlik | — |
| \(\mu_0\) | Vakuum magnit o‘tkazuvchanligi | H/m |
| \(S\) | Magnit o‘zakning ko‘ndalang kesim yuzasi | m² |
| \(l\) | Magnit o‘zak uzunligi | m |
| \(c\) | Havo oralig‘i | m |

Vakuum magnit o‘tkazuvchanligi:

\[
\mu_0=4\pi\times10^{-7}\;H/m
\]

Dasturda:

python
m_0 = 4 * np.pi * 1e-7

ko‘rinishida berilgan.

3. Dasturdagi boshlang‘ich parametrlar

Asosiy hisoblash modelida quyidagi qiymatlar berilgan:

f = 50.0
w_kt = 1
m = 2000
m_0 = 4 * np.pi * 1e-7
l = 0.2
Ue2 = 5.0
tol = 1e-4

Ularning fizik ma'nosi:

Parametr	Qiymat	Tavsifi
f	50 Hz	Chastota
w_kt	1	Birlamchi o‘ramlar soni
m	2000	Nisbiy magnit o‘tkazuvchanlik
μ₀	\(4π×10^{-7}\) H/m	Vakuum magnit o‘tkazuvchanligi
l	0.2 m	Magnit o‘zak uzunligi
Ue2	5 V	Maqsad chiqish kuchlanishi
tol	\(10^{-4}\)	Optimallashtirish aniqligi
4. Optimallashtiriladigan asosiy parametrlar

Loyihaning asosiy optimallashtirish vektori:

$$ \mathbf{x}=[w,S,c] $$

ko‘rinishida beriladi.

Bu yerda:

4.1. O‘ramlar soni — w

O‘ramlar soni sensorning chiqish kuchlanishiga ta'sir qiluvchi asosiy parametrdir.

Kodda:

$$ 20\leq w\leq500 $$

chegaralari berilgan.

Python:

bounds = [
    (20, 500),
    ...
]
4.2. Ko‘ndalang kesim yuzasi — S

Magnit o‘zakning ko‘ndalang kesim yuzasi sensorning elektromagnit xususiyatlariga va chiqish kuchlanishiga ta'sir qiladi.

Optimallashtirish kodida:

$$ 10^{-5}\leq S\leq10^{-3} $$

oralig‘i berilgan.

Python:

(1e-5, 1e-3)
4.3. Havo oralig‘i — c

Havo oralig‘i magnit zanjirning muhim konstruktiv parametrlaridan biridir.

Kodda:

$$ 10^{-4}\leq c\leq2\times10^{-3}\;m $$

chegara qo‘yilgan.

Python:

(1e-4, 2e-3)
5. Tok qiymatlari

Dastur sensor parametrlarining turli tok qiymatlariga bog‘liqligini tekshiradi.

Asosiy tajriba:

$$ I=[10,20,40,80,100,200,400,800,1600,3200]\;A $$

ko‘rinishida bajarilgan.

Notebookning boshqa optimallashtirish tajribasida:

$$ I=[20,100,300,500,1000,2000]\;A $$

qiymatlaridan foydalanilgan.

Shunday qilib, loyiha sensor parametrlarini keng tok diapazonida tahlil qilish imkonini beradi.

6. Optimallashtirish usuli

Optimallashtirish uchun Python SciPy kutubxonasining:

scipy.optimize.minimize

funksiyasidan foydalaniladi.

Optimallashtirish usuli:

method='SLSQP'

ya'ni:

Sequential Least Squares Programming (SLSQP)

usulidir.

Dasturdagi asosiy chaqiruv:

result = optimize.minimize(
    obj_func,
    initial_vars,
    bounds=bounds,
    constraints=constraints,
    method='SLSQP',
    options={'disp': False, 'maxiter': 1000}
)
7. Optimallashtirish cheklovi

Loyihada asosiy cheklov chiqish kuchlanishining maqsad qiymatiga teng bo‘lishidir.

Maqsad:

$$ U_{E2}=5V $$

Shuning uchun cheklov:

$$ U_{E2}-5=0 $$

ko‘rinishida beriladi.

Python kodida:

def constraint_eq(vars):
    w, S, c = vars
    U = 4.44 * f * (I_ * w * m * m_0 * S) / (l + m * c)
    return U - Ue2

ko‘rinishida amalga oshirilgan.

8. Optimallashtirish jarayoni

Dasturdagi hisoblash jarayoni quyidagi ketma-ketlikda amalga oshiriladi:

                Birlamchi tok I
                       │
                       ▼
             Sensor parametrlari
               [w, S, c]
                       │
                       ▼
              Matematik model
                       │
                       ▼
                  U_E2 hisoblash
                       │
                       ▼
                  U_target = 5 V
                       │
                       ▼
              Cheklov tekshiriladi
                       │
                       ▼
                SLSQP algoritmi
                       │
                       ▼
              Parametrlarni yangilash
                       │
                       ▼
              Optimal yechim
                       │
                       ▼
              w_opt, S_opt, c_opt
9. Boshlang‘ich qiymatlarni tanlash

Optimallashtirishdan oldin boshlang‘ich parametrlar tasodifiy tarzda tanlanadi.

Kodda:

w_init = np.random.randint(20, 500)

S_init = np.random.uniform(1e-5, 1e-3)

c_init = np.random.uniform(1e-4, 2e-3)

ishlatilgan.

Natijada boshlang‘ich nuqta:

$$ \mathbf{x}_0=[w_0,S_0,c_0] $$

ko‘rinishida hosil qilinadi.

10. Optimal parametrlarning tokka bog‘liqligi

Optimallashtirish har bir tok qiymati uchun alohida bajariladi.

Natijada:

$$ w=w(I) $$ $$ S=S(I) $$ $$ c=c(I) $$

bog‘lanishlari olinadi.

Bu bog‘lanishlar sensorning konstruktiv parametrlarini tok qiymatiga moslashtirish imkonini beradi.

11. Gradientlarni aniqlash

newmethodoptimizer.py faylida optimal parametrlarning tokka nisbatan o‘zgarish tezligi ham hisoblanadi.

O‘ramlar soni:

$$ \frac{dw}{dI} $$

ko‘ndalang kesim yuzasi:

$$ \frac{dS}{dI} $$

havo oralig‘i:

$$ \frac{dc}{dI} $$

uchun gradientlar aniqlanadi.

Python kodida:

dw_dI = np.gradient(w, I)

dS_dI = np.gradient(S, I)

dc_dI = np.gradient(c, I)

ishlatiladi.

Bu natijalar sensor parametrlarining tok o‘zgarishiga sezgirligini baholash imkonini beradi.

12. Hisoblash natijalari

Koddagi optimallashtirish tajribalaridan birida quyidagi natijalar olingan:

Tok, A	Optimal w	Optimal S, m²	Optimal c, m	U, V
20	388.34	0.000857	0.000271	5.0000
100	497.00	0.000527	0.001360	5.0000
300	305.00	0.000263	0.001244	4.9968
500	333.00	0.000183	0.001601	5.0000
1000	105.00	0.000137	0.000702	5.0000
2000	62.00	0.000145	0.000905	5.0000

Ushbu natijalardan ko‘rinadiki, tok qiymati o‘zgarganda 5 V chiqish kuchlanishini ta'minlash uchun sensorning optimal parametrlari ham o‘zgaradi.

Masalan, tok 20 A dan 2000 A gacha oshganda optimal o‘ramlar soni kamayadi:

$$ w:388.34\rightarrow62 $$

Bu sensor parametrlarining o‘lchanayotgan tok diapazoniga bog‘liq ekanligini ko‘rsatadi.

13. Grafik tahlil

NewMethodOptimizer.ipynb faylida optimal parametrlarning tokka bog‘liqligi grafiklar orqali tahlil qilinadi.

Asosiy grafiklar:

13.1. S(I) va c(I)

Magnit o‘zakning ko‘ndalang kesim yuzasi va havo oralig‘ining tokka bog‘liqligi.

$$ S=S(I) $$ $$ c=c(I) $$
13.2. S(I) va w(I)

Ko‘ndalang kesim yuzasi va o‘ramlar sonining tokka bog‘liqligi.

$$ S=S(I) $$ $$ w=w(I) $$
13.3. c(I) va w(I)

Havo oralig‘i va o‘ramlar sonining tokka bog‘liqligi.

$$ c=c(I) $$ $$ w=w(I) $$

Ushbu grafiklar sensor parametrlarining bir-biri bilan qanday bog‘langanligini ko‘rsatadi.

14. Parametrik tadqiqotlar

Notebookda optimallashtirishdan tashqari parametrik tadqiqotlar ham bajarilgan.

Bunda alohida parametrning chiqish kuchlanishiga ta'siri tekshiriladi.

Asosiy tahlil qilinadigan parametrlar:

o‘ramlar soni w;
ko‘ndalang kesim yuzasi S;
havo oralig‘i l_H;
birlamchi tok I.

Bunda:

$$ U=U(I,w) $$ $$ U=U(I,S) $$ $$ U=U(I,l_H) $$

bog‘lanishlari tahlil qilinadi.

15. 5 V chiqish kuchlanishiga mos tok

Notebookda berilgan parametrlar uchun chiqish kuchlanishi 5 V ga teng bo‘ladigan tok qiymatini aniqlashga ham e'tibor berilgan.

Umumiy holda:

$$ U(I,x)=5V $$

tenglamasidan:

$$ I=I_{5V}(x) $$

aniqlanadi.

Bu yerda x:

w;
S;
l_H

parametrlaridan biri bo‘lishi mumkin.

Natijada sensorning qaysi parametrlarida ma'lum tok uchun 5 V chiqish hosil bo‘lishini aniqlash mumkin.

16. Adekvatlikni baholash

Notebookda chiqish kuchlanishining 5 V maqsad qiymatiga qanchalik yaqinligi ham baholanadi.

Umumiy xatolik:

$$ E=|U-U_{target}| $$

Nisbiy xatolik:

$$ \delta= \frac{|U-U_{target}|} {U_{target}}\times100\% $$

Maqsad kuchlanish:

$$ U_{target}=5V $$

Masalan, ±0.45 % chegarada:

$$ \Delta U=5\times0.0045=0.0225V $$

Shunda:

$$ 4.9775V\leq U\leq5.0225V $$

oralig‘idagi natijalar maqsad qiymatga mos deb baholanishi mumkin.

17. Loyiha fayllari

Repository quyidagi asosiy fayllardan tashkil topgan:

Monitoring_sensori_parametrlari-optimizatsiyasi/
│
├── NewMethodOptimizer.ipynb
│
├── newmethodoptimizer.py
│
└── README.md
newmethodoptimizer.py

Python dasturining asosiy fayli.

U quyidagi vazifalarni bajaradi:

tok qiymatlarini qabul qilish;
sensor modelini hisoblash;
optimallashtirish;
optimal w, S, c qiymatlarini aniqlash;
gradientlarni hisoblash;
natijalarni konsolga chiqarish.
NewMethodOptimizer.ipynb

Jupyter Notebook.

Unda:

matematik hisoblashlar;
optimallashtirish;
parametrik tadqiqotlar;
grafiklar;
natijalarni taqqoslash;
adekvatlik tahlili

bajariladi.

18. Foydalanilgan Python kutubxonalari

Loyihada quyidagi asosiy kutubxonalardan foydalaniladi:

NumPy
SciPy
Matplotlib
Pandas
Jupyter Notebook

O‘rnatish:

pip install numpy scipy matplotlib pandas jupyter
19. Dasturni ishga tushirish

Repositoryni yuklab olish:

git clone https://github.com/aaotemirov/Monitoring_sensori_parametrlari-optimizatsiyasi.git

Repository katalogiga kirish:

cd Monitoring_sensori_parametrlari-optimizatsiyasi

Python dasturini ishga tushirish:

python newmethodoptimizer.py

Notebookni ishga tushirish:

jupyter notebook

Keyin:

NewMethodOptimizer.ipynb

faylini ochish mumkin.

20. Tadqiqotni qayta ishlab chiqarish

Hisoblash natijalarini qayta olish uchun:

Repository yuklab olinadi.
Python muhiti yaratiladi.
Kerakli kutubxonalar o‘rnatiladi.
NewMethodOptimizer.ipynb ochiladi.
Boshlang‘ich parametrlar tekshiriladi.
Tok diapazoni belgilanadi.
Optimallashtirish algoritmi ishga tushiriladi.
Optimal w, S, c qiymatlari olinadi.
Chiqish kuchlanishi tekshiriladi.
Grafiklar hosil qilinadi.
Natijalar jadval ko‘rinishida tahlil qilinadi.
21. Tadqiqotning asosiy natijasi

Loyihaning asosiy natijasi — berilgan birlamchi tok uchun 5 V chiqish kuchlanishini ta'minlaydigan optimal sensor parametrlarini aniqlash.

Asosiy bog‘lanish:

$$ I\rightarrow(w,S,c)\rightarrow U_{E2} $$

ko‘rinishida.

Optimallashtirish natijasida:

$$ (w,S,c)_{opt} $$

topiladi.

Shu orqali:

$$ U_{E2}\approx5V $$

sharti ta'minlanadi.

22. Ilmiy ahamiyati

Ushbu dasturiy model Hall effectli/havo oralig‘idagi tok sensorlarini loyihalash va optimallashtirish bo‘yicha hisoblash tadqiqotlarida foydalanilishi mumkin.

Model yordamida:

tok diapazoniga mos sensor parametrlarini aniqlash;
o‘ramlar sonini optimallashtirish;
magnit o‘zakning ko‘ndalang kesim yuzasini tanlash;
havo oralig‘ini optimallashtirish;
chiqish kuchlanishini maqsad qiymatga moslashtirish;
parametrlarning tokka bog‘liqligini aniqlash;
optimal parametrlarning gradientlarini hisoblash

mumkin.

23. Metodik izoh

Mazkur repositorydagi matematik modelda optimallashtirishning asosiy maqsadi bevosita I_meas - I_true xatoligini minimallashtirish emas.

Ushbu versiyada asosiy optimallashtirish masalasi:

$$ U_{E2}=5V $$

shartini qanoatlantiruvchi:

$$ w,\;S,\;c $$

parametrlarni aniqlashga qaratilgan.

Shuning uchun loyiha ikki asosiy qismga ajratiladi:

1. Matematik model
$$ U_{E2} = \frac{4.44 f I w \mu \mu_0 S} {l+\mu c} $$
2. Optimallashtirish
$$ \mathbf{x}=[w,S,c] $$

uchun:

$$ U_{E2}(\mathbf{x})=5V $$

shartini qanoatlantiruvchi optimal yechimni aniqlash.

Bu yondashuv keyinchalik real eksperimental tok va sensor chiqish signallari bilan birlashtirilib, o‘lchash xatoligini alohida optimallashtirish uchun kengaytirilishi mumkin.

24. Citation

Ushbu repository ilmiy maqola, dissertatsiya, konferensiya maqolasi yoki texnik hisobotda dasturiy tadqiqot manbasi sifatida ko‘rsatilishi mumkin.

APA

Temirov, A. (2026). Hall Effectli Havo Oralig‘idagi Tok Sensorini Optimallashtirish. GitHub.

BibTeX
@software{temirov2026hall,
  author    = {Azizbek Temirov},
  title     = {Hall Effectli Havo Oralig‘idagi Tok Sensorini Optimallashtirish},
  year      = {2026},
  publisher = {GitHub},
  url       = {https://github.com/aaotemirov/Monitoring_sensori_parametrlari-optimizatsiyasi}
}
25. DOI va Zenodo

Loyihaning ilmiy maqola yoki dissertatsiyada doimiy manba sifatida foydalanilishi uchun GitHub repositoryga DOI biriktirish tavsiya etiladi.

Tavsiya etiladigan jarayon:

GitHub Repository
        ↓
Git Tag / Release
        ↓
Zenodo
        ↓
DOI
        ↓
Ilmiy maqola / Dissertatsiya

DOI olingandan so‘ng README faylining Citation qismiga DOI qo‘shiladi.

26. Versiyalash

Tadqiqotning turli bosqichlarini saqlash uchun Git taglardan foydalanish mumkin.

Masalan:

git tag v1.0.0
git push origin v1.0.0

Versiyalar:

v1.0.0 — dastlabki optimallashtirish modeli
v1.1.0 — parametrik tadqiqotlar
v1.2.0 — grafik va adekvatlik tahlili
v2.0.0 — kengaytirilgan sensor modeli
27. Muallif

Azizbek Temirov

Tadqiqot yo‘nalishi:

Hall effectli tok sensorlari;
havo oralig‘idagi magnit tizimlar;
kontaktsiz tok o‘lchash;
sensor parametrlarini optimallashtirish;
elektromagnit modellashtirish;
matematik optimallashtirish;
tok diapazoniga mos sensor parametrlarini aniqlash.
28. Repository

GitHub:

https://github.com/aaotemirov/Monitoring_sensori_parametrlari-optimizatsiyasi

29. Xulosa

Ushbu loyiha Hall effectli/havo oralig‘idagi tok sensorining parametrlarini matematik modellashtirish va optimallashtirish uchun ishlab chiqilgan.

Asosiy optimallashtirish parametrlari:

$$ \boxed{w,\;S,\;c} $$

bo‘lib, ular:

o‘ramlar soni;
magnit o‘zakning ko‘ndalang kesim yuzasi;
havo oralig‘i

ni ifodalaydi.

Kirish parametri:

$$ \boxed{I} $$

ya'ni birlamchi tok.

Asosiy chiqish:

$$ \boxed{U_{E2}} $$

va optimallashtirish maqsadi:

$$ \boxed{U_{E2}=5V} $$

shartini ta'minlashdan iborat.

Shunday qilib, loyiha:

$$ \boxed{ I\rightarrow (w,S,c)_{opt} \rightarrow U_{E2}\approx5V } $$

bog‘lanishi orqali tok sensorining optimal parametrlarini aniqlash imkonini beradi.


Bu variant **sizning faylingizdagi haqiqiy `w`, `S`, `c`, `I`, `Ue2`, `SLSQP`, 5 V va tok diapazonlariga moslangan**; masalan, kodingizda `w`, `S`, `c` aynan optimallashtirish o‘zgaruvchilari sifatida berilgan. :contentReference[oaicite:0]{index=0}

Yana muhim jihati: README'da **Hall sensoriga aloqasi bo‘lmagan umumiy parametrlarni qo‘shmadim**. Asosiy urg‘u tok, tokka bog‘liq sensor parametrlari, havo oralig‘i, o‘ramlar soni, kesim yuzi va 5 V chiqishga qaratilgan.
