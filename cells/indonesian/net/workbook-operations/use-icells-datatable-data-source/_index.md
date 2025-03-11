---
title: Gunakan ICellsDataTableDataSource untuk Workbook Designer
linktitle: Gunakan ICellsDataTableDataSource untuk Workbook Designer
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara menggunakan ICellsDataTableDataSource dengan Aspose.Cells for .NET untuk mengisi lembar Excel secara dinamis. Sempurna untuk mengotomatiskan data pelanggan dalam buku kerja.
weight: 21
url: /id/net/workbook-operations/use-icells-datatable-data-source/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Gunakan ICellsDataTableDataSource untuk Workbook Designer

## Perkenalan
 Membuat spreadsheet tingkat lanjut dengan integrasi data otomatis dapat menjadi pengubah permainan, terutama dalam aplikasi bisnis. Dalam tutorial ini, kita akan mempelajari cara menggunakan`ICellsDataTableDataSource`untuk perancang buku kerja di Aspose.Cells untuk .NET. Kami akan memandu Anda membangun solusi yang sederhana dan mudah dibaca untuk memuat data kustom ke dalam file Excel secara dinamis. Jadi, jika Anda bekerja dengan daftar pelanggan, data penjualan, atau hal serupa, panduan ini cocok untuk Anda!
## Prasyarat
Untuk memulai, pastikan Anda memiliki hal berikut:
-  Pustaka Aspose.Cells untuk .NET – Anda dapat mengunduhnya dari[Di Sini](https://releases.aspose.com/cells/net/) atau dapatkan versi uji coba gratis.
- Lingkungan Pengembangan .NET – Visual Studio adalah pilihan yang tepat.
- Pemahaman Dasar C# – Keakraban dengan kelas dan penanganan data akan membantu Anda mengikutinya.
Sebelum melanjutkan, pastikan lingkungan pengembangan Anda telah disiapkan dengan paket yang diperlukan.
## Paket Impor
Untuk menggunakan Aspose.Cells secara efektif, Anda perlu mengimpor paket-paket penting. Berikut ini adalah referensi cepat untuk namespace yang diperlukan:
```csharp
using Aspose.Cells.Rendering;
using Aspose.Cells.WebExtensions;
using System;
using System.Collections;
```
## Langkah 1: Tentukan Kelas Data Pelanggan
 Untuk memulai, buatlah yang sederhana`Customer` kelas. Kelas ini akan berisi rincian dasar pelanggan seperti`FullName` Dan`Address`Anggap saja ini adalah cara untuk menentukan "bentuk" data Anda.
```csharp
public class Customer
{
    public Customer(string aFullName, string anAddress)
    {
        FullName = aFullName;
        Address = anAddress;
    }
    public string FullName { get; set; }
    public string Address { get; set; }
}
```
## Langkah 2: Siapkan Kelas Daftar Pelanggan
 Selanjutnya, definisikan sebuah`CustomerList` kelas yang memperluas`ArrayList` Daftar yang disesuaikan ini akan menampung contoh-contoh`Customer` dan mengizinkan akses terindeks ke setiap entri.
```csharp
public class CustomerList : ArrayList
{
    public new Customer this[int index]
    {
        get { return (Customer)base[index]; }
        set { base[index] = value; }
    }
}
```
Pada langkah ini, kami membungkus data kami ke dalam format yang dapat dikenali dan diproses oleh Aspose.Cells.
## Langkah 3: Buat Kelas Sumber Data Pelanggan
 Di sinilah hal-hal menjadi menarik. Kita akan membuat`CustomerDataSource` kelas penerapan`ICellsDataTable` untuk membuat data kita kompatibel dengan desainer buku kerja Aspose.Cells.
```csharp
public class CustomerDataSource : ICellsDataTable
{
    internal string[] m_Columns;
    internal ICollection m_DataSource;
    private Hashtable m_PropHash;
    private IEnumerator m_IEnumerator;
    private PropertyInfo[] m_Properties;
    public CustomerDataSource(CustomerList customers)
    {
        this.m_DataSource = customers;
        this.m_Properties = customers[0].GetType().GetProperties();
        this.m_Columns = new string[this.m_Properties.Length];
        this.m_PropHash = new Hashtable(this.m_Properties.Length);
        for (int i = 0; i < m_Properties.Length; i++)
        {
            this.m_Columns[i] = m_Properties[i].Name;
            this.m_PropHash.Add(m_Properties[i].Name, m_Properties[i]);
        }
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public string[] Columns => this.m_Columns;
    public int Count => this.m_DataSource.Count;
    public void BeforeFirst()
    {
        this.m_IEnumerator = this.m_DataSource.GetEnumerator();
    }
    public object this[int index] => this.m_Properties[index].GetValue(this.m_IEnumerator.Current, null);
    public object this[string columnName] => ((PropertyInfo)this.m_PropHash[columnName]).GetValue(this.m_IEnumerator.Current, null);
    public bool Next()
    {
        if (this.m_IEnumerator == null)
            return false;
        return this.m_IEnumerator.MoveNext();
    }
}
```
 Kebiasaan ini`CustomerDataSource` kelas memungkinkan Aspose.Cells untuk menafsirkan setiap`Customer` objek sebagai baris dalam berkas Excel.
## Langkah 4: Inisialisasi Data Pelanggan
Sekarang, mari tambahkan beberapa pelanggan ke daftar kita. Di sinilah kita memuat data yang akan ditulis ke dalam buku kerja. Jangan ragu untuk menambahkan lebih banyak entri sesuai kebutuhan.
```csharp
CustomerList customers = new CustomerList();
customers.Add(new Customer("Thomas Hardy", "120 Hanover Sq., London"));
customers.Add(new Customer("Paolo Accorti", "Via Monte Bianco 34, Torino"));
```
Dalam contoh ini, kita bekerja dengan kumpulan data kecil. Namun, Anda dapat dengan mudah memperluas daftar ini dengan memuat data dari basis data atau sumber lain.
## Langkah 5: Muat Buku Kerja
Sekarang, mari kita buka buku kerja Excel yang sudah ada yang berisi Smart Marker yang diperlukan. Buku kerja ini akan berfungsi sebagai templat kita, dan Aspose.Cells akan secara dinamis mengganti Smart Marker dengan data pelanggan.
```csharp
string sourceDir = "Your Document Directory";
Workbook workbook = new Workbook(sourceDir + "SmartMarker1.xlsx");
```
 Pastikan bahwa`"SmartMarker1.xlsx"` berisi placeholder seperti`&=Customer.FullName` Dan`&=Customer.Address` di mana data harus diisi.
## Langkah 6: Siapkan Desainer Buku Kerja
Sekarang, mari konfigurasikan perancang buku kerja untuk menghubungkan sumber data pelanggan kita dengan Penanda Cerdas buku kerja.
```csharp
WorkbookDesigner designer = new WorkbookDesigner(workbook);
designer.SetDataSource("Customer", new CustomerDataSource(customers));
```
 Itu`SetDataSource` metode mengikat kita`CustomerDataSource` ke Penanda Cerdas di buku kerja. Setiap penanda yang diberi label`&=Customer` di Excel sekarang akan digantikan dengan data pelanggan yang sesuai.
## Langkah 7: Proses dan Simpan Buku Kerja
Terakhir, mari proses buku kerja untuk mengisi data dan menyimpan hasilnya.
```csharp
string outputDir = "Your Document Directory";
designer.Process();
workbook.Save(outputDir + "dest.xlsx");
```
Kode ini memicu pemrosesan Penanda Cerdas, mengganti semua placeholder dengan data, dan menyimpan hasilnya sebagai`dest.xlsx`.
## Kesimpulan
 Selamat! Anda telah berhasil menerapkan`ICellsDataTableDataSource` untuk desainer buku kerja yang menggunakan Aspose.Cells untuk .NET. Pendekatan ini ideal untuk mengotomatiskan pengisian data dalam spreadsheet, terutama saat menangani data dinamis seperti daftar pelanggan atau inventaris produk. Dengan keterampilan ini, Anda berada di jalur yang tepat untuk membangun aplikasi berbasis data yang membuat pelaporan berbasis Excel menjadi mudah!
## Pertanyaan yang Sering Diajukan
###  Apa`ICellsDataTable` in Aspose.Cells?  
Ini adalah antarmuka yang memungkinkan sumber data khusus untuk dihubungkan dengan Penanda Cerdas Aspose.Cells untuk populasi data dinamis.
### Bagaimana saya dapat menyesuaikan data dalam templat buku kerja?  
 Placeholder yang disebut Penanda Cerdas, seperti`&=Customer.FullName`, digunakan. Penanda ini diganti dengan data nyata selama pemrosesan.
### Apakah Aspose.Cells untuk .NET gratis?  
 Aspose.Cells menawarkan uji coba gratis, tetapi akses penuh memerlukan lisensi berbayar. Periksa[uji coba gratis](https://releases.aspose.com/) atau[membeli](https://purchase.aspose.com/buy) pilihan.
### Bisakah saya menambahkan lebih banyak data pelanggan secara dinamis?  
 Tentu saja! Cukup isi`CustomerList`dengan entri tambahan sebelum menjalankan program.
### Di mana saya bisa mendapatkan bantuan jika saya buntu?  
 Aspose memiliki[forum dukungan](https://forum.aspose.com/c/cells/9) tempat pengguna dapat mengajukan pertanyaan dan mendapatkan bantuan dari komunitas dan tim Aspose.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
