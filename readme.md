# <h1 align="center">CPMK 1</h1>
<p align="center">Rifka Annisa Swasthi</p>



### 1. cari cara duplikasi maksimal menggunakan 1 for tidak boleh ada for didalam for menggunakan fungsi rekursif dan index 2314

```C++
#include <iostream>
using namespace std;

// Helper recursive function to check for duplicates
bool checkRecursive(int arr[], int length, int index) {
    if (index >= length - 1) {
        return false;  // Base case: reached the end of the array
    }
    for (int j = index + 1; j < length; j++) {
        if (arr[index] == arr[j]) {
            return true;  // Duplicate found
        }
    }
    return checkRecursive(arr, length, index + 1);  // Recursive call to check next index
}

bool cekDuplikat(int arr[], int panjangArr) {
    return checkRecursive(arr, panjangArr, 0);
}

int main(void) {
    int arrA[] = {2, 1, 3, 1};
    int panjangArr = sizeof(arrA) / sizeof(arrA[0]);
    cout << cekDuplikat(arrA, panjangArr) << endl;
    return 0;
}


```

