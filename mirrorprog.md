<a href="https://ukhtary30.github.io"><img align="right" width="50" height="50" src="figures/home.png"></a>

# Metode transfer matrix untuk mirror structure

Berikut adalah penjelasan mengenai program yang saya gunakan dalam paper saya: [Significant enhancement of light absorption in undoped graphene using dielectric multilayer system](http://aip.scitation.org/doi/abs/10.1063/1.5012604) , S. A. Nulli, **M. S. Ukhtary**, R. Saito, Appl. Phys. Lett. 112, 073101 (2018). Ringkasan mengenai paper ini ada pada halaman berikut: [Cerita Riset](https://ukhtary30.github.io/significant.html). Kode program dapat ditemukan pada repositori Github: https://github.com/ukhtary30/transfer-matrix.git

---

### Penjelasan bagian - bagian kode

Bagian utama dari program ini adalah bagian perhitungan probabilitas serapan cahaya dan besar medan listrik menggunakan metode transfer matrix, yang merupakan perkalian antara matriks matching dan propagasi. Penjelasan mengenai kedua matriks tersebut dapat dibaca di rangkuman paper ini pada halaman [Cerita Riset](https://ukhtary30.github.io/significant.html)

Matriks matching antara medium n<sub>i+1</sub> and n<sub>i</sub> diberikan oleh kode di bawah ini,

    def M(x,y): #x is n_i+1, y is n_i
    A = 1 + x / y
    B = 1 - x / y
    return 0.5 * np.array([[A,B],[B,A]])

yang memberikan matriks matching M<sub>i</sub>,

<img width="360" alt="Screen Shot 2021-07-27 at 9 55 36" src="https://user-images.githubusercontent.com/87349156/127078053-95a2074f-e276-4b88-8ea1-ccfe5e9ce04b.png">

Bila graphene diletakan di antara kedua media, maka matriks matching menjadi,

    def MG(x,y,z): #x is n_i+1, y is n_i, z is the conductivity
    k = 2 * np.pi * y / (lmbd)
    A = 1 + x / y + k * z / (omega * eps0 * y * y)
    B = 1 - x / y + k * z / (omega * eps0 * y * y)
    C = 1 - x / y - k * z / (omega * eps0 * y * y)
    D = 1 + x / y - k * z / (omega * eps0 * y * y)
    return 0.5 * np.array([[A,B],[C,D]])

yang memberikan,

<img width="516" alt="Screen Shot 2021-07-27 at 10 00 13" src="https://user-images.githubusercontent.com/87349156/127078330-1d0e0065-b10f-49ac-bfe7-8eaae9fc93e8.png">

di mana suku tambahan di setiap komponen matriks berisi konduktivitas graphene.

Matriks propagasi di dalam medium n<sub>i</sub>　diberikan oleh kode di bawah ini,

    def P(x,d): # x is the n_i, d is the thickness
    k = 2 * np.pi * x / (lmbd)
    A = 1j * k * d
    return np.array([[np.exp(-A),0],[0,np.exp(A)]])
 
 yang memberikan matriks propagasi di dalam medium n<sub>i</sub>, 
 
 <img width="240" alt="Screen Shot 2021-07-27 at 10 02 13" src="https://user-images.githubusercontent.com/87349156/127078478-52287170-02d4-4f5c-ad12-16f9df346871.png">
 
Di paper ini, ketebalan tiap medium (d<sub>i</sub>) adalah seperempat panjang gelombang dalam medium 

---

Transfer matriks dari mirror structure dengan jumlah repetisi s di berikan oleh kode di bawah ini,

    def TF(x,s): # x is the alpha and s is the repetition
    na = x * nb
    d1 = lmbd / (4 * na)
    d2 = lmbd / (4 * nb)
    J1 = M(na,1)  @ P(na,d1) @ M(nb,na) @ P(nb,d2)
    J2 = M(na,nb) @ P(na,d1) @ M(nb,na) @ P(nb,d2)
    J3 = P(nb,d2) @ M(na,nb) @ P(na,d1) @ M(nb,na)
    J4 = P(nb,d2) @ M(na,nb) @ P(na,d1) @ M(1,na)
    JT = J1 @ matrix_power(J2,s-1) @ MG(nb,nb,sig) @ matrix_power(J3,s-1) @ J4
    return JT
    
Matriks J1 berkaitan dengan penjalaran cahaya ketika memasuki struktur dari udara ke medium A dan B (udara --> AB). Sebaliknya, matriks J4 berkaitan dengan penjalaran cahaya meninggalkan struktur dari medium BA ke udara (BA --> udara). Perlu diperhatikan bahwa kode @ memberikan perkalian matriks.

Matriks matrix_power(J2,s-1) berkaitan dengan penjalaran cahaya melalui medium AB yang berulang sebelum mencapai graphene yang berada di tengah struktur. Sebaliknya matriks matrix_power(J3,s-1) berkaitan dengan penjalaran cahaya melalui medium BA yang berulang sesudah melewati graphene. Kode matrix_power(J2,s-1) memberikan bentuk pangkat dari matriks J2 dengan orde s-1.

---

### Output program

Input dari program ini adalah jumlah repetisi s dan juga nilai indeks bias medium B. Output dari program ini adalah besarnya probabilitas serapan cahaya dan besar medan listrik pada graphene sebagai fungsi rasio antara indeks bias medium A dan B (α) untuk beberapa s. 

Kode di bawah ini memberikan input dari indeks bias medium B, 

    nb   = 1.5 # the refractive index of B medium

Kode di bawah ini memberikan input dari jumlah repetisi s yang akan digunakan dalam perhitungan.

    ##########################################
    # The input for the number of repetitions that will be calculated.

    s1 = 2
    s2 = 3
    s3 = 5

    ##########################################
  
Output dari program ini divisualisasikan dalam bentuk grafik dengan kode di bawah ini.
 
```
nd = 100 # number of data
AB1 = np.zeros(nd+1) # the data for absorption in percent for s1
EE1 = np.zeros(nd+1) # the data for electric field for s1
AB2 = np.zeros(nd+1) # the data for absorption in percent for s2
EE2 = np.zeros(nd+1) # the data for electric field for s2
AB3 = np.zeros(nd+1) # the data for absorption in percent for s3
EE3 = np.zeros(nd+1) # the data for electric field for s3
AA = np.zeros(nd+1) # the data for alpha

for i in range (nd+1):
    AA[i]    = (6 - 1 ) * i/nd + 1
    AB1[i]    = ap(AA[i],s1) * 100
    EE1[i]    = ec(AA[i],s1)
    AB2[i]    = ap(AA[i],s2) * 100
    EE2[i]    = ec(AA[i],s2)
    AB3[i]    = ap(AA[i],s3) * 100
    EE3[i]    = ec(AA[i],s3)

# absorption as a function of alpha
    
plt.plot( AA, AB1, 'k',label='s = 2')
plt.plot( AA, AB2, 'r',label='s = 3')
plt.plot( AA, AB3, 'g',label='s = 5')
plt.tick_params( labelsize  = 18 )
plt.ylabel('Absorption [%]',size  = 18)
plt.xlabel('α',size  = 18)
plt.xlim([1,6])
plt.ylim([0,50])
plt.legend()
plt.show()

# electric field as a function of alpha

plt.plot( AA, EE1, 'k',label='s = 2'  )
plt.plot( AA, EE2, 'r',label='s = 3')
plt.plot( AA, EE3, 'g',label='s = 5')
plt.tick_params( labelsize  = 18 )
plt.ylabel('|E/$E_0$| ',size  = 18)
plt.xlabel('α',size  = 18)
plt.xlim([1,6])
plt.ylim([0,5])
plt.legend()
plt.show()
```

Berikut adalah grafik serapan cahaya dan besar medan listrik pada graphene sebagai fungsi α untuk beberapa repetisi s (Grafik 3a dan b di paper)

![Unknown-39](https://user-images.githubusercontent.com/87349156/127585093-c0318cc8-e3b5-4833-a355-4c94bd0cf0ea.png)

![Unknown-40](https://user-images.githubusercontent.com/87349156/127585100-016b0a44-548b-4d22-b3bb-1199c36b238b.png)

---

Penurunan formula analitis dari serapan cahaya dan medan listrik diberikan di supplemental material paper. Formula analitis dari α yang memberikan serapan maksimum dapat diperoleh dengan melakukan turunan dari formula analitis serapan cahata. Turunan dapat diperoleh menggunakan kode SymPy sebagai berikut,

```
#################################################

# The derivation of the analytical results is given in the supplemental material of the paper. Here we will plot the value of alpha that gives the maximum absorption as a function of s


# Let us use sympy

import sympy
sympy.init_session()
s, al, Z0, sigm = symbols("s alpha Z0 sigma")

A = 4 * al**(2*s)* Z0 * sigm / (2 + al**(2*s) *Z0 * sigm)**2 # the analytical formula for Absorption
B = diff(A,al) # derivative of A
amax = solve(B,al)[0] # the analytical solution of alpha that gives maximum absorption

```
Formula analitis dari alpha diberikan oleh kode amax di atas, yang memberikan,

<img width="137" alt="Screen Shot 2021-07-30 at 13 23 11" src="https://user-images.githubusercontent.com/87349156/127599902-d362cbcf-ee9d-4041-9639-39e91d79c1f5.png">

Grafik dari alpha sebagai fungsi s diberikan oleh kode di bawah ini,

```
##### Ploting the amax
f=lambdify(s,amax.subs([(Z0,377),(sigm,sig)]))
xx = np.linspace(2,12,100)
yy = f(xx)
plt.plot( xx,yy)
plt.tick_params( labelsize  = 18 )
plt.ylabel('$α_{max}$',size  = 18)
plt.xlabel('s',size  = 18)
plt.xlim([2,12])
plt.ylim([1,3.5])
plt.show()
```
dengan output (Grafik 3c di paper),

![alphamax](https://user-images.githubusercontent.com/87349156/127600588-ad81bf6c-dc1c-4f73-9cf9-3715cec77f17.png)



