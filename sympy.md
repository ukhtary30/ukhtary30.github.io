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
