---
title: Gunakan Daftar Umum di Penanda Cerdas Aspose.Cells
linktitle: Gunakan Daftar Umum di Penanda Cerdas Aspose.Cells
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Kuasai Aspose.Cells untuk .NET dengan Daftar Umum dan Penanda Cerdas untuk membuat laporan Excel yang dinamis dengan mudah. Panduan mudah bagi pengembang.
weight: 20
url: /id/net/smart-markers-dynamic-data/generic-list-smart-markers/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gunakan Daftar Umum di Penanda Cerdas Aspose.Cells

## Perkenalan
Membuat laporan dinamis dan aplikasi berbasis data merupakan keterampilan penting dalam lanskap teknologi saat ini. Jika Anda bekerja dengan file .NET dan Excel, Anda mungkin pernah mendengar tentang Aspose.Cells, pustaka canggih yang dirancang khusus untuk memanipulasi lembar kerja Excel secara terprogram. Panduan komprehensif ini akan memandu Anda memanfaatkan Daftar Generik dengan Penanda Cerdas di Aspose.Cells, yang memberi Anda pendekatan langkah demi langkah untuk mengoptimalkan penanganan data dalam aplikasi Anda.
## Prasyarat
Sebelum menyelami kodenya, mari kita bahas secara singkat apa saja yang Anda perlukan:
### Pengetahuan Dasar C#
Anda harus memiliki pemahaman dasar tentang C# dan cara bekerja dengan kelas dan objek. Jika Anda ahli dalam pemrograman berorientasi objek, Anda sudah berada di jalur yang benar.
### Aspose.Cells untuk .NET Terpasang
 Pastikan Anda telah memasang Aspose.Cells di proyek .NET Anda. Anda dapat mengunduh pustaka dari[Situs web Aspose](https://releases.aspose.com/cells/net/). 
### Lingkungan Visual Studio
Menyiapkan Visual Studio di komputer Anda sangatlah penting. Ini adalah lingkungan pengembangan yang paling umum digunakan untuk menulis kode C#.
### File Template
Untuk tutorial ini, kami akan menggunakan templat Excel sederhana yang dapat Anda siapkan terlebih dahulu. Anda hanya memerlukan buku kerja kosong untuk demonstrasi.
## Paket Impor
Sekarang setelah kita memiliki hal-hal penting, mari kita mulai dengan mengimpor paket-paket yang diperlukan. Aturan praktis yang baik adalah menyertakan namespace berikut:
```csharp
using System.IO;
using Aspose.Cells;
using System;
using System.Drawing;
using System.Collections.Generic;
```
Ruang nama ini akan menyediakan fungsionalitas yang dibutuhkan untuk bekerja dengan berkas Excel dan menata sel.
## Langkah 1: Tentukan Kelas Anda
Hal pertama yang harus dilakukan! Kita perlu mendefinisikan`Person` Dan`Teacher` kelas. Berikut caranya:
### Tentukan Kelas Orang
 Itu`Person` kelas akan menampung atribut dasar seperti nama dan usia.
```csharp
public class Person
{
    int _age;
    string _name;
    
    public int Age
    {
        get { return _age; }
        set { _age = value; }
    }
    
    public string Name
    {
        get { return _name; }
        set { _name = value; }
    }
    
    public Person(string name, int age)
    {
        _age = age;
        _name = name;
    }
}
```
### Tentukan Kelas Guru
 Berikutnya adalah`Teacher` kelas, yang mewarisi dari`Person` kelas. Kelas ini selanjutnya akan merangkum daftar siswa.
```csharp
public class Teacher : Person
{
    private IList<Person> m_students;
    public IList<Person> Students
    {
        get { return m_students; }
        set { m_students = value; }
    }
    
    public Teacher(string name, int age) : base(name, age)
    {
        m_students = new List<Person>();
    }
}
```
## Langkah 2: Inisialisasi Buku Kerja dan Buat Desainer
Sekarang setelah kelas-kelas kita siap, saatnya untuk menginisialisasi buku kerja kita:
```csharp
string dataDir = "Your Document Directory"; // Tentukan direktori dokumen Anda
Workbook workbook = new Workbook(); // Contoh Buku Kerja Baru
Worksheet worksheet = workbook.Worksheets[0];
```
## Langkah 3: Siapkan Penanda Cerdas di Lembar Kerja
Kita akan menyiapkan penanda pintar dalam lembar kerja Excel, yang menunjukkan di mana nilai dinamis kita akan ditempatkan.
```csharp
worksheet.Cells["A1"].PutValue("Teacher Name");
worksheet.Cells["A2"].PutValue("&=Teacher.Name");
worksheet.Cells["B1"].PutValue("Teacher Age");
worksheet.Cells["B2"].PutValue("&=Teacher.Age");
worksheet.Cells["C1"].PutValue("Student Name");
worksheet.Cells["C2"].PutValue("&=Teacher.Students.Name");
worksheet.Cells["D1"].PutValue("Student Age");
worksheet.Cells["D2"].PutValue("&=Teacher.Students.Age");
```
## Langkah 4: Terapkan Gaya untuk Meningkatkan Presentasi
Laporan yang bagus harus menarik secara visual! Mari terapkan beberapa gaya pada tajuk:
```csharp
Range range = worksheet.Cells.CreateRange("A1:D1");
Style style = workbook.CreateStyle();
style.Font.IsBold = true;
style.ForegroundColor = Color.Yellow;
style.Pattern = BackgroundType.Solid;
StyleFlag flag = new StyleFlag();
flag.All = true;
range.ApplyStyle(style, flag);
```
## Langkah 5: Buat Instansi Guru dan Siswa
 Sekarang, mari kita buat contoh dari`Teacher` Dan`Person` kelas dan mengisinya dengan data:
```csharp
System.Collections.Generic.List<Teacher> list = new System.Collections.Generic.List<Teacher>();
// Buat objek guru pertama
Teacher h1 = new Teacher("Mark John", 30);
h1.Students = new List<Person>
{
    new Person("Chen Zhao", 14),
    new Person("Jamima Winfrey", 18),
    new Person("Reham Smith", 15)
};
//Buat objek guru kedua
Teacher h2 = new Teacher("Masood Shankar", 40);
h2.Students = new List<Person>
{
    new Person("Karishma Jathool", 16),
    new Person("Angela Rose", 13),
    new Person("Hina Khanna", 15)
};
// Tambahkan ke daftar
list.Add(h1);
list.Add(h2);
```
## Langkah 6: Tetapkan Sumber Data untuk Desainer
Sekarang kita perlu menghubungkan data kita dengan lembar kerja yang telah kita siapkan. 
```csharp
WorkbookDesigner designer = new WorkbookDesigner();
designer.Workbook = workbook;
designer.SetDataSource("Teacher", list);
```
## Langkah 7: Memproses Penanda
Langkah selanjutnya adalah memproses semua penanda pintar yang kita tempatkan sebelumnya:
```csharp
designer.Process();
```
## Langkah 8: Sesuaikan Kolom Secara Otomatis dan Simpan Buku Kerja
Untuk memastikan semuanya terlihat profesional, mari sesuaikan kolom secara otomatis dan simpan buku kerja kita:
```csharp
worksheet.AutoFitColumns();
designer.Workbook.Save(dataDir + "output.xlsx"); // Simpan ke direktori yang ditentukan
```
## Kesimpulan
Nah, itu dia! Anda baru saja membuat lembar kerja Excel secara dinamis, memanfaatkan kekuatan Daftar Umum dan Penanda Cerdas dengan Aspose.Cells untuk .NET. Keterampilan ini akan memungkinkan Anda membuat laporan kompleks dengan mudah dan menggabungkan fungsionalitas berbasis data dalam aplikasi Anda. Baik Anda membuat laporan sekolah, analisis bisnis, atau konten dinamis apa pun, teknik dalam panduan ini akan membantu menyederhanakan alur kerja Anda secara signifikan.
## Pertanyaan yang Sering Diajukan
### Apa itu Aspose.Cells?
Aspose.Cells adalah pustaka .NET untuk membuat dan mengelola file Excel tanpa perlu menginstal Microsoft Excel.
### Dapatkah saya menggunakan Aspose.Cells untuk format file lain?
Ya! Aspose menawarkan pustaka untuk PDF, Word, dan format lainnya, sehingga serbaguna untuk pengelolaan dokumen.
### Apakah saya memerlukan lisensi untuk menggunakan Aspose.Cells?
 Anda dapat memulai dengan uji coba gratis dari[Di Sini](https://releases.aspose.com/), tetapi lisensi berbayar diperlukan untuk penggunaan produksi.
### Apa itu Penanda Cerdas?
Penanda Cerdas adalah tempat penampung dalam templat Excel yang diganti dengan data aktual saat diproses oleh Aspose.Cells.
### Apakah Aspose.Cells cocok untuk kumpulan data besar?
Tentu saja! Aspose.Cells dioptimalkan untuk kinerja, sehingga mampu menangani kumpulan data besar secara efisien.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
