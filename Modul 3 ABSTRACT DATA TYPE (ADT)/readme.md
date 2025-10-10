# <h1 align="center">Laporan Praktikum Modul 3 <br> ABSTRACT DATA TYPE</h1>
<p align="center">NUFAIL ALAUDDIN TSAQIF - 103112400084</p>

## Dasar Teori
Abstract Data Type (ADT) adalah model konseptual atau teoretis dalam ilmu komputer yang mendefinisikan sebuah tipe data berdasarkan kumpulan nilai yang dapat dimiliki dan kumpulan operasi yang dapat dilakukan terhadap nilai tersebut. Hal yang paling fundamental dari ADT adalah pemisahan antara spesifikasi (apa yang dilakukan oleh tipe data) dan implementasi (bagaimana hal itu dilakukan). Dengan kata lain, ADT berfokus pada perilaku sebuah tipe data dari sudut pandang pengguna, tanpa perlu mengetahui detail internal cara kerja atau bagaimana data tersebut disimpan dalam memori.

Prinsip utamanya adalah abstraksi, yang menyembunyikan kompleksitas dan detail implementasi. Analogi yang sering digunakan adalah sebuah mobil. Sebagai pengemudi, Anda berinteraksi dengan mobil melalui antarmuka yang jelas seperti setir, pedal gas, dan rem. Anda tahu operasi apa yang bisa dilakukan (berbelok, mempercepat, berhenti), tetapi Anda tidak perlu tahu bagaimana mesin pembakaran internal atau sistem rem hidrolik bekerja di baliknya. Antarmuka tersebut adalah spesifikasi ADT, sementara mesin dan komponen internalnya adalah implementasi yang tersembunyi.

Dalam praktik pemrograman, konsep ADT ini sering diwujudkan menggunakan class dalam paradigma pemrograman berorientasi objek (OOP). Di dalam sebuah class, member variables (atribut) yang menyimpan data biasanya dijadikan private (implementasi yang tersembunyi), sedangkan member functions (metode) yang mendefinisikan operasi yang valid dijadikan public (antarmuka yang dapat diakses pengguna). Pendekatan ini disebut enkapsulasi. Penggunaan ADT memungkinkan kode menjadi lebih modular, mudah dipelihara, dan dapat digunakan kembali (reusable), karena perubahan pada detail implementasi tidak akan memengaruhi bagian lain dari program selama antarmukanya tetap konsisten.

## Guided

### mahasiswa.h
```c++
#ifndef MAHASISWA_H_INCLUDED
#define MAHASISWA_H_INCLUDED
struct mahasiswa
{
    char nim[10];
    int nilai1, nilai2;
};
void inputMhs(mahasiswa &m);
float rata2(mahasiswa m);
#endif
```

### mahasiswa.cpp
```c++
#ifndef MAHASISWA_H_INCLUDED
#define MAHASISWA_H_INCLUDED
struct mahasiswa
{
    char nim[10];
    int nilai1, nilai2;
};
void inputMhs(mahasiswa &m);
float rata2(mahasiswa m);
#endif
```

### main.cpp
```c++
#include <iostream>
#include "mahasiswa.h"
using namespace std;

int main()
{
    mahasiswa mhs;
    inputMhs(mhs);
    cout << "rata - rata = " << rata2(mhs);
    return 0;
} 
```
> Output
> 
> ![Screenshot bagian x](OUTPUT/guided1.png)

Program ini adalah aplikasi C++ sederhana yang terstruktur dalam tiga file untuk mengelola data seorang mahasiswa. File header mahasiswa.h mendefinisikan struct untuk menyimpan NIM dan dua nilai beserta deklarasi fungsinya, sementara mahasiswa.cpp berisi logika untuk menginput data dan menghitung rata-rata. Alur programnya sendiri dikontrol dari main.cpp, di mana sebuah variabel mahasiswa dibuat, lalu diisi dengan data dari pengguna melalui fungsi inputMhs, dan akhirnya nilai rata-ratanya dihitung menggunakan fungsi rata2 sebelum hasilnya ditampilkan ke layar.

## Unguided

### Soal 1

Buat program yang dapat menyimpan data mahasiswa (max. 10) ke dalam sebuah array
dengan field nama, nim, uts, uas, tugas, dan nilai akhir. Nilai akhir diperoleh dari FUNGSI
dengan rumus 0.3*uts+0.4*uas+0.3*tugas.

### unguided1.h
```c++
#ifndef MAHASISWA_H
#define MAHASISWA_H

#include <string>
using namespace std;

class Mahasiswa {
private:
    string nama;
    string nim;
    float uts;
    float uas;
    float tugas;
    float nilaiAkhir;

public:
    Mahasiswa();
    void inputData();
    void hitungNilaiAkhir();
    void tampilkanData() const;
};

#endif // MAHASISWA_H
```
### unguided1.cpp
```c++
#include "unguided1.h"
#include <iostream>
#include <limits>
using namespace std;

Mahasiswa::Mahasiswa() : uts(0), uas(0), tugas(0), nilaiAkhir(0) {}

void Mahasiswa::inputData() {
    cout << "Nama      : ";
    cin.ignore(numeric_limits<streamsize>::max(), '\n');
    getline(cin, nama);

    cout << "NIM       : ";
    cin >> nim;

    cout << "Nilai UTS : ";
    cin >> uts;

    cout << "Nilai UAS : ";
    cin >> uas;

    cout << "Nilai Tugas: ";
    cin >> tugas;
}

void Mahasiswa::hitungNilaiAkhir() {
    nilaiAkhir = (0.3 * uts) + (0.4 * uas) + (0.3 * tugas);
}

void Mahasiswa::tampilkanData() const {
    cout << "Nama        : " << nama << endl;
    cout << "NIM         : " << nim << endl;
    cout << "Nilai Akhir : " << nilaiAkhir << endl;
}
```
### main.cpp
```c++
#include "unguided1.h"
#include <iostream>

using namespace std;

int main() {
    Mahasiswa daftarMahasiswa[10];
    int jumlahMahasiswa = 0;
    char lanjut;

    do {
        if (jumlahMahasiswa >= 10) {
            cout << "Kapasitas maksimal mahasiswa telah tercapai." << endl;
            break;
        }

        cout << "\nMasukkan Data Mahasiswa ke-" << jumlahMahasiswa + 1 << ":" << endl;
        
        daftarMahasiswa[jumlahMahasiswa].inputData();
        daftarMahasiswa[jumlahMahasiswa].hitungNilaiAkhir();

        jumlahMahasiswa++;

        cout << "\nTambah data lagi? (y/n): ";
        cin >> lanjut;

    } while (lanjut == 'y' || lanjut == 'Y');

    cout << "\n===== Data Lengkap Mahasiswa =====" << endl;
    
    for (int i = 0; i < jumlahMahasiswa; ++i) {
        cout << "----------------------------------" << endl;
        daftarMahasiswa[i].tampilkanData();
    }
    cout << "----------------------------------" << endl;

    return 0;
}
```
> Output
> 
> ![Screenshot bagian x](OUTPUT/unguided1ifx.png)

Program ini merupakan aplikasi C++ untuk mengelola data nilai mahasiswa yang kodenya diorganisir ke dalam tiga file terpisah. File header unguided1.h mendefinisikan struktur (struct) Mahasiswa yang berisi data seperti nama, NIM, dan nilai-nilai ujian. File implementasi unguided1.cpp berisi logika dari fungsi-fungsi yang dideklarasikan di header, seperti fungsi untuk menginput data dan fungsi untuk menghitung nilai akhir secara otomatis berdasarkan bobot nilai UTS, UAS, dan tugas. Terakhir, file main.cpp bertindak sebagai program utama yang mengontrol alur, yaitu dengan membuat sebuah array untuk menampung hingga 10 mahasiswa, kemudian secara berulang meminta input data pengguna hingga selesai, dan akhirnya menampilkan kembali seluruh data mahasiswa yang tersimpan beserta hasil nilai akhirnya ke layar.

### Soal 2

> ![Screenshot bagian x](OUTPUT/soal2.png)

### unguided2.h
```c++
#ifndef PELAJARAN_H
#define PELAJARAN_H

#include <string>
using namespace std;

class Pelajaran {
private:
    string namaMapel;
    string kodeMapel;

public:
    Pelajaran(string nama, string kode);
    void tampilkanInfo() const;
};

#endif 
```
### unguided2.cpp
```c++
#include "unguided2.h"
#include <iostream>
using namespace std;

Pelajaran::Pelajaran(string nama, string kode) {
    namaMapel = nama;
    kodeMapel = kode;
}

void Pelajaran::tampilkanInfo() const {
    cout << "nama pelajaran: " << namaMapel << endl;
    cout << "kode: " << kodeMapel << endl;
}
```
### main.cpp
```c++
#include "unguided2.h"
#include <iostream>
using namespace std;

int main() {
    Pelajaran pel("Struktur Data", "STD");

    pel.tampilkanInfo();

    return 0;
}
```

> Output
> 
> ![Screenshot bagian x](OUTPUT/unguided2.png)

Program C++ ini didesain secara prosedural untuk mengelola data mata pelajaran dan kodenya diorganisir ke dalam tiga file terpisah. File header (unguided2.h) mendefinisikan sebuah struct bernama Pelajaran untuk membungkus data nama dan kode mata pelajaran. File implementasi (unguided2.cpp) berisi logika dari dua fungsi: create_pelajaran yang bertugas membuat sebuah struct Pelajaran baru, dan tampil_pelajaran yang berfungsi untuk menampilkannya ke layar. Alur program utama pada main.cpp kemudian memanggil fungsi create_pelajaran untuk membuat data pelajaran "Struktur Data", lalu hasilnya dilewatkan ke fungsi tampil_pelajaran untuk dicetak ke konsol.

### Soal 3

Buatlah program dengan ketentuan :
- 2 buah array 2D integer berukuran 3x3 dan 2 buah pointer integer
- fungsi/prosedur yang menampilkan isi sebuah array integer 2D
- fungsi/prosedur yang akan menukarkan isi dari 2 array integer 2D pada posisi tertentu
- fungsi/prosedur yang akan menukarkan isi dari variabel yang ditunjuk oleh 2 buah pointer

### unguided2.h
```c++
#ifndef MATRIX_H
#define MATRIX_H

#include <iostream>

class Matrix {
private:
    int data[3][3];

public:
    Matrix(int arr[3][3]);
    void tampilkan() const;
    void tukarElemen(Matrix& other, int baris, int kolom);
};

void tukarNilaiPointer(int* ptr1, int* ptr2);

#endif
```
### unguided2.cpp
```c++
#include "unguided3.h"

Matrix::Matrix(int arr[3][3]) {
    for (int i = 0; i < 3; ++i) {
        for (int j = 0; j < 3; ++j) {
            data[i][j] = arr[i][j];
        }
    }
}

void Matrix::tampilkan() const {
    for (int i = 0; i < 3; ++i) {
        for (int j = 0; j < 3; ++j) {
            std::cout << data[i][j] << "\t";
        }
        std::cout << std::endl;
    }
}

void Matrix::tukarElemen(Matrix& other, int baris, int kolom) {
    if (baris >= 0 && baris < 3 && kolom >= 0 && kolom < 3) {
        int temp = this->data[baris][kolom];
        this->data[baris][kolom] = other.data[baris][kolom];
        other.data[baris][kolom] = temp;
    }
}

void tukarNilaiPointer(int* ptr1, int* ptr2) {
    int temp = *ptr1;
    *ptr1 = *ptr2;
    *ptr2 = temp;
}
```
### main.cpp
```c++
#include "unguided3.h"
#include <iostream>

int main() {
    using namespace std;

    int dataA[3][3] = { {1, 2, 3}, {4, 5, 6}, {7, 8, 9} };
    int dataB[3][3] = { {10, 20, 30}, {40, 50, 60}, {70, 80, 90} };

    Matrix matA(dataA);
    Matrix matB(dataB);

    cout << " Matrix Sebelum Ditukar " << endl;
    cout << "Matrix A:" << endl;
    matA.tampilkan();
    cout << "\nMatrix B:" << endl;
    matB.tampilkan();

    matA.tukarElemen(matB, 1, 1);

    cout << "\n Matrix Setelah Ditukar " << endl;
    cout << "Matrix A:" << endl;
    matA.tampilkan();
    cout << "\nMatrix B:" << endl;
    matB.tampilkan();
    
    cout << "\n================================\n" << endl;

    int var1 = 100;
    int var2 = 200;

    cout << "Nilai pointer sebelum ditukar: " << var1 << " & " << var2 << endl;
    
    tukarNilaiPointer(&var1, &var2);
    
    cout << "Nilai pointer setelah ditukar: " << var1 << " & " << var2 << endl;
    
    return 0;
}
```

> Output
> 
> ![Screenshot bagian x](OUTPUT/unguided3.png)

Program C++ ini didesain secara prosedural untuk mendemonstrasikan operasi pada array dua dimensi (matriks) dan pointer, dengan kodenya yang terorganisir ke dalam tiga file terpisah. File header unguided3.h mendeklarasikan tiga fungsi, yang kemudian diimplementasikan dalam unguided3.cpp untuk menampilkan matriks, menukar elemen tertentu di antara dua matriks, dan menukar nilai yang ditunjuk oleh dua pointer. Program utama di main.cpp menginisialisasi dua matriks 3x3 dan dua variabel integer, kemudian memanggil fungsi-fungsi tersebut untuk menampilkan data awal, menukar sebuah elemen antar matriks dan nilai antar variabel pointer, lalu menampilkan hasilnya setelah pertukaran.

## Referensi

1. https://www.geeksforgeeks.org/abstract-data-types/ (diakses pada 9 Oktober 2025)
2. https://www.tutorialspoint.com/data_structures_algorithms/abstract_data_type.htm (diakses pada 9 Oktober 2025)
3. https://www.programiz.com/dsa/abstract-data-type (diakses pada 9 Oktober 2025)
