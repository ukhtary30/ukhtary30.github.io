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
Baris 1 dan 2 adalah cara memanggil library SymPy, sedangkan baris 3 adalah perintah untuk mendefinisikan variabel dalam perhitungan. Dalam contoh ini, kita menggunakan variable x,y dan z. Semisal kita ingin menghitung $x+z$, maka kita tinggal mengetik seperti baris 5. Berikut, beberapa contoh expresi matematika yang sering dipakai dalam perhitungan.
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

## Limit, Turunan dan Integral
### Limit

Semisal kita ingin menghitung limit dari fungsi berikut,

<img width="528" alt="Screen Shot 2021-07-20 at 15 32 00" src="https://user-images.githubusercontent.com/87349156/126272804-30563d32-35b9-432d-809c-74d5282bba2d.png">

Kita tahu bahwa jawaban dari persamaan (\ref{lim1}) adalah 1. Untuk menghitung persamaan (\ref{lim1}), kita menuliskan input SymPy sebagai berikut,

    limit(sin(x)/x,x,0)
yang memberi output 1. Secara umum, perintah limit terdiri atas tiga argumen. Argumen pertama adalah fungsi yang akan dihitung limitnya, argumen kedua adalah variable dari fungsi tersebut, sedangkan argumen ketiga adalah batas dari limit tersebut. Sebagai contoh lain, semisal kita ingin menghitung limit dari fungsi berikut,

<img width="519" alt="Screen Shot 2021-07-20 at 15 33 25" src="https://user-images.githubusercontent.com/87349156/126272985-550ee95c-4b43-4d42-8f96-85a24578b057.png">

Input pada SymPy adalah sebagai berikut,

    limit((3+4*x)/(5+6*x),x,oo)
    
dengan output $2/3$. oo adalah input untuk $\infty$.
 
 
