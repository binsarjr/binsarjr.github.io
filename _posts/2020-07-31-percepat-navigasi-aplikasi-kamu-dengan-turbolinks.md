---
title: "Percepat navigasi aplikasi kamu dengan Turbolinks"
layout: single
categories: Turbolinks
tags: [Tutorial,Cara mempercepat navigasi]
canonical_url: "https://yoursite.com/custom-canonical-url"
---

Turbolinks adalah pengoptimalan yang meningkatkan kinerja yang dipersepsikan dengan menjadi pintar dalam berpindah halaman dan memuat ulang aset di aplikasi kamu.
Tidak seperti permintaan `GET`, turbolinks tidak memerlukan perubahan pada kode di aplikasi kamu sendiri.

# Turbolinks 5
Turbolinks 5 adalah pustaka JavaScript murni yang dapat digunakan pada halaman HTML apa pun yang menaruhnya di tag `<script>` pada halaman tersebut, atau memasukkannya ke dalam JavaScript.

Ketika dijalankan, Turbolinks akan secara otomatis menemukan semua tautan yang mengarah ke domain yang sama, dan melampirkan events `click`. Setiap klik pada tautan tersebut akan dicegat. Alih-alih mengikuti tautan seperti biasa, ia meminta halaman yang ditautkan di latar belakang melalui JavaScript menggunakan `XMLHttpRequest`. Kemudian, empat hal terjadi:

- Salinan halaman saat ini disimpan dalam cache Turbolinks untuk digunakan nanti
- Turbolinks menggantikan `<body>` halaman saat ini dengan `<body>` dari hasil XHR
- Turbolinks menggabungkan `<head>` halaman saat ini dengan `<head>` dari hasil XHR
- Turbolinks mengubah URL di browser menggunakan History API

Dengan menggabungkan tag `<head>`, browser tidak perlu memuat ulang dan merender aset seperti file CSS dan JavaScript yang ada di kedua halaman. Ini dapat mempercepat aplikasi Anda secara signifikan, terutama jika Anda memiliki banyak aset yang digunakan kembali di sebagian besar halaman Anda.

![Turbolinks 5 (xhr)]({{ site.url }}/assets/turbolinks-xhr.png)

Kamu dapat melihat Turbolinks beraksi dengan menavigasi sekitar dengan mengklik tautan dan menekan tombol kembali. Di tab `Network` browser Anda, Anda akan melihat permintaan untuk halaman yang dimuat melalui Turbolinks ditandai sebagai `"xhr"`. aset kamu juga tidak akan dimuat ulang untuk setiap permintaan.

# Caching and page previews

Untuk mempercepat permintaan berikutnya ke halaman yang sama, Turbolinks menyimpan cache dari halaman yang baru saja dikunjungi. Ini memungkinkan merender halaman sebelumnya segera ketika menekan tombol kembali.

Untuk mempercepat kinerja halaman lambat yang dirasakan, Turbolinks akan menampilkan pratinjau halaman jika ada dalam cache. Setelah mengklik tautan, versi yang di-cache ditampilkan sementara versi yang baru dimuat.

# Peringatan

Turbolinks menambahkan kembali beberapa fitur default browser Anda, sehingga beberapa hal berfungsi berbeda dengan Turbolinks diaktifkan daripada tanpa.
`turbolinks: load` dan tag `<script>`

Karena halaman tidak diperbarui setelah setiap klik tautan, memuat JavaScript pada halaman memuat menggunakan `window.onload` atau `DOMContentLoaded` tidak berfungsi lagi. Untuk memperbaikinya, Turbolinks menggunakan event `turbolinks: load`, yang dapat Anda gunakan sebagai gantinya:

```js
document.addEventListener("turbolinks:load", function() {
  // ...
})
```

# Browser loading

Saat berpindah antar halaman, browser tidak akan menampilkan indikator memuat di browser Anda karena permintaan dieksekusi di latar belakang.

Dalam upaya untuk memperbaikinya, Turbolinks akan menampilkan progress bar (yang dapat ditata dengan CSS) di bagian atas halaman setelah 500 milidetik untuk menunjukkan bahwa halaman dimuat.

## Apa selanjutnya ?

1.  [Percepat navigasi aplikasi anda dengan Turbolinks ]({% post_url 2020-07-31-percepat-navigasi-aplikasi-kamu-dengan-turbolinks %})
2.  Cara mengunakan turbolinks
3.  Masalah umum yang sering ditemui ketika menggunakan turbolinks

Nantikan blog terbaru mengenai turbolinks lainnya.

<!-- # Masalah yang berpotensi dengan Turbolinks

Ada kasus di mana ia akan gagal, dan ketika itu terjadi, itu bisa sangat sulit untuk di-debug. Berikut ini adalah beberapa skenario kegagalan yang lebih umum, dan cara untuk menghindarinya.

# Bekerja dengan Third-Library
Ketika kamu menggunakan library pihak ketiga misalnya `DataTables` dalam beberapa kasus kamu akan menemukan kesalahan -->