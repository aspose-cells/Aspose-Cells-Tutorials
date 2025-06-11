---
"description": "Pelajari cara mengambil data dari sel Excel menggunakan Aspose.Cells untuk .NET dalam tutorial langkah demi langkah ini, cocok untuk pemula dan pengembang berpengalaman."
"linktitle": "Mengambil Data dari Sel di Excel"
"second_title": "Aspose.Cells .NET Excel feldolgozási API"
"title": "Mengambil Data dari Sel di Excel"
"url": "/id/net/excel-data-export-retrieval/retrieve-data-from-cells-in-excel/"
"weight": 10
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Mengambil Data dari Sel di Excel

## Bevezetés

Dalam hal mengelola data di Excel, kemampuan untuk membaca dan mengambil informasi dari sel sangatlah penting. Aspose.Cells untuk .NET adalah pustaka canggih yang memungkinkan pengembang untuk memanipulasi file Excel dengan mudah. Dalam tutorial ini, kita akan membahas cara mengambil data dari sel dalam buku kerja Excel menggunakan Aspose.Cells. Baik Anda seorang pengembang berpengalaman atau baru memulai, panduan ini akan memandu Anda melalui proses ini langkah demi langkah.

## Előfeltételek

Sebelum kita masuk ke kode, ada beberapa prasyarat yang perlu Anda penuhi:

1. Visual Studio: Pastikan Anda telah menginstal Visual Studio di komputer Anda. Ini adalah IDE yang akan kita gunakan untuk menulis dan menjalankan kode.
2. Aspose.Cells untuk .NET: Anda perlu memiliki pustaka Aspose.Cells. Anda dapat mengunduhnya dari [Aspose weboldal](https://releases.aspose.com/cells/net/).
3. Pengetahuan Dasar C#: Keakraban dengan pemrograman C# akan membantu Anda memahami contoh-contohnya dengan lebih baik.
4. File Excel: Siapkan file Excel (misalnya, `book1.xls`) yang akan Anda gunakan untuk tutorial ini.

Setelah Anda menyelesaikan prasyarat ini, kita dapat mulai menjelajahi cara mengambil data dari sel Excel.

## Csomagok importálása

Untuk memulai, Anda perlu mengimpor namespace yang diperlukan dalam proyek C# Anda. Ini akan memungkinkan Anda untuk memanfaatkan kelas dan metode yang disediakan oleh Aspose.Cells.

```csharp
using System.IO;
using Aspose.Cells;
using System;
```

Setelah namespace ini diimpor, Anda siap untuk memulai pengodean. Mari kita uraikan prosesnya menjadi beberapa langkah yang mudah dikelola.

## 1. lépés: Dokumentumkönyvtár beállítása

Langkah pertama adalah menentukan jalur ke direktori dokumen tempat file Excel Anda berada. Hal ini penting karena memberi tahu aplikasi tempat menemukan file yang ingin Anda gunakan.


```csharp
// A dokumentumok könyvtárának elérési útja.
string dataDir = "Your Document Directory";
```

Csere `"Your Document Directory"` a tényleges útvonallal, ahol a `book1.xls` file disimpan. Jalur ini adalah tempat Aspose.Cells akan mencari file saat Anda mencoba membukanya.

## Langkah 2: Buka Buku Kerja yang Ada

Sekarang setelah Anda menyiapkan direktori dokumen, langkah berikutnya adalah membuka buku kerja (file Excel) yang ingin Anda kerjakan.


```csharp
// Membuka buku kerja yang sudah ada
Workbook workbook = new Workbook(dataDir + "book1.xls");
```

Di sini, kita membuat `Workbook` objek dengan meneruskan jalur lengkap file Excel. Langkah ini menginisialisasi buku kerja dan membuatnya siap untuk pengambilan data.

## 3. lépés: Az első munkalap elérése

Setelah membuka buku kerja, Anda akan ingin mengakses lembar kerja tertentu tempat Anda ingin mengambil data. Dalam kasus ini, kita akan mengakses lembar kerja pertama.


```csharp
// Első munkalap elérése
Worksheet worksheet = workbook.Worksheets[0];
```

A `Worksheets` koleksi memungkinkan Anda mengakses lembar yang berbeda dalam buku kerja. Indeks `[0]` mengacu pada lembar kerja pertama. Jika Anda ingin mengakses lembar kerja berikutnya, Anda dapat mengubah indeksnya.

## Langkah 4: Melakukan Looping Melalui Sel

Sekarang setelah Anda memiliki lembar kerja, saatnya untuk mengulang setiap sel untuk mengambil data. Di sinilah keajaiban terjadi!


```csharp
foreach (Cell cell1 in worksheet.Cells)
{
    // Variabel untuk menyimpan nilai tipe data yang berbeda
    string stringValue;
    double doubleValue;
    bool boolValue;
    DateTime dateTimeValue;

    // Melewati jenis data yang terdapat dalam sel untuk evaluasi
    switch (cell1.Type)
    {
        // Mengevaluasi tipe data sel data untuk nilai string
        case CellValueType.IsString:
            stringValue = cell1.StringValue;
            Console.WriteLine("String Value: " + stringValue);
            break;

        // Mengevaluasi tipe data sel data untuk nilai ganda
        case CellValueType.IsNumeric:
            doubleValue = cell1.DoubleValue;
            Console.WriteLine("Double Value: " + doubleValue);
            break;

        // Mengevaluasi tipe data sel data untuk nilai boolean
        case CellValueType.IsBool:
            boolValue = cell1.BoolValue;
            Console.WriteLine("Bool Value: " + boolValue);
            break;

        // Mengevaluasi tipe data data sel untuk nilai tanggal/waktu
        case CellValueType.IsDateTime:
            dateTimeValue = cell1.DateTimeValue;
            Console.WriteLine("DateTime Value: " + dateTimeValue);
            break;

        // Mengevaluasi tipe data sel yang tidak diketahui
        case CellValueType.IsUnknown:
            stringValue = cell1.StringValue;
            Console.WriteLine("Unknown Value: " + stringValue);
            break;

        // Mengakhiri pengecekan tipe tipe data sel adalah null
        case CellValueType.IsNull:
            break;
    }
}
```

Pada langkah ini, kita melakukan pengulangan pada setiap sel di lembar kerja. Untuk setiap sel, kita memeriksa tipe datanya menggunakan `switch` pernyataan. Bergantung pada jenisnya, kami mengambil nilai dan mencetaknya ke konsol. Berikut ini rincian kasusnya:

- IsString: Jika sel berisi string, kami mengambilnya menggunakan `StringValue`.
- IsNumeric: Untuk nilai numerik, kami menggunakan `DoubleValue`.
- IsBool: Jika sel tersebut memiliki nilai boolean, kita mengaksesnya menggunakan `BoolValue`.
- IsDateTime: Untuk nilai tanggal dan waktu, kami menggunakan `DateTimeValue`.
- IsUnknown: Jika tipe data tidak diketahui, kami tetap mengambil representasi string.
- IsNull: Jika sel kosong, kita lewati saja.

## Következtetés

Mengambil data dari sel Excel menggunakan Aspose.Cells untuk .NET merupakan proses yang mudah. Dengan mengikuti langkah-langkah ini, Anda dapat mengekstrak berbagai jenis data dari file Excel secara efisien. Baik Anda sedang membangun alat pelaporan, mengotomatiskan entri data, atau hanya perlu menganalisis data, Aspose.Cells menyediakan fleksibilitas dan kekuatan yang Anda butuhkan untuk menyelesaikan pekerjaan.

## GYIK

### Mi az Aspose.Cells?  
Aspose.Cells adalah pustaka .NET yang memungkinkan pengembang untuk membuat, memanipulasi, dan mengonversi file Excel tanpa perlu menginstal Microsoft Excel.

### Ingyenesen használhatom az Aspose.Cells-t?  
Ya, Aspose.Cells menawarkan uji coba gratis yang dapat Anda gunakan untuk menguji fitur-fiturnya. Anda dapat mengunduhnya [itt](https://releases.aspose.com/).

### Jenis data apa yang dapat saya ambil dari sel Excel?  
Anda dapat mengambil berbagai tipe data, termasuk string, angka, boolean, dan nilai tanggal/waktu.

### Hogyan kaphatok támogatást az Aspose.Cells-hez?  
Támogatást kaphatsz, ha ellátogatsz a következő oldalra: [Aspose fórum](https://forum.aspose.com/c/cells/9) tempat Anda dapat mengajukan pertanyaan dan mendapatkan bantuan dari komunitas.

### Van ideiglenes jogosítvány?  
Ya, Aspose menawarkan lisensi sementara untuk tujuan evaluasi. Anda dapat menemukan informasi lebih lanjut [itt](https://purchase.aspose.com/temporary-license/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}