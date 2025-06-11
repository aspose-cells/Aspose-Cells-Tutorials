---
"date": "2025-04-05"
"description": "Pelajari cara mengimpor data berformat HTML secara mulus dari DataTables ke dalam lembar kerja Excel menggunakan Aspose.Cells untuk .NET, mempertahankan semua gaya teks dan meningkatkan produktivitas Anda."
"title": "Cara Mengimpor DataTable Berformat HTML ke Excel Menggunakan Aspose.Cells untuk .NET"
"url": "/id/net/import-export/aspose-cells-net-data-table-import-html-formatting/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Cara Mengimpor DataTable Berformat HTML ke Excel dengan Aspose.Cells untuk .NET

## Bevezetés

Apakah Anda kesulitan memformat halaman web atau data basis data yang diimpor secara manual di Excel? Anda tidak sendirian! Pengembang sering kali perlu mempertahankan gaya teks seperti tebal dan miring, yang penting untuk keterbacaan. Dengan Aspose.Cells untuk .NET, mengimpor DataTable yang berisi string berformat HTML ke dalam buku kerja Excel sambil mempertahankan gaya menjadi mudah.

Dalam tutorial ini, Anda akan mempelajari cara mengimpor data berformat HTML dari DataTable ke Excel menggunakan Aspose.Cells, memastikan data Anda muncul persis seperti yang diinginkan dalam spreadsheet.

**Amit tanulni fogsz:**
- Menyiapkan dan mengonfigurasi Aspose.Cells untuk .NET
- Mengimpor DataTables dengan format HTML menggunakan Aspose.Cells
- Menyesuaikan ukuran baris dan kolom secara otomatis agar sesuai dengan konten
- Menyimpan buku kerja dalam berbagai format, seperti XLSX dan ODS

Mari kita mulai dengan memastikan Anda memiliki prasyarat yang diperlukan!

## Előfeltételek

Sebelum menyelaminya, pastikan Anda memiliki:
- **Szükséges könyvtárak:** Aspose.Cells untuk .NET (versi 21.9 atau lebih baru)
- **Környezeti beállítási követelmények:** Visual Studio dengan .NET Core SDK terpasang
- **Előfeltételek a tudáshoz:** Pemahaman dasar tentang C# dan keakraban dengan DataTables di .NET

## Az Aspose.Cells beállítása .NET-hez

Pertama, instal pustaka Aspose.Cells di proyek Anda melalui:

**.NET parancssori felület használata:**
```bash
dotnet add package Aspose.Cells
```

**A csomagkezelő konzol használata:**
```plaintext
PM> NuGet\Install-Package Aspose.Cells
```

Dapatkan lisensi untuk fungsionalitas penuh dari [Aspose weboldal](https://purchase.aspose.com/temporary-license/) untuk menjelajahi semua fitur tanpa batasan.

### Alapvető inicializálás

Berikut cara menginisialisasi proyek Anda dengan Aspose.Cells:
```csharp
using Aspose.Cells;

// Új munkafüzet-objektum inicializálása
Workbook workbook = new Workbook();
```

Ini menetapkan dasar untuk bekerja dengan file Excel di .NET menggunakan Aspose.Cells.

## Megvalósítási útmutató

Mari kita uraikan pengimporan DataTables dengan format HTML ke dalam langkah-langkah yang jelas.

### Mempersiapkan Sumber Data Anda

**Áttekintés:**
Mulailah dengan menyiapkan DataTable dengan contoh data yang menyertakan string berformat HTML untuk menunjukkan kemampuan gaya Aspose.Cells.
```csharp
using System.Data;

// Tetapkan direktori sumber dan keluaran Anda di sini
string SourceDir = "YOUR_SOURCE_DIRECTORY";
string OutputDir = "YOUR_OUTPUT_DIRECTORY";

// Siapkan DataTable dengan beberapa nilai berformat HTML
dataTable = new DataTable("Products");
dataTable.Columns.Add("Product ID", typeof(Int32));
dataTable.Columns.Add("Product Name", typeof(string));
dataTable.Columns.Add("Units In Stock", typeof(Int32));

// Menambahkan baris dengan format HTML
DataRow dr = dataTable.NewRow();
dr[0] = 1;
dr[1] = "<i>Aniseed</i> Syrup"; // HTML miring untuk nama produk
dr[2] = 15;
dataTable.Rows.Add(dr);

dr = dataTable.NewRow();
dr[0] = 2;
dr[1] = "<b>Boston Crab Meat</b>"; // HTML tebal untuk nama produk
dr[2] = 123;
dataTable.Rows.Add(dr);
```

### Mengatur Opsi Impor

**Konfigurasikan Opsi Tabel Impor:**
Használat `ImportTableOptions` untuk menentukan bahwa nilai sel harus ditafsirkan sebagai string HTML.
```csharp
// Buat opsi impor untuk menangani string berformat HTML
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.IsFieldNameShown = true; // Sertakan tajuk kolom dalam impor
importOptions.IsHtmlString = true; // Menafsirkan nilai sel sebagai string HTML
```

### Mengimpor Data ke Excel

**Áttekintés:**
Buat buku kerja dan lembar kerja, lalu gunakan `ImportData` untuk membawa DataTable Anda ke Excel dengan semua format utuh.
```csharp
// Buat buku kerja dan dapatkan lembar kerja pertama
Workbook workbook = new Workbook();
Worksheet worksheet = workbook.Worksheets[0];

// Impor DataTable mulai dari baris 0, kolom 0
worksheet.Cells.ImportData(dataTable, 0, 0, importOptions);

// Sesuaikan ukuran baris dan kolom untuk keterbacaan yang lebih baik
worksheet.AutoFitRows();
worksheet.AutoFitColumns();
```

### Menyimpan Buku Kerja Anda

Terakhir, simpan buku kerja Anda dalam format XLSX dan ODS untuk memastikan kompatibilitas di berbagai aplikasi lembar kerja.
```csharp
string output1Path = OutputDir + "Output.out.xlsx";
string output2Path = OutputDir + "Output.out.ods";

// Simpan buku kerja dalam dua format
workbook.Save(output1Path);
workbook.Save(output2Path);
```

## Gyakorlati alkalmazások

Fitur ini sangat berharga untuk skenario di mana penyajian data penting, seperti:
- **Jelentéstétel:** Menerapkan gaya pada laporan keuangan secara otomatis.
- **Adatmigráció:** Memindahkan data yang diambil dari web ke Excel sambil tetap mempertahankan format HTML.
- **Készletgazdálkodás:** Menampilkan rincian produk dengan penekanan pada atribut penting.

Mengintegrasikan fungsi ini dapat secara signifikan menyederhanakan proses dalam tugas analitik dan pelaporan bisnis.

## Teljesítménybeli szempontok

Saat bekerja dengan kumpulan data besar, pertimbangkan hal berikut:
- **Optimalkan Ukuran DataTable:** Hanya sertakan kolom yang diperlukan untuk mengurangi penggunaan memori.
- **Kelola Sumber Daya Buku Kerja:** Buang buku kerja segera setelah menyimpan untuk mengosongkan sumber daya.
- **Gunakan Fitur Aspose.Cells:** Memanfaatkan pengoptimalan bawaan untuk menangani struktur data kompleks secara efisien.

## Következtetés

Anda telah menguasai cara mengimpor DataTables berformat HTML ke Excel menggunakan Aspose.Cells for .NET. Keterampilan ini menghemat waktu dan meningkatkan kualitas presentasi laporan dan dokumen Anda.

Untuk eksplorasi lebih lanjut, pertimbangkan untuk bereksperimen dengan fitur Aspose.Cells lainnya seperti integrasi bagan atau pemformatan bersyarat. Siap untuk melangkah lebih jauh? Coba terapkan solusi ini di proyek Anda berikutnya!

## GYIK szekció

**T: Bagaimana cara menangani kumpulan data besar dengan konten HTML?**
A: Optimalkan ukuran DataTable dan pastikan manajemen memori yang efisien dalam .NET menggunakan praktik terbaik yang disediakan oleh Aspose.Cells.

**T: Dapatkah saya mengimpor data dari sumber selain DataTables?**
A: Ya, Aspose.Cells mendukung berbagai sumber data. Periksa dokumentasi untuk keterangan lebih lanjut.

**T: Bagaimana jika tag HTML saya tidak ditampilkan dengan benar di Excel?**
A: Pastikan Anda `ImportTableOptions` dikonfigurasi dengan `IsHtmlString = true`.

**T: Apakah ada versi gratis Aspose.Cells yang tersedia?**
A: Lisensi uji coba memungkinkan Anda untuk menjelajahi fitur lengkap untuk sementara. Kunjungi [Aspose oldal](https://purchase.aspose.com/temporary-license/) további információkért.

**T: Dapatkah saya menyimpan buku kerja dalam format selain XLSX dan ODS?**
A: Ya, Aspose.Cells mendukung banyak format file termasuk PDF, CSV, dan banyak lagi.

## Erőforrás

Untuk bacaan dan sumber daya lebih lanjut, kunjungi:
- [Aspose.Cells dokumentáció](https://reference.aspose.com/cells/net/)
- [Legújabb kiadások letöltése](https://releases.aspose.com/cells/net/)
- [Licencek vásárlása](https://purchase.aspose.com/buy)
- [Ingyenes próbaverzió letöltése](https://releases.aspose.com/cells/net/)
- [Akuisisi Lisensi Sementara](https://purchase.aspose.com/temporary-license/)
- [Aspose Támogatási Fórum](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}