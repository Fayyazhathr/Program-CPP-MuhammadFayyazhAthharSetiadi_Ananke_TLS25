# Program-CPP-MuhammadFayyazhAthharSetiadi_Ananke_TLS25
#include <iostream>
#include <string>
#include <cctype>
using namespace std;

// Cek huruf vokal
bool isVowel(char c) {
    c = tolower(c);
    return (c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u');
}

// Fungsi reverse buatan sendiri
string myReverse(string s) {
    int n = s.length();
    for (int i = 0; i < n / 2; i++) {
        char temp = s[i];
        s[i] = s[n - 1 - i];
        s[n - 1 - i] = temp;
    }
    return s;
}

// ENCODE: kata asli -> sandi
string encode(string word) {
    // Ambil huruf pertama
    char first = word[0];
    int asciiCode = (int)first;

    // Hilangkan vokal
    string noVowel = "";
    for (char c : word) {
        if (!isVowel(c)) noVowel += c;
    }

    // Balik
    string reversed = myReverse(noVowel);

    // Masukkan kode ASCII di tengah
    int mid = reversed.length() / 2;
    string result = reversed.substr(0, mid) + to_string(asciiCode) + reversed.substr(mid);
    return result;
}

// DECODE: sandi -> rangka konsonan + huruf pertama
string decode(string cipher) {
    string letters = "";
    string num = "";

    // Pisahkan angka ASCII dari huruf
    for (char c : cipher) {
        if (isdigit(c)) num += c;
        else letters += c;
    }

    // Dapatkan huruf pertama dari ASCII
    int asciiCode = stoi(num);
    char first = (char)asciiCode;

    // Balik kembali huruf
    string originalConsonants = myReverse(letters);

    // Tambahkan huruf pertama di depan
    string partial = originalConsonants;
    partial[0] = first; // ganti huruf pertama agar sesuai ASCII
    return partial;
}

int main() {
    // Contoh penggunaan
    string word = "Banana";
    string cipher = encode(word);
    cout << "Asli   : " << word << endl;
    cout << "Encode : " << cipher << endl;

    string back = decode(cipher);
    cout << "Decode (rangka konsonan) : " << back << endl;

    return 0;
}
