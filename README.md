|Nama  | Eka Juliyana Rahayu |
| -----| ------------------ |
|NIM   | 312310594 |
|kelas | TI.23.A6 |
| Mata Kuliah | Pemrograman Web2 |

# Praktikum 1
## Pertanyaan dan Tugas
<p>Lengkapi kode program untuk menu lainnya yang ada pada Controller Page, sehingga semua
link pada navigasi header dapat menampilkan tampilan dengan layout yang sama.</p>
<p>* Controller/Page.php</p>

```
<?php

namespace App\Controllers;

use App\Models\ArtikelModel;

class Page extends BaseController
{
    public function about()
    {
        return view('about', [
            'title'   => 'Halaman About',
            'content' => 'Ini adalah halaman about yang menjelaskan tentang isi halaman ini.'
        ]);
    }

    public function contact()
    {
        $data = [
            'title'   => 'Halaman Kontak',
            'email'   => 'eka610407@gmail.com',
            'alamat'  => 'Sukadami, Cikarang',
            'telepon' => '+62 877-7251-8549'
        ];

        return view('contact', $data);
    }

    public function faqs()
    {
        echo "Ini halaman FAQ";
    }

    public function tos()
    {
        echo "Ini halaman Term of Services";
    }

    // Method untuk menampilkan daftar artikel
    public function artikel()
    {
        $artikelModel = new ArtikelModel();
        
        // Ambil semua artikel dan urutkan dari yang terbaru
        $data['artikel'] = $artikelModel->orderBy('id', 'DESC')->findAll();

        return view('artikel/index', $data);
    }
}
```
## Halaman Kontak
![Screenshot 2025-03-22 105629](https://github.com/user-attachments/assets/39b30349-525b-49e8-a9ba-9190c42988ea)

## Halaman About
![Screenshot 2025-03-22 105609](https://github.com/user-attachments/assets/23729e9d-1e1b-4d5b-96ba-887e7c130dd7)

# Praktikum 2
## Membuat Database: Studi Kasus Data Artikel
<p>* Membuat database</p>

```
CREATE DATABASE lab_ci4;
```
<p>* Membuat Tabel</p>

```
CREATE TABLE artikel (
id INT(11) auto_increment,
judul VARCHAR(200) NOT NULL,
isi TEXT,
gambar VARCHAR(200),
status TINYINT(1) DEFAULT 0,
slug VARCHAR(200),
PRIMARY KEY(id)
);
```
## Konfigurasi koneksi database
<p>* pada file app/config/database.php atau menggunakan
file .env</p>

![Screenshot 2025-03-22 111319](https://github.com/user-attachments/assets/e97029f0-5548-4117-9dbd-6675935963c4)

## Membuat Model
<p>Buat file baru pada
direktori app/Models dengan nama ArtikelModel.php</p>

![Screenshot 2025-03-22 111557](https://github.com/user-attachments/assets/3b42f660-e954-4840-860e-b73a8dff23f4)

## Membuat Controller
<p>Buat Controller baru dengan nama Artikel.php pada direktori app/Controllers.</p>

![Screenshot 2025-03-22 112006](https://github.com/user-attachments/assets/d5348a14-6aa1-4292-81bd-eee2ce4310ad)

## Membuat View
<p>Buat direktori baru dengan nama artikel pada direktori app/views, kemudian buat file baru
dengan nama index.php.</p>

![Screenshot 2025-03-22 112208](https://github.com/user-attachments/assets/a3e04ec2-10aa-485f-810b-29f48c21ecbc)

<p>* tambahkan beberapa data pada database agar
dapat ditampilkan datanya.</p>

```
INSERT INTO artikel (judul, isi, slug) VALUE
('Artikel pertama', 'Lorem Ipsum adalah contoh teks atau dummy dalam industri percetakan dan penataan huruf atau typesetting. Lorem Ipsum telah
menjadi standar contoh teks sejak tahun 1500an, saat seorang tukang cetak
yang tidak dikenal mengambil sebuah kumpulan teks dan mengacaknya untuk
menjadi sebuah buku contoh huruf.', 'artikel-pertama'),
('Artikel kedua', 'Tidak seperti anggapan banyak orang, Lorem Ipsum
bukanlah teks-teks yang diacak. Ia berakar dari sebuah naskah sastra latin
klasik dari era 45 sebelum masehi, hingga bisa dipastikan usianya telah
mencapai lebih dari 2000 tahun.', 'artikel-kedua');
```
## Selanjutnya buka browser kembali dengan mengakses url `http://localhost:8080/artikel`

![Screenshot 2025-03-22 112558](https://github.com/user-attachments/assets/2760860e-e68d-4b94-abb5-11734ff119a6)

## Membuat Tampilan Detail Artikel
<p>Tambahkan fungsi baru pada Controller Artikel dengan nama view().</p>

![Screenshot 2025-03-22 112928](https://github.com/user-attachments/assets/21692572-ab2d-4b9d-82c7-a01d03efc205)

## Membuat View Detail
<p>Buat view baru untuk halaman detail dengan nama app/views/artikel/detail.php.</p>

![Screenshot 2025-03-22 113049](https://github.com/user-attachments/assets/61eee522-a1c1-4dc2-9eae-f72bdba3c23b)

## Membuat Routing untuk artikel detail
<p>Buka Kembali file app/config/Routes.php, kemudian tambahkan routing untuk artikel detail.</p>

```
$routes->get('/artikel/(:any)', 'Artikel::view/$1');
```
![Screenshot 2025-03-22 114145](https://github.com/user-attachments/assets/b968feac-0f56-4c2c-b94f-94e26230ed4d)

## Membuat Menu Admin
<p>Buat method baru pada Controller
Artikel dengan nama admin_index().</p>

![Screenshot 2025-03-22 114443](https://github.com/user-attachments/assets/41b94b4e-8937-4771-8909-c2d2f44db1cf)

<p>Selanjutnya buat view untuk tampilan admin dengan nama admin_index.php</p>

![Screenshot 2025-03-22 114332](https://github.com/user-attachments/assets/a32ca5ee-96e3-4f6b-94f4-9acc530ac590)

<p>Tambahkan routing untuk menu admin seperti berikut:</p>

![Screenshot 2025-03-22 114145](https://github.com/user-attachments/assets/f660ad17-4f7a-41b8-b697-4c9f0b85a898)

Akses menu admin dengan url http://localhost:8080/admin/artikel

![Screenshot 2025-03-22 114838](https://github.com/user-attachments/assets/2fa7ef41-938c-4732-80d3-5f0a7e4e01ee)

## Menambah Data Artikel
Tambahkan fungsi/method baru pada Controller Artikel dengan nama add().

![Screenshot 2025-03-22 114952](https://github.com/user-attachments/assets/742ea2e1-2125-466b-a55c-0bd7718d31e0)

Kemudian buat view untuk form tambah dengan nama form_add.php

![Screenshot 2025-03-22 115120](https://github.com/user-attachments/assets/255ee8dc-a26c-49b7-8fc5-711d102dcb75)

<p>Tampilan </p>

![Screenshot 2025-03-22 115211](https://github.com/user-attachments/assets/271bc7f4-affd-4d90-9a7b-80b0cccbb344)

## Mengubah Data
Tambahkan fungsi/method baru pada Controller Artikel dengan nama edit().

![Screenshot 2025-03-22 115354](https://github.com/user-attachments/assets/5e84c54c-1c30-458f-abf6-571b0fcf4e26)

Kemudian buat view untuk form tambah dengan nama form_edit.php

![Screenshot 2025-03-22 115452](https://github.com/user-attachments/assets/3a5daf9a-b863-4095-9343-696a2c12b99e)

![Screenshot 2025-03-22 115555](https://github.com/user-attachments/assets/11c51146-d6d3-4a14-83f5-f8cc5e1c9a24)

## Menghapus Data
Tambahkan fungsi/method baru pada Controller Artikel dengan nama delete().

![Screenshot 2025-03-22 115752](https://github.com/user-attachments/assets/eb682175-6e77-4903-b3f5-0e010f1a638e)
