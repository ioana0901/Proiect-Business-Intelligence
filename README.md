# Proiect-Business-Intelligence
## Analiza datelor cu privire la comerțul cu amănuntul din Bacău
### Cuprins
[1. Descrierea scenariului de business](#heading)<br>
[2. Pregătirea datelor](#heading)<br>
[3. Analiza și vizualizarea datelor](#heading)<br>
[4. Crearea Dashboard-ului](#heading)<br>
[5. Crearea unei povești](#heading)<br><br>

### 1. Descrierea scenariului de business<br>


În cadrul acestui proiect voi analiza date cu privire la domeniul comerțului cu amănuntul din județul Bacău.<br>
Domeniul de activitate este studiat are codul CAEN 47 și se referă la comerțul cu amănuntul, cu excepția autovehiculelor și motocicletelor.<br>
În cadrul proiectului voi utiliza 8 seturi de date:
<ul>
<li>4 fișiere (tip csv) ce conțin listele cu firmele înregistrate în ONRC până în 2019. De aici voi extrage Codul Unic de Identificare, denumirea firmelor și datele cu privire la localitățile în care firmele își au sediul;</li>
<li>Pentru fiecare an (2016, 2017, 2018, 2019) câte 2 fișiere (de tip text) care conțin date cu privire la firmele care au depus bilanț lung, scurt și raportări anuale; </li>
</ul>

### 2. Pregătirea datelor

a. Încărcarea datelor în Tableau Prep <br>
![image](https://user-images.githubusercontent.com/63421754/124277848-3222b700-db4e-11eb-8dae-f0ef43ce5231.png)
<br>
b.Pregătirea datelor din fișierele ce conțin listele cu firmele care sunt neradiate și au sediu. Mai jos am arătat pașii pe care i-am urmat pentru datele din setul „2019-neradiate-cu-sediu_4” (am urmat aceiași pași și pentru celelalte 3 seturi):<br>
-Mai întâi am eliminat atributele EUID, COD_INMATRICULARE și STARE_FIRMA, întrucât nu este nevoie de acestea:<br>
![image](https://user-images.githubusercontent.com/63421754/124277936-4e265880-db4e-11eb-9c93-4cf3fb179f89.png)<br>
-am adăugat apoi un clean step (curatare-firme-1), după care la vizionarea datelor am observat că atributul CUI este de tip number, așa că l-am schimbat în string. Totodată, am eliminat și valorile nule:<br>
![image](https://user-images.githubusercontent.com/63421754/124278011-64ccaf80-db4e-11eb-8bd0-c71a8e6aa2f0.png)<br>
-După ce am am făcut toate aceste operații și asupra celorlalte 3 seturi de date, am realizat uniunea lor pentru a le avea pe toate la un loc:<br>
![image](https://user-images.githubusercontent.com/63421754/124278081-7ada7000-db4e-11eb-9476-1eae331461d7.png)<br>
-În cadrul reuniunii de mai sus am filtrat rezultatele după județe. Pentru asta, am realizat splitarea coloanei ADRESA după virgulă, pentru ultimele două câmpuri:<br>
![image](https://user-images.githubusercontent.com/63421754/124278153-947bb780-db4e-11eb-880f-9d90691cf64c.png)<br>
-Apoi, am șters primul split, întrucât nu conținea decât detalii în legătură cu adresa și în cadrul splitului 2 am realizat filtrarea după județele Bacău:<br>
![image](https://user-images.githubusercontent.com/63421754/124278209-a52c2d80-db4e-11eb-948a-3efee9e7e704.png)<br>
-Am realizat un nou split al coloanei ADRESA, după virgulă, pentru primul câmp pentru a scoate toate localitățile. Am redenumit coloana în „localitate”:
![image](https://user-images.githubusercontent.com/63421754/124278262-b7a66700-db4e-11eb-9f50-f3b05eb3c6d3.png)<br>
La sfârșit, am eliminat coloana adreselor, rezultatul final arătând astfel:<br>
![image](https://user-images.githubusercontent.com/63421754/124278314-c7be4680-db4e-11eb-9363-9a2d4d211ff5.png)<br>

c.Pregătirea datelor din fișierele bilant_lung:<br>
Mai jos am arătat pașii pe care i-am urmat pentru datele din setul „2016-bilant-lung” (am urmat aceiași pași și pentru celelalte 3 seturi):<br>
-Mai întâi am schimbat tipurile atributelor CUI și CAEN în string, similar cu ce am făcut la celălalt set de date de mai sus;<br>
![image](https://user-images.githubusercontent.com/63421754/124278567-15d34a00-db4f-11eb-8168-c78d58b48d85.png)<br>
-După aceea, am realizat uniunea celor 4 seturi:<br>
![image](https://user-images.githubusercontent.com/63421754/124278634-297eb080-db4f-11eb-893a-723887106ad7.png)<br>
Am adăugat un clean step la această uniune în care am realizat filtrarea după codul CAEN 47:<br>
![image](https://user-images.githubusercontent.com/63421754/124278678-39969000-db4f-11eb-94f5-0c6d16fb29b1.png)<br>
-De asemenea, am observat că unele coloane au valori nule pe care le-am transformat în 0:<br>
![image](https://user-images.githubusercontent.com/63421754/124278762-56cb5e80-db4f-11eb-874b-791cc23cd85f.png)<br>
d.Realizarea join-ului între cele două uniuni:<br>
-La final, am realizat un join între cele două uniuni realizate la pașii anteriori folosind codul CUI;<br>
![image](https://user-images.githubusercontent.com/63421754/124278831-6d71b580-db4f-11eb-9755-22ae10ae338d.png)<br>
-am adăugat un nou clean step pentru a mai adăuga un ultim retuș datelor. Am observat că sunt anumite câmpuri care au valori nule, pecare le-am transformat în zero prin Group Values. De asemenea, am realizat automatic split asupra coloanei localitate pentru a rămâne doar cu denumirea lor și am schimbat tipul coloanelor în care s-au păstrat numele tabelelor cu ajutorul cărora s-au făcut join-ul în date, dar și denumire lor cu anul corespunzător. Am redenumit această coloană în Year:<br>
![image](https://user-images.githubusercontent.com/63421754/124278901-837f7600-db4f-11eb-851d-c8fa3bce5bcf.png)<br>
-La final, am adăugat un Output pentru a putea încărca mai departe rezultatul în Tableau Desktop<br>
![image](https://user-images.githubusercontent.com/63421754/124278966-985c0980-db4f-11eb-8a9e-c0c884bd3ae1.png)<br>
### 3.	Data Visualization & Analysis

În vederea înterpretării datelor, voi utiliza aplicația Tableau Desktop. Astfel, voi începe prin a încărca Output-ul realizat anterior în aplicație:<br>
![image](https://user-images.githubusercontent.com/63421754/124279055-b0cc2400-db4f-11eb-95d5-0a7335ebfbf8.png)<br>
-Am schimbat tipului coloanei Localitate în tip geografic în City pentru a putea realiza o hartă:<br>
![image](https://user-images.githubusercontent.com/63421754/124279128-c9d4d500-db4f-11eb-8403-2447e2712230.png)<br>
Pentru început, am realizat o hartă pentru a putea vizualiza amplasarea județului și numărul firmelor care activează în acesta:<br>
-Am folosit atributele Județ și CUI, pe care l-am schimbat măsura în count distinct, pentru a putea avea numărul firmelor exact în funcție de județ:<br>
![image](https://user-images.githubusercontent.com/63421754/124279187-e113c280-db4f-11eb-8daa-ad547f418daf.png)<br>
-Am adăugat CUI-ul atât în colors, cât și în label pentru ca informația să fie cât mai evidențiată;<br>
-În plus, am adăugat și județul în labels, pentru ca informațiile să fie complete;<br>
![image](https://user-images.githubusercontent.com/63421754/124283061-2639f380-db54-11eb-9185-7faf3c32b90e.png)
<br>

<li>Astfel, din harta de mai sus se observă faptul că, în județul Bacău se află 567 de firme care au ca domeniu de activitate comerțul cu amănuntul.</li>
Pentru a vedea distribuția firmelor în orașele din județ, am realizat o nouă hartă ca cea de mai sus, însă în loc de județ, am utilizat Localitate.<br>
![image](https://user-images.githubusercontent.com/63421754/124282097-1cfc5700-db53-11eb-8925-aa8e721f2050.png)
<br>
<li>Astfel, se observă faptul că cele mai multe astfel de firme se află în Municipiul Bacău, în număr de 219.</li>
<br>Mai departe, pentru a vedea profitul net la nivel de județ pe parcursul celor 4 ani, am realizat un grafic cu bare utilizând atributele Profit net în rows și Year în columns.
<br> 
![image](https://user-images.githubusercontent.com/63421754/124283239-5aadaf80-db54-11eb-8f61-cdbe5b269fae.png)
<br>
<li>Din grafic se observă faptul că în 2019 s-a înregistrat cel mai mare profit. De asemenea, se mai observă faptul că din 2016 până în 2019 profitul net a tot crescut.</li>
<br>Pentru a putea compara profitul și pierderea, am creat un nou grafic de tip side-by-side pentru a putea compara profitul si pierderea netă înregistrate. Pentru acest grafic am utilizat year, pierdere netă și profit net. De asemenea, am realizat o filtrare după nume, prin care am exclus firma Dedeman, întrucât aceasta influența foarte mult rezultatele. Nu în ultimul rând, am evidențiat valorile rezultatelor prin <i>mark label->always show.</i><br>
![image](https://user-images.githubusercontent.com/63421754/124279879-ac543b00-db50-11eb-8675-71d7c5563ab8.png)<br>
![image](https://user-images.githubusercontent.com/63421754/124282385-706ea500-db53-11eb-89c9-509eb96e2ff9.png)<br>
<li>Din graficul de mai sus se observă faptul că de-a lungul celor 4 ani, s-au profitul s-a menținut mult mai sus de cât perderea, în special în anul 2019 unde diferența este cu mult mai mare.</li>
<br>Un rol important în reflectarea performanţelor întreprinderilor o are <b>rata profitului</b>, care se calculează ca raport procentual între suma profitului aferent cifrei de afaceri și venituri. Astfel, am adăugat un câmp calculat folosind formula de mai jos:<br>
![image](https://user-images.githubusercontent.com/63421754/124280258-24bafc00-db51-11eb-87b1-2d59f1fe078f.png)<br>
-Pentru a crea graficul am utilizat Year și Rata Profitului, a cărei măsură am transformat-o în average. În plus, am modifcat axa pentru a restrânge intervalul arătat pe aceasta:<br>
![image](https://user-images.githubusercontent.com/63421754/124280507-706da580-db51-11eb-9042-c71521d1f667.png)<br>
![image](https://user-images.githubusercontent.com/63421754/124280391-4c11c900-db51-11eb-83db-4bea5e8a2f4e.png)<br>
<li>Din graficul de mai sus, reiese faptul că în anii 2016 și 2018 rata medie a profitului a avut cele mai mari valori, pe când în 2019, aceasta a scăzut.</li>
<br>Mai departe, doresc să aflu în ce măsură sunt influențate activele totale de datorii în cadrul firmelor din acest domeniu.<br>
-Mai întâi am creat un nou câmp pentru a calcula <b>activele totale</b>
![image](https://user-images.githubusercontent.com/63421754/124280670-a27f0780-db51-11eb-874b-53c09969d0fb.png)<br>
-Apoi, m-am folosit de Datorii și ActiveTotale pentru a crea un grafic de tip scatterplot, după care am adăugat o linie de trend:<br>
![image](https://user-images.githubusercontent.com/63421754/124280753-bd517c00-db51-11eb-9dfb-6593db397ee3.png)<br>
<li>Din imaginea de mai sus se observă că există o corelație puternică (0.84) între cele două variabile arătând faptul că activele totale sunt într-adevăr influențate de datorii.</li>
<br>Mai departe, am mai creat un nou câmp calculat pentru a putea afla <b>viteza de rotație a activelor circulante</b>:<br>
![image](https://user-images.githubusercontent.com/63421754/124280955-ebcf5700-db51-11eb-88ad-9da1d09fd2d0.png)<br>
-Am creat apoi un nou grafic asemănător cu cel care prezintă activelel totale:<br>
![image](https://user-images.githubusercontent.com/63421754/124281073-086b8f00-db52-11eb-9e2d-655bb8f99d00.png)<br>
<li>De aici se observă faptul că acest coeficient a scăzut de-a lungul anilor, fapt ce sugerează că gradul de imobilizare a activelor a în creștere.</li>
### 4. Crearea Dashboard-ului
<br> Mai jos sunt prezentate dashboard-urile create în cadrul proiectului. acestea au fost folosite și în crearea poveștii de la punctul 5.<br>
![image](https://user-images.githubusercontent.com/63421754/124281591-87f95e00-db52-11eb-8762-6d6edc4bebd1.png)
<br>
![image](https://user-images.githubusercontent.com/63421754/124281647-9778a700-db52-11eb-9c5d-8e0de60df267.png)
<br>
![image](https://user-images.githubusercontent.com/63421754/124281707-a8c1b380-db52-11eb-87f9-7e6b492619e8.png)
<br>
![image](https://user-images.githubusercontent.com/63421754/124281744-b4ad7580-db52-11eb-80f0-78e1acefe519.png)
<br>
![image](https://user-images.githubusercontent.com/63421754/124281775-c131ce00-db52-11eb-88ac-95182a35e179.png)
<br>
![image](https://user-images.githubusercontent.com/63421754/124281813-cc84f980-db52-11eb-9bb8-29dc988d1e7e.png)
<br>












 













