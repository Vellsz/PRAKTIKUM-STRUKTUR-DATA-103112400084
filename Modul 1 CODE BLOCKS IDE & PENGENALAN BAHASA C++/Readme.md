
# <h1 align="center">Laporan Praktikum Modul 1 <br> CODE BLOCKS IDE & PENGENALAN BAHASA C++</h1>
<p align="center">NUFAIL ALAUDDIN TSAQIF - 103112400084</p>

## Dasar Teori
Bahasa pemrograman C++ merupakan pengembangan dari bahasa C yang bersifat case sensitive dan memerlukan Integrated Development Environment (IDE) seperti Code::Blocks untuk menulis, mengompilasi, serta menjalankan kode. Struktur fundamental program C++ meliputi penggunaan library seperti <iostream> untuk fungsi input (cin) dan output (cout), serta pendeklarasian variabel dengan tipe data dasar (misalnya int, float, char) dan konstanta (const) untuk menyimpan data. Untuk memanipulasi data dan mengontrol alur program, C++ memanfaatkan beragam operator—seperti aritmatika (+, -, *) dan logika (&&, ||)—serta struktur kontrol kondisional seperti if-else untuk pengambilan keputusan dan perulangan (misalnya for dan while) untuk mengeksekusi blok kode secara berulang berdasarkan kondisi tertentu. 

## Guided

### Aritmatika
```c++
#include <iostream>
using namespace std;
int main()
{
    int W, X, Y;
    float Z;
    X = 7;
    Y = 3;
    W = 1;
    Z = (X + Y) / (Y + W);
    cout << "Nilai z = " << Z << endl;
    return 0;
}
```
> Output
> 
> ![Screenshot bagian x](OUTPUT/aritmatika.png)

Program ini bersifat non-interaktif atau statis. Tidak meminta input: Program ini langsung berjalan tanpa memintamu memasukkan angka apa pun. Perhitungan sudah ditentukan Operasi matematikanya (misalnya, z = 5 - 3;) sudah tertulis di dalam kode. Nilainya sudah pasti dan tidak bisa diubah saat program berjalan. Tujuannya biasanya untuk mendemonstrasikan sebuah perhitungan spesifik atau untuk mendapatkan hasil dari sebuah rumus yang nilainya sudah diketahui. Singkatnya, program ini menjalankan perhitungan yang sudah ditetapkan dari awal dan hanya menampilkan hasilnya.

### Fungsi
```c++
#include <iostream>
using namespace std;

// Prosedur: hanya menampilkan hasil, tidak mengembalikan nilai
void tampilkanHasil(double p, double l)
{
    cout << "\n=== Hasil Perhitungan ===" << endl;
    cout << "Panjang : " << p << endl;
    cout << "Lebar   : " << l << endl;
    cout << "Luas    : " << p * l << endl;
    cout << "Keliling: " << 2 * (p + l) << endl;
}

// Fungsi: mengembalikan nilai luas
double hitungLuas(double p, double l)
{
    return p * l;
}

// Fungsi: mengembalikan nilai keliling
double hitungKeliling(double p, double l)
{
    return 2 * (p + l);
}

int main()
{
    double panjang, lebar;

    cout << "Masukkan panjang: ";
    cin >> panjang;
    cout << "Masukkan lebar  : ";
    cin >> lebar;

    // Panggil fungsi
    double luas = hitungLuas(panjang, lebar);
    double keliling = hitungKeliling(panjang, lebar);

    cout << "\nDihitung dengan fungsi:" << endl;
    cout << "Luas      = " << luas << endl;
    cout << "Keliling  = " << keliling << endl;

    // Panggil prosedur
    tampilkanHasil(panjang, lebar);

    return 0;
}

```

> Output
> 
> ![Screenshot bagian x](OUTPUT/fungsi.png)

Program ini bertugas untuk menghitung luas dan keliling persegi panjang. Kamu hanya perlu memasukkan nilai panjang dan lebar. Program ini menggunakan "fungsi" terpisah untuk masing-masing perhitungan, sehingga kodenya lebih rapi dan terstruktur.

### Kondisi
```c++
int main()
{
    int kode_hari;
    cout << "Menentukan hari kerja/libur\n"<<endl;
    cout << "1=Senin 3=Rabu 5=Jumat 7=Minggu "<<endl;
    cout << "2=Selasa 4=Kamis 6=Sabtu "<<endl;
    cin >> kode_hari;
    switch (kode_hari)
    {
    case 1:
    case 2:
    case 3:
    case 4:
    case 5:
        cout<<"Hari Kerja";
        break;
    case 6:
    case 7:
        cout<<"Hari Libur";
        break;
    default:
        cout<<"Kode masukan salah!!!";
    }
    return 0;
}
```

> Output
> 
> ![Screenshot bagian x](OUTPUT/kondisi.png)

Program ini adalah penentu hari kerja atau hari libur. Kamu memasukkan angka yang mewakili hari (misalnya 1 untuk Senin, 6 untuk Sabtu). Program kemudian akan menggunakan logika if-else atau switch untuk memeriksa angka tersebut dan memberimu output "Hari Kerja" atau "Hari Libur" sesuai aturan yang ditentukan.

### Perulangan
```c++
int main()
{
    int i = 1;
    int jum;
    cin >> jum;
    do
    {
        cout << "bahlil ke-" << (i + 1) << endl;
        i++;
    } while (i < jum);
    return 0;
}
```

> Output
> 
> ![Screenshot bagian x](OUTPUT/perulangan.png)

Program ini menunjukkan cara kerja perulangan (looping). Kamu memasukkan sebuah angka (misalnya 5), dan program akan mencetak sebuah kalimat berulang kali, dari angka 2 sampai angka yang kamu masukkan. Ini berguna untuk melakukan tugas yang sama berkali-kali secara otomatis.

### Struct
```c++
#include <iostream>
#include <string>
using namespace std;

// Definisi struct
struct Mahasiswa {
    string nama;
    string nim;
    float ipk;
};

int main() {

    Mahasiswa mhs1;

    cout << "Masukkan Nama Mahasiswa: ";
    getline(cin, mhs1.nama);
    // cin >> mhs1.nama;
    cout << "Masukkan NIM Mahasiswa : ";
    cin >> mhs1.nim;
    cout << "Masukkan IPK Mahasiswa : ";
    cin >> mhs1.ipk;

    cout << "\n=== Data Mahasiswa ===" << endl;
    cout << "Nama : " << mhs1.nama << endl;
    cout << "NIM  : " << mhs1.nim << endl;
    cout << "IPK  : " << mhs1.ipk << endl;

    return 0;
}

```

> Output
> 
> ![Screenshot bagian x](OUTPUT/struct.png)

Program ini berfungsi seperti formulir digital untuk data mahasiswa. Kamu akan diminta mengisi: Nama, NIM, IPK, Data tersebut kemudian disimpan dalam sebuah struct, yaitu sebuah "wadah" yang bisa menampung berbagai jenis data yang saling berhubungan. Setelah diisi, program akan menampilkan kembali data yang sudah kamu masukkan.

### Test
```c++
#include <iostream>
using namespace std;
int main()
{
    string ch;
    cout << "Masukkan sebuah karakter: ";
    // cin >> ch;
    ch = getchar();  //Menggunakan getchar() untuk membaca satu karakter
    cout << "Karakter yang Anda masukkan adalah: " << ch << endl;
    return 0;
}

```
> Output
> 
> ![Screenshot bagian x](OUTPUT/testcpp.png)

Program ini dirancang untuk membaca satu karakter saja. Walaupun kamu mengetik "Kelapa Muda", program hanya akan mengambil dan menampilkan huruf pertamanya, yaitu 'K'. Ini menunjukkan cara kerja input dasar untuk tipe data karakter (char) di C++

## Unguided

### Soal 1

> ![Screenshot bagian x](SOAL/GSoal1.png)

```c++
#include <iostream>
using namespace std;

int main() {

  float angka1, angka2;

  cout << "Masukkan angka pertama: ";
  cin >> angka1;

  cout << "Masukkan angka kedua: ";
  cin >> angka2;

  cout << "Penjumlahan : " << angka1 + angka2 << endl;
  cout << "Pengurangan : " << angka1 - angka2 << endl;
  cout << "Perkalian   : " << angka1 * angka2 << endl;
  cout << "Pembagian   : " << angka1 / angka2 << endl;

  return 0;
}
```

> Output
> 
> ![Screenshot bagian x](OUTPUT/unguided1.png)

Program ini seperti kalkulator dasar. Kamu memasukkan dua angka, lalu program akan otomatis melakukan empat operasi matematika dasar:
Penjumlahan (+), Pengurangan (-), Perkalian (*), Pembagian (/), Hasil dari setiap operasi kemudian ditampilkan di layar. Program aritmatika.png juga melakukan hal serupa, yaitu menghitung nilai menggunakan operasi matematika dan menampilkan hasilnya.

### Soal 2

> ![Screenshot bagian x](SOAL/GSoal2.png)

```c++
#include <iostream>
#include <string>

using namespace std;

string ubahKeTeks(int nomor) {
    string satuan[] = {"", "satu", "dua", "tiga", "empat", "lima", "enam", "tujuh", "delapan", "sembilan"};

    if (nomor < 0 || nomor > 100) {
        return "Input tidak valid. Harap masukkan angka antara 0 dan 100.";
    }

    if (nomor == 0) return "nol";
    if (nomor == 100) return "seratus";
    if (nomor == 10) return "sepuluh";
    if (nomor == 11) return "sebelas";

    if (nomor < 10) {
        return satuan[nomor];
    } else if (nomor < 20) {
        return satuan[nomor % 10] + " belas";
    } else {
        int puluhan = nomor / 10;
        int sisa = nomor % 10;

        string hasil = satuan[puluhan] + " puluh";
        if (sisa > 0) {
            hasil += " " + satuan[sisa];
        }
        return hasil;
    }
}

int main() {
    int angka;
    cout << "Masukkan angka (0-100): ";
    cin >> angka;

    // Memanggil fungsi untuk melakukan konversi
    string tulisan = ubahKeTeks(angka);

    cout << "Output: " << angka << " : " << tulisan << endl;

    return 0;
}
```

> Output
> 
> ![Screenshot bagian x](OUTPUT/unguided2.png)

Ini adalah program penerjemah angka menjadi tulisan. Kamu memasukkan sebuah angka (contohnya 79), dan program akan mengubahnya menjadi format teks dalam bahasa Indonesia, yaitu "tujuh puluh sembilan".

### Soal 3

> ![Screenshot bagian x](SOAL/GSoal3.png)
> 
```c++
#include <iostream>

using namespace std;

int main() {
    int n;
    cout << "Input: ";
    cin >> n;
    cout << "Output:" << endl;

    for (int baris = 0; baris < n; baris++) {
        for (int spasi = 0; spasi < baris; spasi++) {
            cout << "  ";
        }
        int angka_maks = n - baris;
        for (int j = angka_maks; j >= 1; j--) {
            cout << j << " ";
        }
        cout << "* ";
        for (int j = 1; j <= angka_maks; j++) {
            cout << j << " ";
        }
        cout << endl;
    }
    for (int k = 0; k < n; k++) {
        cout << "  ";
    }
    cout << "*" << endl;

    return 0;
}
```

> Output
> 
> ![Screenshot bagian x](OUTPUT/unguided3.png)

Program ini adalah contoh kreativitas menggunakan perulangan bersarang (nested loop). Kamu memasukkan satu angka, dan program akan menggunakan angka tersebut sebagai titik awal untuk menggambar pola segitiga simetris yang unik menggunakan angka dan simbol bintang *.

## Referensi

1. https://www.learncpp.com/ (diakses pada 27 september 2025)
2. https://www.w3schools.com/cpp/ (diakses pada 27 september 2025)
