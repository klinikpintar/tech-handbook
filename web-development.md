# Panduan untuk *Web Developer*
Bagian ini berisi mengenai panduan untuk membuat kode baik.
Panduan ini dibuat berdasarkan Clean Code karya Robert Cecil Martin a.k.a Uncle Bob

---

### Panduan Clean Code
Kenapa kita perlu mempelajari clean code? Karena saat ini hampir seluruh aspek kehidupan manusia dipengaruhi oleh *software*. Penulisan *software* yang buruk dapat menyebabkan masalah besar, bahkan sampai bisa membahayakan nyawa manusia.
Maka dari itu kita sebagai *engineer* perlu untuk bisa menuliskan *software* dengan baik.
Salah satu panduan penulisan *software* yang paling populer ditulis oleh Robert C. Martin dalam bukunya yang berjudul *Clean Code*.

---
<br/>

### Berikut ini adalah beberapa poin penting dalam penerapan clean code:

### 1. Long code is not good code
Code yang terlalu panjang itu tidak baik. Code yang terlalu panjang akan menyulitkan pembaca di kemudian hari, baik itu orang lain maupun penulisnya sendiri. Hal ini akan menyulitkan ketika terdapat bug yang berkaitan dengan code tersebut, atau ketika code tersebut perlu di-*refactor*.

Tidak apa menulis code yang panjang di awal, tapi setelah itu kita harus langsung memecah code tersebut ke dalam beberapa *function* atau bahkan *class*.

### 2. Refactoring a function
Katakanlah kita punya sebuah function yang sangat panjang, bagaimana cara me-*refactor*-nya?

Jika dalam sebuah function yang panjang kita menemukan ada beberapa baris code yang dapat dikelompokkan, kita bisa memindahkan code tersebut ke dalam sebuah function baru.

Contohnya kita punya function seperti di bawah: <br>
Code A
```PHP
function printOwing() {
  $this->printBanner();

  // Print details.
  print("name:  " . $this->name);
  print("amount " . $this->getOutstanding());
}
```

Kita bisa me-*refactornya*-nya menjadi <br>
Code B
```PHP
function printOwing() {
  $this->printBanner();
  $this->printDetails($this->getOutstanding());
}

function printDetails($outstanding) {
  print("name:  " . $this->name);
  print("amount " . $outstanding);
}
```
##### source: https://refactoring.guru/extract-method

Informasi ebih lanjut tentang *refactoring* dapat dilihat di [Refactoring Guru](https://refactoring.guru/)
### 3. Polite code - rules for writing a news paper article
Yang dimaksud dengan *polite code* disini adalah ketika sebuah potongan code mengizinkan pembacanya untuk melakukan *early exit*.

Ketika seseorang membaca sebuah code dan di dalam code tersebut terdapat *function call* dengan nama function yang tidak deskriptif, misalnya `retrieve()` dan function ini belum di-*refactor*, maka pembaca tidak bisa *exit* atau berhenti sampai disitu saja, dia harus melihat isi dari function tersebut. Jika ternyata  function tersebut belum di-*refactor* dengan baik, katakanlah function tersebut terdiri dari 150 baris, maka pembaca harus memahami keseluruhan dari 150 baris tersebut untuk memahami apa yang dilakukan oleh si function. Ini memakan banyak waktu dan mencegah pembaca untuk melakukan *early exit*.

Jika dari awal *function call* pada code yang dibaca oleh si pembaca memiliki nama yang deskriptif, misalnya `getDoctorsByPolyclinicId()` dan function ini sudah di-*refactor* dengan baik, pembaca tidak perlu membaca isi dari function tersebut untuk memahami apa yang dilakukannya. Kalaupun pembaca ingin melihat isi dari function tersebut, maka dia akan mendapati isinya mudah dibaca karena setiap actions di dalamnya sudah terpecah menjadi beberapa *function calls* dan ini membuat pembaca mudah memahami isi dari function tersebut dan mengizinkan pembaca untuk melakukan *early exit*.

### 4. Shrunk code - the rules of functions
```
THE RULES OF FUNCTIONS:

The first rule:
    - They should be small

The second rule:
    - They should be smaller than that
```
Seberapa kecil seharusnya sebuah function ditulis?
Sebenarnya tidak ada aturan baku tentang ukuran sebuah function, namun pada dasarnya kita ingin sebuah fungsi hanya melakukan satu hal.\
Sekarang pertanyaannya adalah apa definisi dari *satu hal*?
Uncle Bob mengatakan:
```
A function does one thing until if you cannot meaningfully extract another function from it.
```
Supaya function yang kita tulis hanya melakukan satu hal kita harus memecahnya terus menerus sampai kita tidah bisa memecahnya lagi.

### 5. Rules for arguments
Sebaiknya kita tidak membuat function yang menerima *boolean* sebagai argumen, karena di dalam function tersebut pasti akan ada *if statement*. Lebih baik pisah function tersebut menjadi 2 function berbeda.
### 6. Avoid switch statements
Hindari penggunaan *switch statement* karena akan menyebabkan code menjadi tidak *maintainable*.
Katakanlah kita membuat code untuk menghandle bentuk, segitiga, lingkaran, persegi, dll.
Kita akan perlu *switch statement* untuk merender bentuk, menghapus bentuk, memutar bentuk, dll. Lalu katakan kita perlu menambahkan bentuk baru, saat inilah masalah muncul, karena sekarang kita harus mengupdate seluruh *switch statements* yang sudah kita buat.

Solusi untuk masalah ini adalah *polymorphism*. Kita bisa membuat *base class* bernama *shapes* untuk bentuk dan membuat *subclasses* untuk setiap bentuk yang kita inginkan, lalu mengaplikasikan functions yang sesuai pada *subclasses* tersebut.

### 7. Command and query separation
Sebuah function dikatakan memiliki side effect jika dia merubah state dari sistem. Misalkan function`open()` untuk membuka file, atau `malloc()` untuk mengalokasikan blok memori.

Sebuah function yang me-*return* *void* pasti punya side effect, maka dari itu function yang me-*return* sebuah value, sehrusnya tidak memiliki side effect. Ini adalah konvensi yang disebut dengan *command and query separation*. *Command* merubah state dari sistem maka dari itu dia me-*return* *void*, *query* me-*return* *void* dan berdasarkan konvensi seharusnya tidak merubah state dari sistem.

Pemisahan ini memudahkan kita untuk melacak semua penggunaan *command*. Setiap *command* memiliki pasangan, misalnya `open()` dan `close()`. Setiap kita memanggil `open()`, kita harus memanggil `close()`. Jika terlalu banyak user yang membuka file dan tidak ditutup, sistem bisa mengalami *crash*. Melakukan *command and query separation* dapat membantu menghindari hal ini.

### 8. Prefer exeptions to returning error codes
Ketika kita men-*throw exeption*, *code execution* akan berpindah jalur dari "*happy-path*" ke "*error-path*", ini memudahkan kita dalam menghandle error.

### 9. Rule for try block
Ketika kita menggunakan *try block* dalam sebuah function, satu-satunya yang boleh menjadi isi dari function tersebut adalah *try block*. Jangan menulis code sebelum atau sesudah *try block*, jangan menulis terlalu banyak code di dalam *try block*, dan jangan menulis *nested try block*. Lebih baik jika isi dari sebuah *try block* hanyalah sebuah function call. Sebuah function yang menggunakan *try block* hanya boleh berisi *try*, *catch*, dan *finally*.

### 10. DRY principle (Don't Repeat Yourself)
Jangan menggunakan potongan code yang sama berulang-ulang di berbagai tempat. Ketika kita memiliki potongan code yang perlu digunakan berkali-kali, jadikan potongan code tersebut sebagai sebuah function dan panggil function tersebut dimana dibutuhkan.

Referensi tentang clean code:
- [Clean Code - Uncle Bob / Lesson 1](https://www.youtube.com/watch?v=7EmboKQH8lM&t=2643s)

---
Bacaan tambahan:

- [Upskilling Courses Klinik Pintar](https://docs.klinikpintar.id/doc/upskilling-courses-RnrDYzWaIO)
