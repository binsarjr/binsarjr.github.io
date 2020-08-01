---
title: "Belajar Turbolinks - Bagaimana cara menggunakannya"
layout: single
categories: Turbolinks
tags: [Cara mempercepat navigasi website]
keywords: [
  tutorial,
  cara mempercepat navigasi website,
  turbolinks,
  cara meningkatkan kecepatan navigasi website,
  cara membuat website seperti SPA,
  tutorial turbolinks,
  cara menggunakan turbolinks,
  turbolink tutorial
  ]
---

Dalam blog ini, kami akan membagikan 4 langkah sederhana yang kamu butuhkan di aplikasi kamu untuk mempercepat navigasi dengan mengaktifkan Turbolinks. Ini akan mempercepat situs web kamu untuk merender halaman dengan cepat.

# Apa itu Turbolinks ?
Turbolinks adalah pengoptimalan yang meningkatkan kinerja yang dipersepsikan dengan menjadi pintar dalam berpindah halaman dan memuat ulang aset di aplikasi kamu.

Penjelasan tentang turbolinks secara lengkap sudah saya jelaskan [disini]({% post_url 2020-07-31-percepat-navigasi-aplikasi-kamu-dengan-turbolinks %}).

## Hasil akhir ketika menggunakan Turbolinks
### Dengan Turbolinks
![Hasil akhir ketika menggunakan Turbolinks]({{ site.url }}/assets/dengan-turbolinks.gif)
### Tanpa Turbolinks
![Hasil akhir ketika menggunakan Turbolinks]({{ site.url }}/assets/tanpa-turbolinks.gif)

Mungkin kamu tidak begitu melihat perbedaanya karena saya mencobanya di localhost.Namun, kamu bisa mengecek secara langsung website yang menggunakan Turbolinks yaitu salah satunya [Cookpad](https://cookpad.com) atau website [Ngeblog Skuy](https://binsarjr.github.io/) ini sendiri. Disable/Enable kan javascript nya untuk melihat perbedaan.

Mari kita mulai langkah langkahnya

1. [**Install Turbolinks menggunakan NPM**](#langkah-1---install-turbolink-menggunakan-npm)
2. [**Cara memanggil dan menjalankan turbolinks**](#langkah-2---cara-memanggil-dan-menjalankan-turbolinks)
3. [**Verifikasi semua halaman yang akan dimuat oleh Turbolinks**](#langkah-3---verifikasi-semua-halaman-yang-akan-dimuat-oleh-turbolinks)
4. [**Nonaktifkan cache pada halaman**](#langkah-4---nonaktifkan-cache-pada-halaman)

## Langkah 1 - install Turbolink menggunakan NPM
```bash
npm install turbolinks
```
<small>*Penjelasan & tutorial NPM akan dibahas dilain waktu, nantikan blog terbaru lainnya.*</small>

"Kok pake npm bang,pake versi cdn dari cdnjs bisa tidak?", kata netizen.
Jawabannya belum tentu bisa karena saya sendiri sudah pernah mencobanya dan hasilnya nihil.Jadi,saya tetap menyarankan instalasinya menggunakan NPM

## Langkah 2 - cara memanggil dan menjalankan turbolinks
Buatlah file dengan struktur seperti berikut
```
.
├── index2.html
├── index.html
└── js
    └── script.js
```
Karena kita hanya akan mempelajari cara menggunakan `Turbolinks`. Kita hanya akan membuat kode html sederhana pada file `index.html` dan `index2.html` dengan kode:
```html
<!-- index.html & index2.html -->
<!DOCTYPE html>
<html>
<head>
    <title>Belajar Turbolinks</title>
    <script src="js/script.js"></script>
</head>
<body>
    <h1>Halaman 1</h1>
    <ul>
        <li><a href="index.html">Halaman 1</a></li>
        <li><a href="index2.html">Halaman 2</a></li>
    </ul>
</body>
</html>
```
Ubah sedikit kode pada file `index2.html` guna melihat perbedaan dari kedua file tersebut yang awalnya
```html
<h1>Halaman 1</h1>
```
menjadi
```html
<h1>Halaman 2</h1>
```

sehingga file `index2.html` akan terlihat seperti ini
```html
<!-- index2.html -->
<!DOCTYPE html>
<html>
<head>
    <title>Belajar Turbolinks</title>
    <script src="js/script.js"></script>
</head>
<body>
    <h1>Halaman 2</h1>
    <ul>
        <li><a href="index.html">Halaman 1</a></li>
        <li><a href="index2.html">Halaman 2</a></li>
    </ul>
</body>
</html>
```

Cara memanggil turbolinks sendiri ada 2 cara yaitu menggunakan `require javascript` atau  menggunakan tag `<script>`

### Cara pertama - menggunakan require javascript
Cara ini disarankan untuk kamu yang sudah terbiasa bermain dengan NPM.
Tambahkan kode dibawah ini ke file `script.js` pada folder `js` yang telah dibuat sebelumnya
```js
var Turbolinks = require('turbolinks');
if(Turbolinks.supported) {
    Turbolinks.start()
} else {
    console.warn("browser kamu tidak mendukung `Turbolinks`")
}
```
<small>*Gunakan cara kedua apabila kamu masih bingung dengan cara ini.*</small>

### Cara kedua - menggunakan tag `<script>`
Cari file `turbolinks.js` dengan struktur folder seperti berikut
```
.
└── node_modules
    └── turbolinks
        └── dist
            └── turbolinks.js
```
dan copy-kan file tersebut ke folder `js` yang sudah kita buat sebelumnya.
Tambahkan kode dibawah ini di semua file html kamu didalam tag `<head>`
```html
<!-- index.html & index2.html -->
<script src="js/turbolinks.js"></script>
```
lalu, buka file `script.js` pada folder `js` dan tambahkan kode berikut
```js
// js/script.js
if(Turbolinks.supported) {
    Turbolinks.start()
} else {
    console.warn("browser kamu tidak mendukung `Turbolinks`")
}
```

dan Turbolinks sudah berhasil dijalankan

## Langkah 3 - verifikasi semua halaman yang akan dimuat oleh Turbolinks
Jika, ada halaman yang tidak ingin anda proses dengan turbolinks.Maka, tambahkan `data-turbolinks="false"` untuk memberitahu turbolinks bahwa halaman tersebut tidak perlu diproses olehnya.

Sebelum itu,buatlah file html baru dengan nama `index3.html` dengan kode
```html
<!-- index3.html -->
<!DOCTYPE html>
<html>
<head>
    <title>Belajar Turbolinks</title>
    <script src="js/script.js"></script>
</head>
<body>
    <h1>Halaman 3</h1>
    <ul>
        <li><a href="index.html">Halaman 1</a></li>
        <li><a href="index2.html">Halaman 2</a></li>
        <li><a href="index3.html">Halaman 3</a></li>
    </ul>
</body>
</html>
```
lalu, tambahkan `data-turbolinks="false"` pada tag anchor Halaman 3 yang awalnya
```html
<li><a href="index3.html">Halaman 3</a></li>
```
menjadi 
```html
<li><a href="index3.html" data-turbolinks="false">Halaman 3</a></li>
```
dengan ini setiap kali kamu ingin pergi kehalaman 3 browser akan melakukan navigasi seperti biasanya tanpa melibatkan turbolinks

## Langkah 4 - Nonaktifkan cache pada halaman
Dalam beberapa kasus, ketika kamu menggunakan turbolinks dan bermain dengan DOM ataupun web dinamis. Kamu akan menemukan hasil yang tidak diinginkan seperti adanya tombol yang terduplikasi adanya tombol yang seharusnya tidak ditampilkan dll.

Ini disebabkan karena secara default turbolinks menyimpan halaman kamu kedalam cache guna meningkatkan performa yang bagus untuk pengguna. seperti yang telah dijelaskan [disini](https://github.com/turbolinks/turbolinks#understanding-caching)

Untuk menonaktifkanya kamu hanya perlu menambahkan kode

`<meta name="turbolinks-cache-control" content="no-cache">`

pada bagian `<head>` di kode html kamu

# Kesimpulan
Jika, kamu menginnginkan aplikasi yang rasanya seperti SPA yang akan membuat navigasi menjadi sangat cepat gunakanlah [Turbolinks](https://github.com/turbolinks/turbolinks#understanding-caching).

Sampai sekarang, Turbolinks merupakan Ruby on Rails, tetapi masih bagus untuk menggunakannya di aplikasi lainnya dan meningkatkan pengalaman pengguna. SPA itu bagus, tetapi mereka tidak SEO Friendly. Jika, pengaturan Server Side Rendering terlalu banyak bekerja untuk aplikasi kamu maka, saya merekomendasikan kamu untuk menggunakan Turbolinks pada aplikasi kamu.