# <h1 align="center">Tugas 3 Struktur Data</h1>
<p align="center">Rifka Annisa Swasthi</p>

## 1. Priority Queue

Queue adalah struktur data linear yang mengikuti prinsip FIFO (First In, First Out). Dalam struktur ini, elemen yang pertama kali dimasukkan akan dikeluarkan pertama kali. FIFO digunakan untuk membuat buffer sederhana yang menampung paket-paket sementara waktu. FIFO memiliki beberapa karakteristik, antara lain:

Cepat dan sederhana karena tidak melakukan klasifikasi.
Merupakan solusi umum yang banyak digunakan.
Menggunakan satu buffer untuk berbagai jenis paket.
Sulit memperkirakan kemacetan.
Memungkinkan terjadinya penundaan yang lebih lama.
Sering mengalami kondisi paket terbuang (drop packet).
Pada queue FIFO, elemen pertama yang masuk atau dikeluarkan disebut Front atau Head, sedangkan elemen terakhir disebut Back, Rear, atau Tail. Proses penambahan elemen dinamakan Enqueue, dan proses penghilangan elemen disebut Dequeue[1].

Jenis-Jenis Queue[2]

Berdasarkan Implementasinya:

Linear/Simple Queue: Penghapusan atau penambahan elemen hanya terjadi di dua ujung barisan.
Circular Queue: Ujung-ujung barisan terhubung, membentuk struktur antrean melingkar.
Berdasarkan Penggunaannya:

Priority Queue: Elemen dengan prioritas tertinggi diambil terlebih dahulu.
Double-ended Queue: Elemen bisa ditambahkan atau dihapus dari kedua ujung antrean.
Queue dapat direpresentasikan dengan dua cara:

Array: Menggunakan penunjuk rear dan front, array memiliki akses cepat ke elemen berdasarkan indeks, namun ukuran tetapnya tidak fleksibel.
Linked List: Terdiri dari node-node yang terhubung, setiap node memiliki dua bagian, yaitu data dan pointer ke node berikutnya. Linked list memungkinkan penambahan dan penghapusan elemen dengan lebih fleksibel, namun memiliki overhead memori untuk menyimpan pointer tambahan.
Operasi dasar pada Queue[3]:

a. Enqueue: Menambahkan elemen ke dalam Queue.
b. Dequeue: Menghapus elemen dari Queue.
c. Front: Mendapatkan elemen pertama dalam Queue.
d. Rear: Mendapatkan elemen terakhir dalam Queue.
e. IsEmpty: Memeriksa apakah Queue kosong.
f. Size: Mendapatkan jumlah elemen dalam Queue.


### Contoh Kode

```C++
#include <iostream>
#include<algorithm>

int H[50];
int heapsize = -1;

int parent(int i) {
    return (i-1) /2;
}

int leftchild(int i) {
    return ((2 * i) +1);
}

int rightchild(int i){
    return ((2*i) + 2);
}

void shiftup (int i) {
    while (i > 0 && H[parent(i)] < H[i]){
        std :: swap(H[parent(i)], H[i]);
        i= parent(i);
    }
}

void shiftdown (int i) {
    int mmaxindex = i;
    int l = leftchild(i);
    if (l <= heapsize && H[l] > H [mmaxindex]) {
        mmaxindex = l;
    }
    int r = rightchild(i);
    if (r <= heapsize && H[r] > H[mmaxindex]){
        mmaxindex = r;
    }
    if (i != mmaxindex){
        std :: swap (H[i], H[mmaxindex]);
        shiftdown(mmaxindex);
    }
}

void insert( int p){
    heapsize = heapsize +1;
    H[heapsize] = p;
    shiftup(heapsize);
}

int extractmax() {
    int result = H[0];
    H[0] = H[heapsize];
    heapsize = heapsize -1;
    shiftdown(0);
    return result;
}
 void changepriority (int i, int p) {
    int oldp = H[i];
    H[i] = p;
    if (p > oldp) {
        shiftup (i);
    } else {
        shiftdown (i);
    }
 }

int getmax(){
    return H[0];
}

void remove(int i){
    H[i] = getmax() +1;
    shiftup(i);
    extractmax();
}

int main(){
    insert(45);
    insert(20);
    insert(14);
    insert(12);
    insert(31);
    insert(7);
    insert(11);
    insert(13);
    insert(7);

    std :: cout << "priority queue :";
    for ( int i =0; i<= heapsize; ++i){
        std :: cout << H[i] << "";
    }
    std :: cout << "\n";
    std :: cout << "node with maximum priority :" << extractmax() << "\n";
    std :: cout << "priority queue after estracting maximum:";
    for ( int i = 0; i <= heapsize; i++){
        std :: cout << H[i] << " ";
    }
    std :: cout << "\n";

    changepriority(2, 49);
    std :: cout << "priority queue after priority change:";
    for ( int i = 0; i <= heapsize; i++){
        std :: cout << H[i] << " ";
    }
    std:: cout <<"\n";

    remove(3);
    std :: cout << "priority queue after removing teh element:";
    for ( int i = 0; i <= heapsize; i++){
        std :: cout << H[i] << " ";
    }
    return 0;
}


```
Kode di atas digunakan untuk mencetak teks "ini adalah file code guided praktikan" ke layar menggunakan function cout untuk mengeksekusi nya.

## 2. Hash Table

Hash table adalah struktur data yang menggunakan array untuk menyimpan data, dengan setiap nilai data memiliki indeks unik. Fungsi utama hash table adalah mempercepat akses data karena array menawarkan efisiensi dalam operasi waktu.

Dalam hash table, hashing adalah proses mengubah kunci atau string karakter menjadi nilai lain. Linear probing digunakan untuk mengatasi tabrakan (collision) ketika dua kunci di-mapping ke indeks yang sama. Dalam kasus ini, linear probing mencari lokasi kosong terdekat dalam tabel dan menempatkan kunci baru di sana.[4]

Operasi utama dalam hash table meliputi pencarian, penyisipan, penghapusan, dan pembaruan elemen data. Pencarian dilakukan berdasarkan kunci atau indeks, sedangkan penyisipan menambahkan elemen baru ke dalam tabel. Penghapusan menghilangkan elemen dari tabel, dan pembaruan mengubah nilai elemen yang sudah ada.[5]

Penanganan tabrakan sangat penting untuk memastikan elemen dengan indeks yang sama dapat disimpan dan diakses dengan benar. Resize diperlukan ketika jumlah elemen melebihi kapasitas hash table, memungkinkan tabel untuk menyesuaikan ukurannya. Selain itu, iterasi memungkinkan pengaksesan dan pemrosesan semua elemen dalam hash table secara berurutan.


### Contoh Kode

```C++
#include <iostream>
using namespace std;
const int MAX_SIZE = 10;

// Fungsi hash sederhana
int hash_func(int key) {
    return key % MAX_SIZE;
}

// Struktur data untuk setiap node
struct Node {
    int key;
    int value;
    Node* next;
    Node(int key, int value) : key(key), value(value), next(nullptr) {}
};

// Class hash table
class HashTable {
private:
    Node** table;
public:
    HashTable() {
        table = new Node*[MAX_SIZE]();
    }
    ~HashTable() {
        for (int i = 0; i < MAX_SIZE; i++) {
            Node* current = table[i];
            while (current != nullptr) {
                Node* temp = current;
                current = current->next;
                delete temp;
            }
        }
        delete[] table;
    }

    // Insertion
    void insert(int key, int value) {
        int index = hash_func(key);
        Node* current = table[index];
        while (current != nullptr) {
            if (current->key == key) {
                current->value = value;
                return;
            }
            current = current->next;
        }
        Node* node = new Node(key, value);
        node->next = table[index];
        table[index] = node;
    }

    // Searching
    int get(int key) {
        int index = hash_func(key);
        Node* current = table[index];
        while (current != nullptr) {
            if (current->key == key) {
                return current->value;
            }
            current = current->next;
        }
        return -1;
    }

    // Deletion
    void remove(int key) {
        int index = hash_func(key);
        Node* current = table[index];
        Node* prev = nullptr;
        while (current != nullptr) {
            if (current->key == key) {
                if (prev == nullptr) {
                    table[index] = current->next;
                } else {
                    prev->next = current->next;
                }
                delete current;
                return;
            }
            prev = current;
            current = current->next;
        }
    }

    // Traversal
    void traverse() {
        for (int i = 0; i < MAX_SIZE; i++) {
            Node* current = table[i];
            while (current != nullptr) {
                cout << current->key << ": " << current->value << endl;
                current = current->next;
            }
        }
    }
};

int main() {
    HashTable ht;
    // Insertion
    ht.insert(1, 10);
    ht.insert(2, 20);
    ht.insert(3, 30);

    // Searching
    cout << "Get key 1: " << ht.get(1) << endl;
    cout << "Get key 4: " << ht.get(4) << endl;
   
    // Deletion
    ht.remove(4);
   
    // Traversal
    ht.traverse();
   
    return 0;
}

```

## 3. Rekursif

Rekursif adalah teknik di mana sebuah fungsi memanggil dirinya sendiri, baik secara langsung maupun tidak langsung. Fungsi rekursif berulang kali memanggil dirinya dalam proses pengolahan data atau pemanggilan fungsi.

Dalam proses rekursif, fungsi atau prosedur yang sama akan dipanggil berulang kali. Setiap kali rekursif dijalankan, suatu item akan dimasukkan atau dikeluarkan dari daftar barang yang akan dibeli[6]

Ada empat jenis utama dari fungsi rekursif [7] : tail recursion, head recursion, nested recursion, dan tree recursion. Tail recursion adalah optimisasi dalam fungsi rekursif di mana pemanggilan rekursif adalah operasi terakhir yang dilakukan. Head recursion adalah teknik di mana pemanggilan rekursif dilakukan di awal atau sebelum operasi lainnya. Nested recursion melibatkan pemanggilan fungsi rekursif dalam suatu fungsi sebagai parameter input untuk pemanggilan rekursif pada fungsi lain. Tree recursion adalah jenis di mana setiap panggilan rekursif menghasilkan beberapa panggilan rekursif lainnya.

Rekursif dapat dibagi menjadi dua jenis[8] : rekursi langsung dan rekursi tidak langsung. Rekursi langsung adalah bentuk paling dasar di mana fungsi memanggil dirinya sendiri secara langsung, dengan membagi masalah menjadi submasalah yang lebih kecil hingga mencapai kasus dasar yang mengakhiri rekursi. Rekursi tidak langsung melibatkan serangkaian pemanggilan fungsi di mana fungsi tidak secara eksplisit memanggil dirinya sendiri, melainkan melalui serangkaian fungsi lain.


### Contoh Kode

```C++
#include <iostream>
using namespace std;

//Code ini berfungsi untuk melakukan hitung mundur
//dari angka yang diinputkan

void countdown(int n) {
    if (n == 0) {
        return;
    }
    cout << n << " ";
    countdown(n - 1);
}

int main() {
    cout << "Rekursi Langsung: ";
    countdown(5); //5 merupakan input nya
    cout << endl;
    return 0;
}

```

## 4. Graph and Tree

Graph adalah struktur data yang terdiri dari kumpulan simpul (nodes) yang tidak bersebelahan, di mana setiap simpul terhubung melalui sisi (edges). Simpul-simpul dalam graph disebut vertex (V), dan sisi yang menghubungkannya disebut edge (E). Pasangan (x,y) menunjukkan bahwa simpul x terhubung ke simpul y.

Dalam teori graph, simpul adalah elemen dasar yang merepresentasikan objek atau entitas tertentu, sedangkan sisi adalah hubungan atau koneksi yang menghubungkan simpul-simpul tersebut. Ketika sebuah lintasan dimulai dan berakhir di simpul yang sama, ini disebut siklus. Graph berarah memiliki arah tertentu untuk setiap sisi, sedangkan graph tak berarah tidak memiliki arah tertentu. Derajat suatu simpul adalah jumlah sisi yang terhubung ke simpul tersebut. Graph berbobot memiliki nilai tertentu yang ditetapkan pada setiap sisi, sedangkan graph sederhana adalah graph tak berarah tanpa sisi ganda. Sebuah graph disebut terhubung jika setiap simpul dapat dijangkau dari simpul lainnya. Komponen terhubung adalah kelompok simpul yang saling terhubung dalam graph, dan graph beraturan adalah graph di mana setiap simpul memiliki derajat yang sama.

Graph dapat dibagi menjadi beberapa jenis berdasarkan sifat-sifatnya. Undirected graph memiliki simpul-simpul yang terhubung dengan sisi dua arah. Directed graph memiliki simpul-simpul yang terhubung dengan sisi satu arah. Weighted graph adalah graph di mana setiap sisi memiliki bobot tertentu, sedangkan unweighted graph tidak memiliki bobot pada sisinya dan hanya menunjukkan apakah dua simpul saling terhubung atau tidak[9].

Karakteristik graph mencakup eksentrisitas, yaitu jarak maksimum dari sebuah simpul ke semua simpul lainnya. Simpul dengan eksentrisitas minimum dianggap sebagai pusat dari graph, dan nilai eksentrisitas minimum dari semua simpul disebut jari-jari dari graph terhubung [10]. 

Graph digunakan dalam berbagai aplikasi. Mereka digunakan untuk merepresentasikan aliran komputasi, pemodelan grafik, dan alokasi sumber daya dalam sistem operasi. Google Maps memanfaatkan graph untuk menemukan rute terpendek, dan dalam jaringan komputer, graph digunakan untuk aplikasi peer-to-peer.


### Contoh Kode

```C++
#include <iostream>
#include <iomanip>

using namespace std;

string simpul[7] = {
    "Ciamis", "Bandung", "Bekasi", "Tasikmalaya", "Cianjur", "Purwokerto", "Yogyakarta"
};

int busur[7][7] = {
    {0, 7, 8, 0, 0, 0, 0},
    {0, 0, 5, 0, 0, 15, 0},
    {0, 6, 0, 0, 5, 0, 0},
    {0, 5, 0, 0, 2, 4, 0},
    {23, 0, 0, 10, 0, 0, 8},
    {0, 0, 0, 0, 7, 0, 3},
    {0, 0, 0, 0, 9, 4, 0}
};

void tampilGraph(){
    for (int baris = 0; baris < 7; baris++) {
        cout << " " << setiosflags(ios::left) << setw(15) << simpul[baris] << " : ";
        for (int kolom = 0; kolom < 7; kolom++) {
            if (busur[baris][kolom] != 0) {
                cout << " " << simpul[kolom] << " (" << busur[baris][kolom] << ")"; 
            }
        }
        cout << endl;
    }
}

int main() {
    tampilGraph();
    return 0;
}
```


## Referensi
[1] Enggar Febriyanti1, Suwanto Raharjo2, Muhammad Sholeh3. 2017, PERBANDINGAN MANAJEMEN BANDWIDTH MENGGUNAKAN METODE FIFO (FIRST-IN FIRST-OUT) DANPCQ (PER CONNECTION QUEUE) PADA ROUTER MIKROTIK,  Institut Sains & Teknologi  AKPRIND Yogyakarta: [Jurna]l JARKOM.
[2] Rizki Maulana. 2023, Struktur Data Queue: Pengertian, Fungsi, dan Jenisnya [Artikel], dicoding.com.
[3] Riczky Pratama. 2023, Queue: Pengenalan, Implementasi, Operasi Dasar, dan Aplikasi, [Artikel] Medium.
[4] 2022. Apa itu hash table dan bagaimana penggunaanya[Artikel], algorit.ma.
[5] Annisa. 2023, Struktur Data Hash Table:Pengertian, Cara Kerja dan Operasi Hash Table, Fakultas Ilmu Komputer dan Teknologi Informasi[Artikel], fikti.umsu.ac.id.
[6] sandykosasi. 2013, PENYELESAIAN BOUNDED KNAPSACK PROBLEM
MENGGUNAKAN DYNAMIC PROGRAMMING
(Studi Kasus: CV. Mulia Abadi), Program Studi Teknik Informatika
Sekolah Tinggi Manajemen Informatika dan Komputer Pontianak, [Jurnal] Informatika Mulawarman.
[7]  soffya ranti. 2023, Pengertian dan Fungsi Rekursif serta Contohnya, [Artikel] Kompas.com.
[8] Candan Bengi. 2023, Berbagai Jenis Rekursi,[Artikel] HashDork.com
[9] LamanIT, 2023. Teori Graf: Pengertian, Sejarah, Konsep, Komponen dan Contoh, [Artikel], LamanIT.
[10] Trivusi. 2022, Struktur Data Graph: Pengertian, Jenis, dan Kegunaannya,[Artikel] trivusi.web.id.

