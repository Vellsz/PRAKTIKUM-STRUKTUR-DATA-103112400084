# <h1 align="center">Laporan Praktikum Modul 5 <br> SINGLY LINKED LIST (BAGIAN KEDUA)</h1>
<p align="center">NUFAIL ALAUDDIN TSAQIF - 103112400084</p>

## Dasar Teori
Singly Linked List (SLL) adalah struktur data linear dinamis yang terdiri dari sekumpulan elemen yang disebut node. Setiap node dalam SLL secara fundamental memiliki dua bagian: sebuah infotype yang menyimpan data aktual, dan sebuah pointer (next) yang menyimpan alamat memori dari node berikutnya dalam urutan. Keseluruhan struktur list ini diidentifikasi oleh satu pointer kepala, yang biasa disebut first atau head, yang menunjuk ke node pertama. Jika pointer first ini bernilai Nil (atau NULL), maka list tersebut dianggap kosong. Berbeda dengan array, node-node dalam linked list tidak disimpan secara berurutan (kontigu) di memori, melainkan terhubung secara logis melalui pointer.

Operasi searching (pencarian) adalah salah satu operasi dasar paling penting dalam singly linked list. Karena linked list tidak mendukung akses acak (seperti akses via indeks pada array), satu-satunya metode pencarian yang dapat diimplementasikan secara efisien adalah pencarian linear (atau linear search). Algoritma pencarian linear bekerja dengan cara mengunjungi atau melintasi (traversing) setiap node satu per satu, dimulai dari node first. Proses ini menggunakan sebuah pointer temporer (misalnya current) yang awalnya diinisialisasi ke first. Kemudian, algoritma masuk ke dalam sebuah perulangan yang akan terus berjalan selama pointer temporer tidak Nil (yang menandakan akhir dari list). Di dalam perulangan, data pada node yang sedang ditunjuk (current->info) dibandingkan dengan nilai X yang dicari. Jika data ditemukan (cocok), perulangan berhenti dan fungsi akan mengembalikan address dari node tersebut. Jika data tidak cocok, pointer temporer akan diperbarui untuk menunjuk ke node berikutnya (current = current->next), dan proses perbandingan diulang. Jika perulangan selesai (mencapai akhir list) tanpa menemukan kecocokan, fungsi akan mengembalikan Nil, menandakan bahwa data tidak ada di dalam list. Operasi pencarian ini menjadi fondasi krusial untuk operasi lain seperti insertAfter, deleteAfter, dan update, karena operasi-operasi tersebut perlu menemukan node atau posisi spesifik terlebih dahulu sebelum dapat dieksekusi.

## Guided

### Guided 1
```c++
#include <iostream>
using namespace std;

// Struktur Node
struct Node {
    int data;
    Node* next;
};

// Pointer awal dan akhir
Node* head = nullptr;

// Fungsi untuk membuat node baru
Node* createNode(int data) {
    Node* newNode = new Node();
    newNode->data = data;
    newNode->next = nullptr;
    return newNode;
}

void insertDepan(int data) {
    Node* newNode = createNode(data);
    newNode->next = head;
    head = newNode;
    cout << "Data " << data << " berhasil ditambahkan di depan.\n";
}

void insertBelakang(int data) {
    Node* newNode = createNode(data);
    if (head == nullptr) {
        head = newNode;
    } else {
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }
    cout << "Data " << data << " berhasil ditambahkan di belakang.\n";
}

void insertSetelah(int target, int dataBaru) {
    Node* temp = head;
    while (temp != nullptr && temp->data != target) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << target << " tidak ditemukan!\n";
    } else {
        Node* newNode = createNode(dataBaru);
        newNode->next = temp->next;
        temp->next = newNode;
        cout << "Data " << dataBaru << " berhasil disisipkan setelah " << target << ".\n";
    }
}

// ========== DELETE FUNCTION ==========
void hapusNode(int data) {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = head;
    Node* prev = nullptr;

    // Jika data di node pertama
    if (temp != nullptr && temp->data == data) {
        head = temp->next;
        delete temp;
        cout << "Data " << data << " berhasil dihapus.\n";
        return;
    }

    // Cari node yang akan dihapus
    while (temp != nullptr && temp->data != data) {
        prev = temp;
        temp = temp->next;
    }

    // Jika data tidak ditemukan
    if (temp == nullptr) {
        cout << "Data " << data << " tidak ditemukan!\n";
        return;
    }

    prev->next = temp->next;
    delete temp;
    cout << "Data " << data << " berhasil dihapus.\n";
}

// ========== UPDATE FUNCTION ==========
void updateNode(int dataLama, int dataBaru) {
    Node* temp = head;
    while (temp != nullptr && temp->data != dataLama) {
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "Data " << dataLama << " tidak ditemukan!\n";
    } else {
        temp->data = dataBaru;
        cout << "Data " << dataLama << " berhasil diupdate menjadi " << dataBaru << ".\n";
    }
}

// ========== DISPLAY FUNCTION ==========
void tampilkanList() {
    if (head == nullptr) {
        cout << "List kosong!\n";
        return;
    }

    Node* temp = head;
    cout << "Isi Linked List: ";
    while (temp != nullptr) {
        cout << temp->data << " -> ";
        temp = temp->next;
    }
    cout << "NULL\n";
}

void searchData(int key) {
    Node* temp = head;
    int pos = 1;
    bool found = false;

    if (head == nullptr) {
        cout << "List kosong! Tidak ada data yang bisa dicari.\n";
        return;
    }

    while (temp != nullptr) {
        if (temp->data == key) {
            cout << "Data " << key << " ditemukan pada posisi ke-" << pos << endl;
            found = true;
            break;
        }
        temp = temp->next;
        pos++;
    }

    if (!found) {
        cout << "Data " << key << " tidak ditemukan dalam list.\n";
    }
}

// ========== MAIN PROGRAM ==========
int main() {
    int pilihan, data, target, dataBaru;

    do {
        cout << "\n=== MENU SINGLE LINKED LIST ===\n";
        cout << "1. Insert Depan\n";
        cout << "2. Insert Belakang\n";
        cout << "3. Insert Setelah\n";
        cout << "4. Hapus Data\n";
        cout << "5. Update Data\n";
        cout << "6. Tampilkan List\n";
        cout << "7. Cari Data\n";
        cout << "0. Keluar\n";
        cout << "Pilih: ";
        cin >> pilihan;

        switch (pilihan) {
            case 1:
                cout << "Masukkan data: ";
                cin >> data;
                insertDepan(data);
                break;
            case 2:
                cout << "Masukkan data: ";
                cin >> data;
                insertBelakang(data);
                break;
            case 3:
                cout << "Masukkan data target: ";
                cin >> target;
                cout << "Masukkan data baru: ";
                cin >> dataBaru;
                insertSetelah(target, dataBaru);
                break;
            case 4:
                cout << "Masukkan data yang ingin dihapus: ";
                cin >> data;
                hapusNode(data);
                break;
            case 5:
                cout << "Masukkan data lama: ";
                cin >> data;
                cout << "Masukkan data baru: ";
                cin >> dataBaru;
                updateNode(data, dataBaru);
                break;
            case 6:
                tampilkanList();
                break;
            case 7:
                cout << "Masukkan data yang ingin dicari: ";
                cin >> data;
                searchData(data);
                break;
            case 0:
                cout << "Program selesai \n";
                break;
            default:
                cout << "Pilihan tidak valid!\n";
        }
    } while (pilihan != 0);

    return 0;
}
```

> Output
> 
> ![Screenshot bagian x](OUTPUT/guided1.png)

Program pencarian ini, yang diimplementasikan dalam fungsi searchData, bekerja dengan cara menerima satu nilai integer (key) yang ingin dicari. Fungsi ini akan memulai penelusuran dari node pertama (head) dan bergerak maju satu per satu ke node berikutnya, sambil melacak posisi saat ini (dimulai dari 1). Jika nilai data di node yang sedang diperiksa sama dengan key yang dicari, program akan mencetak pesan sukses yang menyatakan data ditemukan beserta nomor posisinya, lalu pencarian dihentikan. Apabila penelusuran sudah mencapai akhir list (NULL) tanpa menemukan data tersebut, atau jika list-nya memang kosong, program akan menampilkan pesan bahwa data tidak ditemukan.

### Soal 1

buatlah searcing untuk mencari nama pembeli pada unguided sebelumnya

```c++


```

> Output
> 
> ![Screenshot bagian x](OUTPUT/unguided2.png)

pencarian pada program ini (fungsi searchData) bekerja dengan cara menerima satu nilai integer (key) yang ingin dicari. Fungsi ini akan memulai penelusuran dari node pertama (head) dan bergerak maju satu per satu ke node berikutnya, sambil melacak posisi saat ini (dimulai dari 1). Jika nilai data di node yang sedang diperiksa sama dengan key yang dicari, program akan mencetak pesan sukses yang menyatakan data ditemukan beserta nomor posisinya, lalu pencarian dihentikan. Apabila penelusuran sudah mencapai akhir list (NULL) tanpa menemukan data tersebut, atau jika list-nya memang kosong, program akan menampilkan pesan bahwa data tidak ditemukan.

### Soal 2
gunakan latihan pada pertemuan minggun ini dan tambahkan seardhing untuk mencari buku berdasarkan judul, penulis, dan ISBN

```c++
#include <iostream>
#include <string>

using namespace std;

struct Buku {
    string isbn;
    string judul;
    string penulis;
};

struct Node {
    Buku data;
    Node* next;
};

Node* head = nullptr;

void tambahBuku();
void hapusBuku();
void perbaruiBuku();
void lihatBuku();
void cariBuku();
void bersihkanMemori();

int main() {
    int pilihan;

    do {
        cout << "\nMENU PERPUSTAKAAN LINKED LIST\n";
        cout << "1. Tambah Buku\n";
        cout << "2. Hapus Buku (berdasarkan ISBN)\n";
        cout << "3. Perbarui Buku (berdasarkan ISBN)\n";
        cout << "4. Lihat Semua Buku\n";
        cout << "5. Cari Buku\n";
        cout << "6. Keluar\n";
        cout << "Pilih menu: ";
        cin >> pilihan;
        cin.ignore(); 

        switch (pilihan) {
            case 1:
                tambahBuku();
                break;
            case 2:
                hapusBuku();
                break;
            case 3:
                perbaruiBuku();
                break;
            case 4:
                lihatBuku();
                break;
            case 5:
                cariBuku();
                break;
            case 6:
                cout << "Membersihkan memori dan keluar...\n";
                break;
            default:
                cout << "Pilihan tidak valid. Silakan coba lagi.\n";
        }
    } while (pilihan != 6);

    bersihkanMemori(); 
    return 0;
}

void tambahBuku() {
    Buku bukuBaru;
    cout << "Masukkan ISBN: ";
    getline(cin, bukuBaru.isbn);
    cout << "Masukkan Judul: ";
    getline(cin, bukuBaru.judul);
    cout << "Masukkan Penulis: ";
    getline(cin, bukuBaru.penulis);

    Node* newNode = new Node{bukuBaru, nullptr};

    if (head == nullptr) {
        head = newNode;
    } else {
        Node* temp = head;
        while (temp->next != nullptr) {
            temp = temp->next;
        }
        temp->next = newNode;
    }
    cout << "\n>> Buku '" << bukuBaru.judul << "' berhasil ditambahkan." << endl;
}

void lihatBuku() {
    if (head == nullptr) {
        cout << "\n>> Perpustakaan kosong." << endl;
        return;
    }

    cout << "\nDAFTAR SEMUA BUKU\n";
    Node* temp = head;
    int nomor = 1;
    while (temp != nullptr) {
        cout << nomor << ". ISBN     : " << temp->data.isbn << endl;
        cout << "   Judul    : " << temp->data.judul << endl;
        cout << "   Penulis  : " << temp->data.penulis << endl;
        temp = temp->next;
        nomor++;
    }
}

void perbaruiBuku() {
    if (head == nullptr) {
        cout << "\n>> Perpustakaan kosong." << endl;
        return;
    }

    string isbnCari;
    cout << "Masukkan ISBN buku yang ingin diperbarui: ";
    getline(cin, isbnCari);

    Node* temp = head;
    while (temp != nullptr) {
        if (temp->data.isbn == isbnCari) {
            cout << "Buku ditemukan! Masukkan data baru:\n";
            cout << "Masukkan Judul Baru: ";
            getline(cin, temp->data.judul);
            cout << "Masukkan Penulis Baru: ";
            getline(cin, temp->data.penulis);
            cout << "\n>> Data buku berhasil diperbarui." << endl;
            return;
        }
        temp = temp->next;
    }
    cout << "\n>> Buku dengan ISBN " << isbnCari << " tidak ditemukan." << endl;
}

void hapusBuku() {
    if (head == nullptr) {
        cout << "\n>> Perpustakaan kosong." << endl;
        return;
    }
    
    string isbnCari;
    cout << "Masukkan ISBN buku yang akan dihapus: ";
    getline(cin, isbnCari);

    Node* temp = head;
    Node* prev = nullptr;

    if (temp != nullptr && temp->data.isbn == isbnCari) {
        head = temp->next;
        delete temp;
        cout << "\n>> Buku berhasil dihapus." << endl;
        return;
    }

    while (temp != nullptr && temp->data.isbn != isbnCari) {
        prev = temp;
        temp = temp->next;
    }

    if (temp == nullptr) {
        cout << "\n>> Buku dengan ISBN " << isbnCari << " tidak ditemukan." << endl;
        return;
    }

    prev->next = temp->next;
    delete temp;
    cout << "\n>> Buku berhasil dihapus." << endl;
}

void cariBuku() {
    if (head == nullptr) {
        cout << "\n>> Perpustakaan kosong. Tidak bisa mencari." << endl;
        return;
    }

    int pilihanCari;
    cout << "\nCARI BUKU BERDASARKAN\n";
    cout << "1. ISBN\n";
    cout << "2. Judul\n";
    cout << "3. Penulis\n";
    cout << "Pilih kriteria: ";
    cin >> pilihanCari;
    cin.ignore(); 

    string searchTerm;
    switch (pilihanCari) {
        case 1:
            cout << "Masukkan ISBN yang dicari: ";
            getline(cin, searchTerm);
            break;
        case 2:
            cout << "Masukkan Judul yang dicari: ";
            getline(cin, searchTerm);
            break;
        case 3:
            cout << "Masukkan Penulis yang dicari: ";
            getline(cin, searchTerm);
            break;
        default:
            cout << "Pilihan tidak valid.\n";
            return;
    }

    Node* temp = head;
    bool ditemukan = false;
    int nomor = 1;

    cout << "\nHASIL PENCARIAN\n";
    while (temp != nullptr) {
        bool match = false;
        if (pilihanCari == 1 && temp->data.isbn == searchTerm) {
            match = true;
        } else if (pilihanCari == 2 && temp->data.judul == searchTerm) {
            match = true;
        } else if (pilihanCari == 3 && temp->data.penulis == searchTerm) {
            match = true;
        }

        if (match) {
            cout << nomor << ". ISBN     : " << temp->data.isbn << endl;
            cout << "   Judul    : " << temp->data.judul << endl;
            cout << "   Penulis  : " << temp->data.penulis << endl;
            ditemukan = true;
            nomor++;
        }
        temp = temp->next;
    }

    if (!ditemukan) {
        cout << ">> Buku tidak ditemukan." << endl;
    }
}

void bersihkanMemori() {
    Node* current = head;
    while (current != nullptr) {
        Node* nextNode = current->next;
        delete current;
        current = nextNode;
    }
    head = nullptr; 
}

```

> Output
> 
> ![Screenshot bagian x](OUTPUT/unguided2.png)

Fungsi pencarian (cariBuku) pada program ini memberikan pengguna tiga pilihan kriteria untuk mencari buku: berdasarkan ISBN, Judul, atau Penulis. Setelah pengguna memilih kriteria dan memasukkan kata kunci pencarian (misalnya, judul "durian runtuh"), program akan melakukan penelusuran (traversal) ke seluruh linked list dari buku pertama (head) hingga buku terakhir. Untuk setiap buku yang ditemui, program akan membandingkan data pada buku tersebut (ISBN, judul, atau penulis) dengan kata kunci yang dicari. Jika terjadi kecocokan, program akan mencetak seluruh detail buku tersebut (ISBN, Judul, dan Penulis) dan melanjutkan pencarian ke buku berikutnya, sehingga program ini dapat menemukan dan menampilkan lebih dari satu hasil jika ada beberapa buku yang sesuai kriteria (misalnya, semua buku karya penulis "nufail"). Apabila program telah memeriksa seluruh daftar dan tidak menemukan satu pun kecocokan, barulah program akan menampilkan pesan bahwa buku tidak ditemukan.

## Referensi

1. https://www.geeksforgeeks.org/cpp/cpp-program-for-searching-an-element-in-a-linked-list/ (diakses pada 20 Oktober 2025)
2. https://www.tutorialspoint.com/searching-an-element-in-a-linked-list-using-cplusplus (diakses pada 20 Oktober 2025)
3. https://www.programiz.com/dsa/linear-search (diakses pada 18 Oktober 2025)
