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
