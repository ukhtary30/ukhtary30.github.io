# Tutorial penggunaan Github secara remote

Berikut saya berikan beberapa kode untuk mengupdate Github secara remote melalui Git. Halaman ini saya buat sebagai pengingat untuk saya pribadi, karena sering lupa :flushed:

## Mengunduh suatu repositori

Untuk berkolaborasi dalam suatu repositori, kita harus mengunduh repositori tersebut ke komputer lokal kita. Perintah untuk mengunduh adalah,

    git clone (link web dari repositori)
    
Sebagai contoh saya ingin mengunduh repositori dengan link web: https://github.com/ukhtary30/dummyrep.git

    git clone https://github.com/ukhtary30/dummyrep.git
    
Link web dari repositori dapat di lihat pada,

<img width="1302" alt="Screen Shot 2021-07-24 at 11 27 18" src="https://user-images.githubusercontent.com/87349156/126854977-e6d0376e-ab02-4943-aadd-71106516d3ef.png">

---

## Mengupdate perubahan dari komputer lokal ke Github

Setelah mendownload repositori, maka kita dapat melakukan perubahan secara lokal. Setelah melakukan perubahan, kita harus mengunggah perubahan tersebut ke repositori yang ada di Github. Untuk melihat file apa saja yang berubah di komputer lokal, maka kita bisa menggunakan perintah

    git status

Setelah mengetahui file apa saja yang berubah, maka kota dapat menambahkan file tersebut untuk diunggah ke Github. Perintah pertama adalah menambahkan file apa yang akan diunggah

    git add (nama file)
    
Bila tidak ingin menambahkan file satu persatu, maka bisa menggunakan perintah di bawah,

    git add --all

setelah menambahkan filenya, kita melakukan perintah commit untuk file yang sudah ditambahkan. 

    git commit -m "(isi dengan suatu pesan, yang berkaitan dengan perubahan yang dilakukan)"
    
Terakhir, kita mengunggah file tersebut dengan perintah

    git push origin (branch repositori, atau bila tidak ada branch, isikan dengan main)
    
## Mengunduh perubahan yang dilakukan langsung di Github

Bila perubahan dilakukan langsung di web Github, dan kita ingin menunduh ke komputer lokal kita, maka perintah yang diketikan adalah 


