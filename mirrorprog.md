# Metode Transfer Matrix method untuk mirror structure

Berikut adalah penjelasan mengenai program yang saya gunakan dalam paper saya: [Significant enhancement of light absorption in undoped graphene using dielectric multilayer system](http://aip.scitation.org/doi/abs/10.1063/1.5012604) , S. A. Nulli, **M. S. Ukhtary**, R. Saito, Appl. Phys. Lett. 112, 073101 (2018). Ringkasan mengenai paper ini ada pada halaman berikut: [Cerita Riset](https://ukhtary30.github.io/significant.html). Kode program dapat ditemukan pada repositori Github: https://github.com/ukhtary30/transfer-matrix.git

---

### Penjelasan bagian - bagian kode

Bagian utama dari program ini adalah bagian perhitungan probabilitas serapan cahaya dan besar medan listrik menggunakan metode transfer matrix, yang merupakan perkalian antara matriks matching dan propagasi.


Matriks matching antara medium n<sub>i+1</sub> and n<sub>i</sub> diberikan oleh kode di bawah ini,

    def M(x,y): #x is n_i+1, y is n_i
    A = 1 + x / y
    B = 1 - x / y
    return 0.5 * np.array([[A,B],[B,A]])

yang memberikan mtriks matching M<sub>i</sub>,

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


By inputting the number of repetition and the value of the refractive index of medium B, the absorption and electric field on graphene are calculated as a function of α.

The code, 

    nb   = 1.5 # the refractive index of B medium

gives the input for the refractive index of medium B.

The following code gives the input for the umber of repetitions that will be calculated.

    ##########################################
    # The input for the number of repetitions that will be calculated.

    s1 = 2
    s2 = 3
    s3 = 5

    ##########################################
  
 The outputs are plotted by the following code,
 
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
     

