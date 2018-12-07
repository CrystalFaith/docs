---
$title: Memonetisasi halaman AMP dengan iklan
---

[TOC]

Panduan ini memberikan petunjuk dan praktik terbaik untuk menampilkan iklan di halaman AMP.

## Menambahkan iklan ke halaman

Di halaman non-AMP (HTML biasa), jika ingin menampilkan iklan di halaman, Anda perlu menyertakan cuplikan JavaScript untuk menayangkan iklan dari jaringan iklan Anda.  Karena alasan performa dan keamanan, Anda tidak dapat menyertakan JavaScript pihak ketiga di halaman AMP.  Oleh karena itu, untuk menampilkan iklan di AMP, Anda perlu menambahkan komponen [`<amp-ad>`](/id/docs/reference/components/amp-ad.html) kustom ke halaman AMP.

{% call callout('Tips', type='success') %}
Lihat [AMP By Example untuk demo langsung](https://ampbyexample.com/components/amp-ad/) yang menunjukkan cara menambahkan tag amp-ad ke halaman AMP.
{% endcall %}

Mari kita ikuti langkah-langkah dalam menambahkan komponen ini agar Anda dapat menampilkan iklan di halaman AMP.

### Langkah 1: Tambahkan skrip amp-ad

Komponen `<amp-ad>` adalah ekstensi iklan kustom untuk library AMP. Di bawah `<amp-ad>` terdapat JavaScript kustom yang dirancang dengan cermat untuk mengoptimalkan performa. Untuk menjalankan komponen `<amp-ad>`, Anda harus menambahkan JavaScript wajib untuk komponen ini di bagian `head` halaman AMP:

```html
<script async custom-element="amp-ad" src="https://cdn.ampproject.org/v0/amp-ad-0.1.js"></script>
```

### Langkah 2: Tambahkan tag amp-ad ke halaman AMP

Lebih dari 100 [server dan jaringan iklan]({{g.doc('/content/docs/ads/ads_vendors.html', locale=doc.locale).url.path}}) menyediakan integrasi bawaan dengan AMP.  Untuk menambahkan iklan pada jaringan iklan tertentu, tambahkan tag `<amp-ad>`, dan tentukan jaringannya dalam atribut `type`.

Pada contoh ini, kita akan menambahkan slot iklan untuk menayangkan iklan dari jaringan a9: 

```html
<amp-ad type="a9">
</amp-ad>
```

### Langkah 3: Tentukan ukuran unit iklannya

Tambahkan atribut `width` dan `height` ke tag `<amp-ad>`.  Atribut ini menentukan ukuran iklan di halaman AMP Anda: 

```html hl_lines="2"
<amp-ad type="a9">
   width="400" height="300"
</amp-ad>
```

### Langkah 4: Tetapkan parameter jaringan iklan

Setiap jaringan memiliki atribut data spesifik yang dibutuhkan untuk menayangkan iklan.  Lihat dokumentasi `<amp-ad>` jaringan iklan dan tambahkan atribut yang diperlukan. Pada contoh berikut, jaringan a9 memerlukan parameter tambahan untuk menentukan ukuran iklan, dan detail lainnya:

```html hl_lines="3 4 5"
<amp-ad type="a9"
    width="400" height="300"
    data-aax_size="300x250"
    data-aax_pubname="test123"
    data-aax_src="302">
</amp-ad>
```

### Langkah 5: (Opsional) Tentukan placeholder 

Bergantung pada jaringan iklannya, Anda dapat memilih untuk menampilkan placeholder sampai iklan tersedia untuk ditayangkan. Hal ini memberikan pengalaman pengguna yang lebih baik dengan mencegah ruang kosong.  Untuk menentukan placeholder, tambahkan elemen turunan dengan atribut `placeholder`. Pelajari lebih lanjut di [Placeholder & fallback]({{g.doc('/content/docs/design/responsive_amp/placeholders.md', locale=doc.locale).url.path}}).

```html hl_lines="6"
<amp-ad type="a9"
    width="400" height="300"
    data-aax_size="300x250"
    data-aax_pubname="test123"
    data-aax_src="302">
   <amp-img placeholder src="placeholder-image.jpg"></amp-img>
</amp-ad>
```

### Langkah 6: (Opsional) Tentukan fallback 

Bergantung pada jaringan iklannya, Anda dapat memilih untuk menampilkan elemen fallback jika tidak ada iklan yang tersedia untuk ditayangkan. Untuk menentukan fallback, tambahkan elemen turunan dengan atribut `fallback`. Pelajari lebih lanjut di [Placeholder & fallback]({{g.doc('/content/docs/design/responsive_amp/placeholders.md', locale=doc.locale).url.path}}).

```html hl_lines="6"
<amp-ad type="a9"
    width="400" height="300"
    data-aax_size="300x250"
    data-aax_pubname="test123"
    data-aax_src="302">
   <amp-img fallback src="fallback-image.jpg"></amp-img>
</amp-ad>
```

Selamat! Sekarang Anda siap menayangkan iklan di halaman AMP!

## Menayangkan iklan AMPHTML yang dijual langsung

Komponen [`amp-ad`](/id/docs/reference/components/amp-ad.html) menayangkan iklan dari jaringan yang Anda tentukan.  Iklan tersebut dapat berupa iklan HTML standar atau iklan AMPHTML, asalkan jaringan iklannya mendukung iklan AMPHTML. Untuk menayangkan iklan yang dijual langsung sebagai iklan AMPHTML, buatlah iklan di AMP HTML sesuai dengan persyaratan [spesifikasi iklan AMPHTML](/id/docs/ads/a4a_spec.html) dan gunakan [server iklan yang menayangkan iklan AMPHTML](https://github.com/ampproject/amphtml/blob/master/ads/google/a4a/docs/a4a-readme.md#publishers).

## Meningkatkan data penargetan pada permintaan iklan

Sebagai bagian dari mekanisme penayangan Fast Fetch, fitur Real-Time Config (RTC) memungkinkan penayang untuk meningkatkan permintaan iklan dengan informasi penargetan pihak pertama dan pihak ketiga yang diambil selama runtime. RTC mendukung hingga 5 pemanggilan ke server penargetan untuk setiap slot iklan individual, yang hasilnya ditambahkan ke akhir permintaan iklan.  Untuk menggunakan RTC pada iklan, jaringan iklan yang Anda gunakan harus mendukung RTC dan Fast Fetch.  

Anda dapat mempelajari lebih lanjut tentang RTC dari video YouTube ini:

{{ youtube('mvAmvKiWPfA', 480, 270, caption='Tonton video tentang Monetisasi AMP yang Efektif dengan Header Bidding.') }}

Atau, pelajari lebih lanjut dari referensi RTC ini:

*   [Panduan implementasi penayang RTC AMP](https://github.com/ampproject/amphtml/blob/master/extensions/amp-a4a/rtc-publisher-implementation-guide.md)
*   [Real Time Config AMP](https://github.com/ampproject/amphtml/blob/master/extensions/amp-a4a/rtc-documentation.md)


## Praktik terbaik

Berikut ini beberapa tips untuk memaksimalkan efektivitas iklan di halaman AMP:


### Penempatan & kontrol: optimalkan penempatan iklan Anda

*   **Tempatkan jumlah iklan yang sama** pada Halaman AMP seperti pada halaman non-AMP untuk menghasilkan pendapatan per halaman yang maksimum.
*   **Tempatkan iklan pertama tepat di bawah viewport pertama** ("paruh bawah") untuk memberikan pengalaman pengguna yang optimal.
*   Kecuali Anda menggunakan CSS lanjutan atau kueri media, **pastikan unit iklan berada di tengah-tengah halaman** untuk memberikan pengalaman web seluler yang optimal kepada pengguna.
*   Aktifkan [permintaan iklan multi-ukuran](https://github.com/ampproject/amphtml/blob/master/ads/README.md#support-for-multi-size-ad-requests) pada inventaris AMP Anda untuk meningkatkan tekanan lelang iklan dan mendorong pendapatan.

### Permintaan & harga: dapatkan harga yang tepat untuk iklan Anda

*   **Jual unit iklan di halaman AMP Anda di seluruh saluran penjualan**, termasuk saluran penjualan langsung dan tidak langsung guna memaksimalkan persaingan untuk inventaris Anda di halaman AMP.
*   **Tetapkan harga inventaris iklan di halaman AMP** yang sama dengan harga untuk inventaris Anda di halaman non-AMP. Pantau performa dan sesuaikan harga berdasarkan pemantauan tersebut.
*   **Pastikan semua saluran permintaan iklan bersaing** untuk inventaris iklan yang ada di halaman AMP guna meningkatkan persaingan.

### Jenis iklan: Tayangkan jenis iklan terbaik

*   **Hindari materi iklan yang berat** sesuai [panduan IAB](http://www.iab.com/wp-content/uploads/2015/11/IAB_Display_Mobile_Creative_Guidelines_HTML5_2015.pdf).
*   **Hindari iklan interstisial** atau format iklan lain yang menyebabkan konten diulang saat iklan dimuat.
*   **Optimalkan visibilitas** dengan mengatur strategi pemuatan data agar lebih mengutamakan visibilitas daripada penayangan.
*   **Tempatkan iklan dalam konten video** melalui [pemutar yang didukung](/id/docs/reference/components.html#media) atau [amp-iframe](https://ampbyexample.com/components/amp-iframe/) untuk mengaktifkan pendapatan pada semua jenis konten.
* **Terapkan iklan native** untuk bersaing dengan iklan display menggunakan permintaan iklan multi-ukuran, yang akan meningkatkan tekanan permintaan sekaligus memberikan pengalaman pengguna premium kepada pembaca Anda.

### Inovasi: Tawarkan produk iklan yang paling menarik

* **Terapkan iklan pada halaman AMP tambahan** untuk menghasilkan pendapatan tambahan:
    *   [Iklan di carousel](https://ampbyexample.com/amp-ads/advanced_ads/carousel_ad/)
    *   [Iklan di lightbox](https://ampbyexample.com/amp-ads/experimental_ads/lightbox_ad/)
    *   ... dan [lain-lain](https://ampbyexample.com/amp-ads/#amp-ads/advanced_ads)
* **Terapkan format baru untuk iklan yang dijual langsung** untuk membekali tim penjualan Anda dengan produk iklan inovatif yang berdampak tinggi:
    *   [Iklan Melekat](https://ampbyexample.com/components/amp-sticky-ad/)
    *   [Flying Carpet](https://ampbyexample.com/components/amp-fx-flying-carpet/)

## Referensi tambahan

*   [Template iklan AMPHTML](https://ampbyexample.com/amp-ads/#amp-ads/advanced_ads)
*   [Demo: Memperlihatkan cara menambah amp-ad ke halaman AMP](https://ampbyexample.com/components/amp-ad/)
 
