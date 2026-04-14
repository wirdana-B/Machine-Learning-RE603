# Python Data Types

## 1. Primitive Data Types

Primitive data types adalah tipe data dasar yang digunakan untuk menyimpan satu nilai.

* **Integer (int)** → Bilangan bulat
  Contoh: `10`, `150`, `-5`

* **Float (float)** → Bilangan desimal
  Contoh: `3.14`, `1.5`, `-35.59`

* **Complex (complex)** → Bilangan kompleks dengan bagian real dan imajiner
  Contoh: `3 + 4j`

* **String (str)** → Tipe data teks
  Contoh: `"Hello World"`

* **Boolean (bool)** → Nilai logika
  Nilai yang mungkin: `True` atau `False`

---

# 2. Non-Primitive Data Types

## List

List digunakan untuk menyimpan banyak data dalam satu variabel dan **dapat diubah (mutable)**.

Ciri-ciri:

* Menggunakan tanda `[]`
* Bisa diakses dengan **index**
* Bisa **ditambah, diubah, dan dihapus**

Contoh operasi:

* Akses elemen → `list[index]`
* Menambah data → `append()`, `insert()`
* Menghapus data → `remove()`, `pop()`, `del`
* Bisa digunakan dalam **loop**

---

## Tuple

Tuple mirip dengan list tetapi **tidak bisa diubah (immutable)** setelah dibuat.

Ciri-ciri:

* Menggunakan tanda `()`
* Data **tidak bisa dimodifikasi**
* Lebih aman dan cepat untuk data tetap

Fitur:

* Packing & Unpacking data
* Menggabungkan tuple dengan `+`
* Fungsi seperti `count()` dan `index()`

---

## Dictionary

Dictionary digunakan untuk menyimpan data dalam bentuk **pasangan key dan value**.

Ciri-ciri:

* Menggunakan `{ }`
* Akses data menggunakan **key**
* Data bisa **ditambah, diubah, atau dihapus**

Operasi umum:

* Tambah / ubah data → `dict[key] = value`
* Hapus data → `del`, `pop()`

---

## Set

Set digunakan untuk menyimpan **elemen unik tanpa duplikasi**.

Ciri-ciri:

* Menggunakan `{ }`
* Tidak memiliki **index**
* Tidak menyimpan data yang sama

Operasi:

* Tambah elemen → `add()`
* Hapus elemen → `remove()`

Operasi himpunan:

* **Intersection** → `a & b`
* **Union** → `a | b`
* **Difference** → `a - b`

---

# 3. Konversi Tipe Data

## Implicit Conversion

Konversi otomatis yang dilakukan Python saat operasi data.

Contoh:
`int + float → float`

---

## Explicit Conversion (Casting)

Konversi tipe data secara manual menggunakan fungsi bawaan Python.

Contoh fungsi casting:

* `int()`
* `float()`
* `str()`
* `list()`
* `tuple()`
* `set()`

Digunakan untuk menyesuaikan tipe data agar tidak terjadi error saat operasi.
--------------------------------------------------------------------------------------------------------------------------------

# Object Oriented Programming (OOP) di Python
## Pengertian OOP

Object Oriented Programming (OOP) adalah paradigma pemrograman yang mengorganisir kode ke dalam **class** dan **object**.
Setiap **object** memiliki **atribut (data)** dan **method (perilaku/fungsi)** yang dapat berinteraksi dalam program.

Contoh sederhana:
Objek **Mobil** memiliki:

* **Atribut**: jenis mobil, warna, ban, setir, dll.
* **Perilaku (method)**: berjalan, mengerem, membunyikan klakson.

---

# 1. Class

**Class** adalah blueprint atau rancangan untuk membuat sebuah object.
---

# 2. Object

**Object** adalah instance dari sebuah class.
---

# 3. Constructor (`__init__`)

`__init__` adalah method khusus yang dijalankan ketika object dibuat.
Digunakan untuk menginisialisasi atribut dari object.
---

# 4. Default Constructor

Constructor tanpa parameter tambahan.
---

# 5. Parameterized Constructor
---

# 6. Method

Method adalah fungsi yang berada di dalam class dan digunakan oleh object.
---

# 7. Instance Variable

Instance variable adalah variabel yang dimiliki oleh setiap object dari suatu class.
---

# Contoh Studi Kasus

Class **Mobil** dapat memiliki:

* atribut: jenis mobil, warna, bensin, kilometer
* method: `jalan_maju()`, `jalan_mundur()`, `isi_bensin()`

Method tersebut mengatur perilaku mobil seperti bergerak dan mengonsumsi bensin.

---

# Contoh OOP Sederhana

Class **Lingkaran**:

```python
class Lingkaran:
    def __init__(self):
        self.jari_jari = 10
        self.pi = 3.14159

    def luas_lingkaran(self):
        return self.pi * self.jari_jari ** 2

    def keliling_lingkaran(self):
        return 2 * self.pi * self.jari_jari
```

Object dapat menghitung:

* **Luas Lingkaran**
* **Keliling Lingkaran**

--------------------------------------------------------------------------------------------------------------------------------

# Python – Advanced Programming

Pada bagian ini dipelajari beberapa konsep lanjutan dalam Python, yaitu:

1. **Object Oriented Programming (OOP)**
2. **Modular Code**
3. **Efficiency Code**
4. **Best Practice dalam Python Coding**

---

# Object Oriented Programming (OOP)

**OOP (Object Oriented Programming)** adalah paradigma pemrograman yang berfokus pada **objek**.
Dalam OOP, program dibangun dari **class** yang kemudian dibuat menjadi **object** yang saling berinteraksi.

Python merupakan salah satu bahasa pemrograman yang **mendukung konsep OOP**.

---

# Main Principles of OOP

Terdapat **4 prinsip utama OOP**, yaitu:

* Encapsulation
* Inheritance
* Polymorphism
* Abstraction

---

# 1. Encapsulation

**Encapsulation** adalah konsep menyembunyikan data internal suatu objek agar tidak dapat diakses langsung dari luar class.

Ciri utama:

* Atribut biasanya diawali dengan `_` (underscore)
* Akses dilakukan melalui **getter** dan **setter**

Contoh konsep:

* `get_username()` digunakan untuk mengambil data
* `set_username()` digunakan untuk mengubah data dengan validasi tertentu

Manfaat:

* Melindungi data dari perubahan yang tidak diinginkan
* Membuat kode lebih aman dan terkontrol

---

# 2. Inheritance

**Inheritance (pewarisan)** memungkinkan sebuah class **mewarisi atribut dan method dari class lain**.

Istilah dalam inheritance:

* **Parent class** → class induk
* **Child class** → class turunan

Contoh:
`PremiumUser` dapat mewarisi atribut dari `User`.

Keuntungan:

* Mengurangi duplikasi kode
* Mempermudah pengembangan program

---

# 3. Polymorphism

**Polymorphism** memungkinkan **method yang sama digunakan oleh objek yang berbeda** tetapi dengan perilaku yang berbeda.

Contohnya:

* Method `display_user_info()` dapat digunakan oleh `User` dan `PremiumUser`.
* Class turunan dapat **override** method dari class induk.

Manfaat:

* Membuat kode lebih fleksibel
* Mempermudah penggunaan objek berbeda dengan cara yang sama

---

# 4. Abstraction

**Abstraction** adalah konsep menyembunyikan detail implementasi dan hanya menampilkan fitur penting kepada pengguna.

Dalam Python dapat menggunakan:

* `ABC` (Abstract Base Class)
* `@abstractmethod`

Class abstrak:

* Tidak dapat langsung dibuat objeknya
* Harus diwarisi oleh subclass yang mengimplementasikan method abstrak.

Manfaat:

* Mengurangi kompleksitas program
* Membuat struktur kode lebih jelas

----------------------------------------------------------------------------------------------------------------------------------------------------------------
# Python Functions

Function adalah blok kode yang digunakan untuk menjalankan tugas tertentu dan dapat dipanggil kembali saat dibutuhkan.
Dengan function, program menjadi lebih **terstruktur, mudah dibaca, dan dapat digunakan kembali (reusable)**.

---

# 1. Format Dasar Function

Function dibuat menggunakan keyword `def` diikuti nama fungsi dan tanda kurung.

Contoh:

```python
def nama_function():
    print("Hello, ini saya")

nama_function()
```

---

# 2. Function dengan Parameter

Parameter digunakan untuk menerima input dari pengguna saat fungsi dipanggil.

Contoh:

```python
def saya(nama):
    print(f"Halo, {nama}! Ada yang bisa dibantu?")

saya("Wirdana")
```

Parameter memungkinkan fungsi digunakan dengan nilai yang berbeda.

---

# 3. Default Parameter

Parameter dapat memiliki nilai default sehingga fungsi tetap bisa dijalankan meskipun tidak diberikan nilai.

Contoh:

```python
def saya(nama="User"):
    print(f"Halo, {nama}")

saya()
saya("Raihan Noval")
```

Jika tidak ada nilai yang diberikan, maka Python menggunakan nilai default.

---

# 4. Function dengan Return Value

Function dapat mengembalikan nilai menggunakan keyword `return`.

Contoh:

```python
def tambah(a, b):
    return a + b

hasil = tambah(5, 3)
print(hasil)
```

`return` digunakan untuk mengirim hasil dari fungsi ke pemanggil.

---

# 5. Function dengan Banyak Parameter

Jika jumlah parameter tidak diketahui, Python menyediakan:

### *args

Digunakan untuk menerima banyak argumen tanpa nama.

```python
def jumlahkan(*angka):
    return sum(angka)

print(jumlahkan(1,2,3,4))
```

### **kwargs

Digunakan untuk menerima banyak argumen dengan nama (dictionary).

```python
def biodata(**data):
    for key, value in data.items():
        print(f"{key}: {value}")
```

---

# Contoh Penggunaan Function

Menghitung **Luas Lingkaran** dan **Keliling Lingkaran**.

```python
def luas_lingkaran(jari_jari):
    return 3.14 * jari_jari**2

def keliling_lingkaran(jari_jari):
    return 2 * 3.14 * jari_jari

print(luas_lingkaran(15))
print(keliling_lingkaran(15))
```




