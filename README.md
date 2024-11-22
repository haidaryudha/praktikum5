# praktikum5
### **Fungsi `hitung_nilai_akhir`**

```python
def hitung_nilai_akhir(tugas, uts, uas):
    return (tugas * 0.3) + (uts * 0.35) + (uas * 0.35)
```

#### Penjelasan:
Fungsi `hitung_nilai_akhir` bertugas untuk menghitung nilai akhir seorang mahasiswa berdasarkan tiga komponen nilai:
- **Nilai Tugas** (30% bobot)
- **Nilai UTS** (35% bobot)
- **Nilai UAS** (35% bobot)

Prosentase bobotnya sudah ditentukan secara eksplisit, sehingga fungsi ini mengalikan nilai masing-masing komponen dengan bobotnya, kemudian menjumlahkan hasilnya untuk mendapatkan **nilai akhir** mahasiswa. Fungsi ini menerima tiga argumen berupa nilai tugas, uts, dan uas, dan mengembalikan nilai akhir sebagai hasil perhitungan.

---

### **Fungsi `tampilkan_data`**

```python
def tampilkan_data():
    if not data_mahasiswa:
        print("\nDaftar Nilai Mahasiswa Kosong")
        return
    print("\nDaftar Nilai Mahasiswa:")
    print("="*86)
    print(f"| {'No':^3} | {'NIM':^10} | {'Nama':^15} | {'Tugas':^5} | {'UTS':^5} | {'UAS':^5} | {'Akhir':^7} |")
    print("="*86)
    for i, (nim, mahasiswa) in enumerate(data_mahasiswa.items(), start=1):
        print(f"| {i:^3} | {nim:^10} | {mahasiswa['Nama']:^15} | {mahasiswa['Tugas']:^5} | {mahasiswa['UTS']:^5} | {mahasiswa['UAS']:^5} | {mahasiswa['Nilai Akhir']:^7.2f} |")
    print("="*86)
```

#### Penjelasan:
Fungsi `tampilkan_data` bertugas untuk menampilkan seluruh data mahasiswa yang ada di dalam **dictionary** `data_mahasiswa`. Berikut alur kerjanya:
1. Fungsi memeriksa apakah `data_mahasiswa` kosong. Jika kosong, program akan menampilkan pesan "Daftar Nilai Mahasiswa Kosong" dan keluar dari fungsi.
2. Jika ada data, maka program akan menampilkan data mahasiswa dalam bentuk tabel dengan format yang rapi. Tabel ini memiliki kolom-kolom berikut:
   - **No**: Nomor urut data mahasiswa.
   - **NIM**: Nomor Induk Mahasiswa.
   - **Nama**: Nama mahasiswa.
   - **Tugas**: Nilai tugas.
   - **UTS**: Nilai Ujian Tengah Semester.
   - **UAS**: Nilai Ujian Akhir Semester.
   - **Akhir**: Nilai akhir yang dihitung berdasarkan bobot tugas, uts, dan uas.
3. Setiap baris data mahasiswa ditampilkan dalam format yang rapi, menggunakan perulangan `for` yang akan mencetak satu per satu informasi mahasiswa berdasarkan urutan NIM.

---

### **Inisialisasi `data_mahasiswa`**

```python
data_mahasiswa = {}
```

#### Penjelasan:
`data_mahasiswa` adalah sebuah **dictionary kosong** yang akan digunakan untuk menyimpan data mahasiswa. Di dalam dictionary ini, **key**-nya adalah `NIM` mahasiswa dan **value**-nya adalah sebuah dictionary yang berisi:
- **Nama mahasiswa**
- **Nilai Tugas**
- **Nilai UTS**
- **Nilai UAS**
- **Nilai Akhir**

Setiap kali ada data mahasiswa baru yang dimasukkan, dictionary ini akan diperbarui untuk menyimpan informasi mahasiswa tersebut.

---

### **Program Utama dan Menu Interaktif**

Bagian utama dari program adalah sebuah loop `while True` yang memungkinkan pengguna untuk memilih berbagai opsi dalam menu dan terus menjalankan aplikasi sampai mereka memilih untuk keluar.

```python
while True:
    print("\nMenu:")
    print("[T]ambah, [U]bah, [H]apus, [L]ihat, [C]ari, [K]eluar")
    pilihan = input("Pilih menu: ").lower()
```

#### Penjelasan:
- Program menampilkan menu yang berisi beberapa opsi yang dapat dipilih oleh pengguna:
  - **[T]ambah**: Menambah data mahasiswa baru.
  - **[U]bah**: Mengubah data mahasiswa yang sudah ada.
  - **[H]apus**: Menghapus data mahasiswa berdasarkan NIM.
  - **[L]ihat**: Menampilkan seluruh data mahasiswa.
  - **[C]ari**: Mencari data mahasiswa berdasarkan NIM.
  - **[K]eluar**: Keluar dari program.

Program kemudian menunggu input pengguna untuk memilih salah satu opsi menu. Input ini akan diproses untuk menentukan tindakan yang akan dilakukan. Setiap opsi memiliki penanganan yang berbeda sesuai dengan pilihan yang dimasukkan.

---

### **Penjelasan Setiap Opsi dalam Menu**

#### **1. [T]ambah - Menambah Data Mahasiswa**

```python
if pilihan == "t":  # Tambah data
    print("\nTambah Data Mahasiswa")
    nim = input("Masukkan NIM Mahasiswa: ")
    if nim in data_mahasiswa:
        print("NIM sudah terdaftar. Gunakan menu Ubah untuk memperbarui data.")
        continue
    nama = input("Masukkan Nama Mahasiswa: ")
    tugas = float(input("Masukkan Nilai Tugas: "))
    uts = float(input("Masukkan Nilai UTS: "))
    uas = float(input("Masukkan Nilai UAS: "))
    nilai_akhir = hitung_nilai_akhir(tugas, uts, uas)
    data_mahasiswa[nim] = {
        "Nama": nama,
        "Tugas": tugas,
        "UTS": uts,
        "UAS": uas,
        "Nilai Akhir": nilai_akhir
    }
    print("Data berhasil ditambahkan!")
```

Penjelasan:
- Program meminta input NIM mahasiswa baru. Jika NIM tersebut sudah ada dalam `data_mahasiswa`, maka akan ditampilkan pesan bahwa NIM sudah terdaftar dan meminta pengguna untuk memilih menu **Ubah**.
- Jika NIM belum terdaftar, program kemudian meminta inputan untuk **Nama**, **Nilai Tugas**, **Nilai UTS**, dan **Nilai UAS**.
- Fungsi `hitung_nilai_akhir` dipanggil untuk menghitung nilai akhir berdasarkan input yang diberikan.
- Data mahasiswa kemudian disimpan dalam `data_mahasiswa` dengan NIM sebagai key dan informasi mahasiswa sebagai value.

#### **2. [U]bah - Mengubah Data Mahasiswa**

```python
elif pilihan == "u":  # Ubah data
    nim = input("\nMasukkan NIM Mahasiswa yang ingin diubah: ")
    if nim in data_mahasiswa:
        print("Data ditemukan. Silakan perbarui.")
        nama = input("Masukkan Nama Baru: ")
        tugas = float(input("Masukkan Nilai Tugas Baru: "))
        uts = float(input("Masukkan Nilai UTS Baru: "))
        uas = float(input("Masukkan Nilai UAS Baru: "))
        nilai_akhir = hitung_nilai_akhir(tugas, uts, uas)
        data_mahasiswa[nim] = {
            "Nama": nama,
            "Tugas": tugas,
            "UTS": uts,
            "UAS": uas,
            "Nilai Akhir": nilai_akhir
        }
        print("Data berhasil diperbarui!")
    else:
        print("Data dengan NIM tersebut tidak ditemukan.")
```

Penjelasan:
- Program meminta NIM mahasiswa yang datanya ingin diubah. Jika NIM ditemukan, program akan meminta input nilai yang baru untuk **Nama**, **Nilai Tugas**, **Nilai UTS**, dan **Nilai UAS**.
- Nilai akhir dihitung kembali menggunakan fungsi `hitung_nilai_akhir` dan kemudian memperbarui data mahasiswa dalam `data_mahasiswa`.

#### **3. [H]apus - Menghapus Data Mahasiswa**

```python
elif pilihan == "h":  # Hapus data
    nim = input("\nMasukkan NIM Mahasiswa yang ingin dihapus: ")
    if nim in data_mahasiswa:
        del data_mahasiswa[nim]
        print("Data berhasil dihapus!")
    else:
        print("Data dengan NIM tersebut tidak ditemukan.")
```

Penjelasan:
- Program meminta input NIM mahasiswa yang ingin dihapus.
- Jika NIM ditemukan dalam `data_mahasiswa`, data mahasiswa tersebut dihapus menggunakan perintah `del`.
- Jika N

IM tidak ditemukan, pesan kesalahan akan ditampilkan.

#### **4. [L]ihat - Menampilkan Semua Data Mahasiswa**

```python
elif pilihan == "l":  # Tampilkan data
    tampilkan_data()
```

Penjelasan:
- Fungsi `tampilkan_data()` dipanggil untuk menampilkan semua data mahasiswa dalam bentuk tabel. Jika data kosong, pesan "Daftar Nilai Mahasiswa Kosong" akan ditampilkan.

#### **5. [C]ari - Mencari Data Mahasiswa Berdasarkan NIM**

```python
elif pilihan == "c":  # Cari data
    nim = input("\nMasukkan NIM Mahasiswa yang ingin dicari: ")
    if nim in data_mahasiswa:
        mahasiswa = data_mahasiswa[nim]
        print("\nData Mahasiswa:")
        print("="*86)
        print(f"| {'No':^3} | {'NIM':^10} | {'Nama':^15} | {'Tugas':^5} | {'UTS':^5} | {'UAS':^5} | {'Akhir':^7} |")
        print("="*86)
        print(f"| {'1':^3} | {nim:^10} | {mahasiswa['Nama']:^15} | {mahasiswa['Tugas']:^5} | {mahasiswa['UTS']:^5} | {mahasiswa['UAS']:^5} | {mahasiswa['Nilai Akhir']:^7.2f} |")
        print("="*86)
    else:
        print("Data dengan NIM tersebut tidak ditemukan.")
```

Penjelasan:
- Program meminta input NIM untuk mencari data mahasiswa yang bersangkutan.
- Jika ditemukan, informasi mahasiswa tersebut ditampilkan dalam format tabel yang serupa dengan fungsi `tampilkan_data()`.

#### **6. [K]eluar - Keluar dari Program**

```python
elif pilihan == "k":  # Keluar
    print("Terima kasih telah menggunakan program ini!")
    break
```

Penjelasan:
- Program mengakhiri loop dan keluar dari aplikasi, menampilkan pesan terima kasih.
