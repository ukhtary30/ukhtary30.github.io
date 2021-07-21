# Tutorial Symbolic Python (SymPy)
## Pendahuluan

Selain digunakan untuk perhitungan numerik, Phyton dapat digunakan juga untuk perhitungan simbolik (analytical calculation). Perhitungan simbolik Phyton dapat dilakukan dengan menggunakan library SymPy. Library ini memiliki fitur seperti program Mathematica, tetapi dapat digunakan tanpa biaya. SymPy sangat berguna saat kita memerlukan ekspresi analitik dari suatu perhitungan, seperti turunan dan integral dari suatu fungsi atau menyelesaikan suatu persamaan differensial. 

Untuk memulai menggunakan SymPy, kita harus memanggil library SymPy. Di tutorial ini, saya menggunakan Jupyter notebook, supaya hasil dari perhitungan SymPy bisa langsung terlihat. 
```ruby
import sympy
sympy.init_session()
x, y, z = symbols("x y z ")

x + z # semisal kita ingin menghitung x + z
```
Baris 1 dan 2 adalah cara memanggil library SymPy, sedangkan baris 3 adalah perintah untuk mendefinisikan variabel dalam perhitungan. Dalam contoh ini, kita menggunakan variable x,y dan z. Semisal kita ingin menghitung x+z, maka kita tinggal mengetik seperti baris 5. Berikut, beberapa contoh expresi matematika yang sering dipakai dalam perhitungan.
```ruby
exp(-I*x), cos(x), atan(x), besselj(0,x), sqrt(pi) 
```  
Bila kita evaluasi, maka akan memberikan output sebagai berikut.
  
<img width="524" alt="Screen Shot 2021-07-20 at 15 18 45" src="https://user-images.githubusercontent.com/87349156/126271355-d5bb1d88-334d-449c-a149-d750d1dd383a.png">
di mana I adalah bilangan imajiner. Semisal kita ingin melakukan expansi aljabar sebagai berikut,

<img width="55" alt="Screen Shot 2021-07-20 at 15 23 43" src="https://user-images.githubusercontent.com/87349156/126271989-a89b2319-6b10-4d53-b330-c6fd88b852ac.png">
input pada SymPy adalah,

    expand(x*(z+y)**2)
    
dengan output sebagai berikut,

<img width="498" alt="Screen Shot 2021-07-20 at 15 26 13" src="https://user-images.githubusercontent.com/87349156/126272229-6bf2bb08-0ce0-443d-8470-30cba264b1a1.png">

Sebaliknya, bila kita ingin menyederhanakan suatu persamaan, semisal kita ingin menyederhanakan persamaan (2), maka ada dua jenis input pada SymPy,

    simplify(x*y**2+2*x*y*z + x*z*z)
    factor(x*y**2+2*x*y*z + x*z*z)
    
Baris 1 akan memberi output sebagai berikut,

<img width="528" alt="Screen Shot 2021-07-20 at 15 28 08" src="https://user-images.githubusercontent.com/87349156/126272377-06538595-2e3b-441a-8d9f-ec22883879bd.png">
Sedangkan baris 2 akan memberi output,

<img width="530" alt="Screen Shot 2021-07-20 at 15 29 45" src="https://user-images.githubusercontent.com/87349156/126272569-8e199229-a9e3-4e2c-989b-b9193da36028.png">

Selanjutnya, kita akan mencoba bagaimana cara kita melakukan perhitungan simbolik yang lebih kompleks.

---

## Limit, Turunan dan Integral
### Limit

Semisal kita ingin menghitung limit dari fungsi berikut,

<img width="528" alt="Screen Shot 2021-07-20 at 15 32 00" src="https://user-images.githubusercontent.com/87349156/126272804-30563d32-35b9-432d-809c-74d5282bba2d.png">

Kita tahu bahwa jawaban dari persamaan (5}) adalah 1. Untuk menghitung persamaan (5), kita menuliskan input SymPy sebagai berikut,

    limit(sin(x)/x,x,0)
    
yang memberi output 1. Secara umum, perintah limit terdiri atas tiga argumen. Argumen pertama adalah fungsi yang akan dihitung limitnya, argumen kedua adalah variable dari fungsi tersebut, sedangkan argumen ketiga adalah batas dari limit tersebut. Sebagai contoh lain, semisal kita ingin menghitung limit dari fungsi berikut,

<img width="519" alt="Screen Shot 2021-07-20 at 15 33 25" src="https://user-images.githubusercontent.com/87349156/126272985-550ee95c-4b43-4d42-8f96-85a24578b057.png">

Input pada SymPy adalah sebagai berikut,

    limit((3+4*x)/(5+6*x),x,oo)
    
dengan output 2/3. oo adalah input untuk ∞.

---

### Turunan

Semisal kita ingin menghitung turunan fungsi sebagai berikut

<img width="532" alt="Screen Shot 2021-07-21 at 11 19 25" src="https://user-images.githubusercontent.com/87349156/126420235-fc4c42b5-30aa-4bc1-834d-8a0af042281d.png">

Maka input pada SymPy adalah sebagai berikut,

    f=5*x**2-cos(3*x)+6*x*y*z
    diff(f,x,1)
    
di mana kita mendefinisikan fungsi tersebut sebagai f. Perintah diff memiliki tiga argumen. Argumen pertama adalah fungsi yang akan diturunkan, argumen kedua adalah variabel fungsi yang diturunkan, dan argumen ketiga adalah orde dari turunan. Dalam contoh ini kita memilih orde 1, karena kita menghitung turunan pertama. Output dari input SymPy ini adalah,

<img width="527" alt="Screen Shot 2021-07-21 at 11 20 40" src="https://user-images.githubusercontent.com/87349156/126420360-e95044ad-b5c2-457d-9dbd-086b32048721.png">

Sebagai contoh lain, semisal kita ingin menghitung turunan dari fungsi Bessel berikut,

<img width="318" alt="Screen Shot 2021-07-21 at 11 21 32" src="https://user-images.githubusercontent.com/87349156/126420437-e3959f74-d1d0-4de9-a261-c6543c581c65.png">

y adalah orde dari fungsi Bessel. Maka input pada SymPy adalah sebagai berikut,

    f=besselj(y,x)
    diff(f,x,2)
    
dengan output sebagai berikut,

<img width="381" alt="Screen Shot 2021-07-21 at 11 22 49" src="https://user-images.githubusercontent.com/87349156/126420525-38fba59d-52e6-437f-b35a-8b885bceb380.png">

---

### Integral

Mari kita coba integralkan fungsi pada persamaan (8) sebagai berikut,

<img width="382" alt="Screen Shot 2021-07-21 at 11 24 07" src="https://user-images.githubusercontent.com/87349156/126420639-aa6725af-f5ab-49ec-9be3-2f380309451f.png">

Untuk menghitung intgral tanpa batas tersebut menggunakan SymPy, input pada SymPy adalah sebagai berikut,

    f=10*x + 6*y*z + 3 * sin(3*x)
    integrate(f,x)
    
dengan output sebagai berikut,

<img width="348" alt="Screen Shot 2021-07-21 at 11 25 01" src="https://user-images.githubusercontent.com/87349156/126420705-0bc11815-efdf-4379-be1a-65796940668e.png">

Argumen pertama dari integrate adalah fungsi yang akan diintegralkan, sedangkan argumen kedua adalah variable integral. Bagaimana dengan integral yang memiliki batas seperti di bawah ini?

<img width="397" alt="Screen Shot 2021-07-21 at 11 25 39" src="https://user-images.githubusercontent.com/87349156/126420752-a818cc12-8802-43c7-ac7b-53f403467fd2.png">

Untuk menyelesaikan integral tersebut, input pada SymPy adalah sebagai berikut,

    f=10*x + 6*y*z + 3 * sin(3*x)
    integrate(f,(x,a,b))
    
Contoh selanjutnya adalah intergral rangkap dua seperti di bawah ini,

<img width="403" alt="Screen Shot 2021-07-21 at 11 26 39" src="https://user-images.githubusercontent.com/87349156/126420852-c38ff8cb-c1c1-444e-8a83-d3fb0f631825.png">

Input pada SymPy adalah sebagai berikut.

    f=10*x + 6*y*z + 3 * sin(3*x)
    integrate(f,(x,a,b),(y,d,c))
    
Contoh terakhir adalah integral berikut yang merupakan definisi fungsi Gamma (Γ(y)),

<img width="367" alt="image" src="https://user-images.githubusercontent.com/87349156/126421009-8b86406c-8d9f-4195-8c69-c1507915cf57.png">

Maka, input pada SymPy adalah,

    f=x**(y-1)*exp(-x)
    integrate(f,(x,0,oo))
    
yang menghasilkan output sebagai berikut,

<img width="369" alt="image" src="https://user-images.githubusercontent.com/87349156/126421109-15a43dda-41a3-45d8-a8b9-e16293dbc497.png">
---
## Ekspansi fungsi, Akar dari fungsi, dan Matriks
### Ekspansi fungsi

Semisal kita ingin mengkespansi suatu fungsi dalam bentuk deret. Ekspansi ini dikenal dengan nama ekspansi Taylor. Sebagai contoh, semisal kita ingin mengekspansi fungsi berikut,

<img width="301" alt="Screen Shot 2021-07-21 at 11 30 08" src="https://user-images.githubusercontent.com/87349156/126421225-bce11f5b-e3a6-4c11-9fed-ac4c95965d20.png">

dekat titik x = a, maka input pada SymPy adalah sebagai berikut,

    f=sin(x)
    series(f,x,a,3)
    
di mana kita melakukan ekspansi sampai tiga deret. Output dari perhitungan ini adalah,

<img width="522" alt="Screen Shot 2021-07-21 at 11 31 49" src="https://user-images.githubusercontent.com/87349156/126421365-bd713608-3fbf-47f7-8870-2b973dac272c.png">

di mana O menyatakan orde error dari perhitungan. Argumen pertama dari series adalah fungsi yang ingin dideretkan, argumen kedua adalah variabel dari deret, argumen ketiga adalah titik evaluasi deret dan argumen keempat adalah jumlah orde deret yang diinginkan.

Contoh lainnya adalah ekspansi dari fungsi Bessel berikut di sekitar x = 0,

<img width="311" alt="Screen Shot 2021-07-21 at 11 32 37" src="https://user-images.githubusercontent.com/87349156/126421439-e04130d1-dfb6-4ae9-b77d-7e331dba144e.png">

Maka, input pada SymPy adalah sebagai berikut,

    f=besselj(0,x)/x
    series(f,x,0,3)

dengan output sebagai berikut,

<img width="346" alt="Screen Shot 2021-07-21 at 11 34 26" src="https://user-images.githubusercontent.com/87349156/126421594-ceed7af4-1206-4a84-95f6-0740cd3bc85e.png">

---

### Akar dari fungsi

Akar dari suatu fungsi f(x) didefinisikan sebagai berikut,

<img width="306" alt="Screen Shot 2021-07-21 at 11 35 38" src="https://user-images.githubusercontent.com/87349156/126421740-e6dc8b78-69d1-4d2f-b077-c756c6be04ec.png">

di mana x<sub>0</sub> adalah akar dari fungsi f(x). Semisal kita ingin mencari akar dari fungsi kuadratik berikut

<img width="317" alt="Screen Shot 2021-07-21 at 11 36 26" src="https://user-images.githubusercontent.com/87349156/126421834-4fae3672-2018-4bca-9756-c9d541ecfc66.png">

Maka, input pada SymPy adalah sebagai berikut,

    f=a*x**2+b*x+c
    solve(f,x)
    
yang memberikan output sebagai berikut,

<img width="411" alt="Screen Shot 2021-07-21 at 11 37 25" src="https://user-images.githubusercontent.com/87349156/126421912-56dec405-ceb5-48a6-bf5e-0973d330d357.png">

Argumen pertama dari solve adalah fungsi yang akan dicari akarnya dan argumen kedua adalah variabel akar. Solve juga dapat digunakan untuk menyelesaikan suatu persamaan transendental seperti berikut,

<img width="327" alt="Screen Shot 2021-07-21 at 11 37 52" src="https://user-images.githubusercontent.com/87349156/126421947-cc4183c3-9f91-478f-abdc-c4493516c915.png">

Maka, solusi dari persamaan tersebut dapat dihitung menggunakan SymPy dengan input sebagai berikut,

    f=cos(x)-sin(2x)
    solve(f,x)
    
yang memberikan output untuk x sebagai berikut,

<img width="341" alt="Screen Shot 2021-07-21 at 11 38 40" src="https://user-images.githubusercontent.com/87349156/126422038-575a63ba-2505-406b-8b52-f64b60acf1fa.png">

---

### Matriks

Matriks dapat ditulis pada SymPy sebagai berikut,

    M = Matrix([[1,2],[3,4]])
    M
yang memberikan output matriks M sebagai berikut,

<img width="307" alt="Screen Shot 2021-07-21 at 11 40 22" src="https://user-images.githubusercontent.com/87349156/126422160-2d0d4a1b-04e0-4b6e-b581-bf75e81ea480.png">

Perkalian matriks dapat dilakukan seperti berikut,

    M = Matrix([[1,2],[3,4]])
    M*M
    
yang menghasilkan output berupa perkalian matriks M x M

<img width="312" alt="Screen Shot 2021-07-21 at 11 41 18" src="https://user-images.githubusercontent.com/87349156/126422226-305749aa-cbc8-49d7-9680-7d9fe8011e15.png">

Determinant dan inverse dari suatu matriks dapat dihitung dengan input sebagai berikut,

    M = Matrix([[1,2],[3,4]])
    M.det()
    M.inv()
    
Baris kedua akan memberikan determinant dari matriks M, sedangkan baris ketiga memberikan inverse dari matriks M.
Eigen value dan eigen vektor dari matriks M dapat dihitung dengan input sebagai berikut,

    M = Matrix([[1,2],[3,4]])
    M.eigenvects()
   
yang memberikan output sebagai berikut,

  <img width="523" alt="Screen Shot 2021-07-21 at 11 42 46" src="https://user-images.githubusercontent.com/87349156/126422356-a1909ef0-7c61-4fda-908e-51aa7c16463e.png">
  
Ada dua eigen value dan eigen vektor dari matriks M. Kolom pertama dari masing-masing solusi adalah nilai eigenvalue, kolom kedua adalah multiplisitas dari eigen value dan kolom ketiga adalah eigen vektor. Terkhir, kita juga bisa mendiagonalisasi matriks M. Dalam kasus ini, kita menuliskan matriks M sebagai M=PDP<sup>-1</sup>, di mana $D$ adalah matriks yang sudah didiagonalisasi dan matriks P adalah matriks yang mendiagonalisasi matriks M. Matriks P dan D diperoleh melalui input SymPy sebagai berikut,

    M = Matrix([[1,2],[3,4]])
    M.diagonalize()

dengan output sebagai berikut,

<img width="458" alt="Screen Shot 2021-07-21 at 11 43 47" src="https://user-images.githubusercontent.com/87349156/126422428-18409490-1846-4eb9-9a93-1b8763651c17.png">

Di mana matriks pada kolom pertama adalah matriks P dan matriks pada kolom kedua adalah matriks D. Dapat kita lihat bahwa matriks D hanya memiliki komponen diagonal yang tidak lain adalah eigen value dari matriks M.

---

## Nilai numerik dari ekspresi analitik

Sejauh ini, kita hanya mengevaluasi ekspresi analitik dari suatu perhitungan. Semisal kita ingin mengevaluasi nilai numerik dari perhitungan berikut,

<img width="344" alt="Screen Shot 2021-07-21 at 11 45 55" src="https://user-images.githubusercontent.com/87349156/126422619-641367ad-c953-46a1-beee-1e6e151b13ea.png">

Untuk mengevaluasi nilai numerik dari fungsi f(x) pada x = 0.1, input pada SymPy adalah,

    f=lambdify(x,diff(x**3*exp(-5*x),x,2))
    f(0.1)
    
Pada baris pertama, kita menggunakan perintah lambdify agar dapat mengevaluasi secara numerik dari suatu fungsi. Argumen pertama pada lambdify adalah variabel fungsi yang akan dievaluasi, sedangkan argumen kedua adalah fungsi yang akan dievaluasi. Baris kedua akan memberikan nilai numerik dari fungsi untuk x = 0.1. Input SymPy di atas akan memberikan output berupa nilai numerik sebagai berikut,

<img width="355" alt="Screen Shot 2021-07-21 at 11 47 22" src="https://user-images.githubusercontent.com/87349156/126422711-3d058c81-a7eb-4715-b7ad-d75b64ef802c.png">

Dengan menggunakan perintah lambdify, kita dapat membuat plot dari ekspresi analitik yang kita peroleh dari SymPy. Input untuk membuat plot adalah sebagai berikut,

    import numpy as np
    import matplotlib.pyplot as plt
    f=lambdify(x,diff(x**3*exp(-5*x),x,2))
    xx = np.linspace(0,5,500)
    yy = f(xx)
    plt.plot( xx,yy)
    plt.tick_params( labelsize  = 18 )
    plt.ylabel('f(x)',size  = 18)
    plt.xlabel('x',size  = 18)
    plt.show()
    
Output dari input di atas adalah berupa plot dari f(x).




 
