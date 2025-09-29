#include <iostream>
#include <string>
using namespace std;

// Fungsi menentukan warna lampu berdasarkan detik
string getLight(int t, int offset = 78) {
    // offset default = 78 (agar detik ke-45 kuning)
    int cycle = 103;
    int pos = (t + offset) % cycle;

    if (pos < 20) return "Hijau";
    else if (pos < 23) return "Kuning";
    else return "Merah";
}

int main() {
    int times[] = {80, 135, 150, 212};
    for (int t : times) {
        cout << "Detik " << t << " -> " << getLight(t) << endl;
    }
    return 0;
}
