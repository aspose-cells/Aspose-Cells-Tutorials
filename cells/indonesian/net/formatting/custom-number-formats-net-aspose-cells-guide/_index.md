---
"date": "2025-04-05"
"description": "Pelajari cara menerapkan format angka kustom di .NET menggunakan Aspose.Cells untuk presentasi data Excel yang akurat. Panduan ini mencakup pengaturan, pemformatan tanggal, persentase, dan mata uang."
"title": "Cara Menggunakan Format Angka Kustom di .NET dengan Aspose.Cells&#58; Panduan Langkah demi Langkah"
"url": "/id/net/formatting/custom-number-formats-net-aspose-cells-guide/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Cara Menggunakan Format Angka Kustom di .NET dengan Aspose.Cells: Panduan Langkah demi Langkah

## Bevezetés

Tingkatkan manipulasi berkas Excel Anda menggunakan C# dan .NET dengan kontrol yang tepat atas format angka. Tutorial ini memandu Anda dalam pengaturan format angka kustom dalam aplikasi .NET menggunakan Aspose.Cells for .NET, pustaka canggih yang dirancang untuk manipulasi Excel.

Dengan memanfaatkan Aspose.Cells, terapkan berbagai gaya pada data dengan mudah, memastikan kejelasan dan ketepatan dalam laporan Anda. Baik memformat tanggal, persentase, atau nilai mata uang, menguasai fungsi ini akan memperlancar alur kerja Anda.

**Amit tanulni fogsz:**
- Az Aspose.Cells beállítása .NET-hez
- Menerapkan format angka khusus dengan C#
- Menerapkan gaya secara terprogram ke sel Excel
- Aplikasi nyata dari format angka khusus

## Előfeltételek

Pastikan Anda memiliki hal berikut sebelum memulai:
1. **Fejlesztői környezet**: Pengaturan kerja .NET dengan Visual Studio atau IDE apa pun yang kompatibel.
2. **Aspose.Cells .NET könyvtárhoz**: Versi 22.x atau yang lebih baru diperlukan untuk panduan ini.
3. **Alapvető C# ismeretek**:Keakraban dengan sintaksis C# dan konsep pemrograman akan membantu Anda mengikutinya dengan lancar.

## Az Aspose.Cells beállítása .NET-hez

Untuk menggunakan Aspose.Cells di proyek Anda, instal pustaka menggunakan .NET CLI atau Konsol Manajer Paket dalam Visual Studio.

**.NET parancssori felület telepítése:**
```bash
dotnet add package Aspose.Cells
```

**Csomagkezelő telepítése:**
```powershell
PM> NuGet\Install-Package Aspose.Cells
```

### Licencszerzés

Aspose.Cells menawarkan uji coba gratis untuk evaluasi dan opsi untuk penggunaan lanjutan melalui lisensi sementara atau yang dibeli.
- **Ingyenes próbaverzió**Letöltés innen: [itt](https://releases.aspose.com/cells/net/).
- **Ideiglenes engedély**Jelentkezés: [Aspose ideiglenes licencoldal](https://purchase.aspose.com/temporary-license/) az értékelési korlátok megszüntetése érdekében.
- **Vásárlás**A teljes hozzáférésért látogassa meg a következőt: [Vásárlási oldal](https://purchase.aspose.com/buy).

Az Aspose.Cells inicializálása a projektben:
```csharp
// Impor namespace
using Aspose.Cells;

// Új munkafüzet-objektum inicializálása
Workbook workbook = new Workbook();
```

## Megvalósítási útmutató

Kami akan membahas fitur-fitur utama untuk menyesuaikan format angka menggunakan Aspose.Cells.

### Menambahkan Format Tanggal Kustom
**Áttekintés**: Pelajari cara memformat tanggal di sel Excel dengan gaya kustom.
1. **Membuat atau Mengakses Lembar Kerja**
   ```csharp
   int sheetIndex = workbook.Worksheets.Add();
   Worksheet worksheet = workbook.Worksheets[sheetIndex];
   ```
2. **Tetapkan Tanggal Sistem Saat Ini dengan Format Kustom**
   Tambahkan tanggal saat ini ke sel "A1" dan terapkan format tampilan khusus.
   ```csharp
   // Masukkan tanggal sistem saat ini ke A1
   worksheet.Cells["A1"].PutValue(DateTime.Now);

   // Ambil objek gaya untuk penyesuaian
   Style style = worksheet.Cells["A1"].GetStyle();

   // Atur format angka kustom ke "d-mmm-yy"
   style.Custom = "d-mmm-yy";

   // Terapkan gaya yang disesuaikan kembali ke sel A1
   worksheet.Cells["A1"].SetStyle(style);
   ```

### Memformat Nilai Numerik sebagai Persentase
**Áttekintés**: Menampilkan nilai numerik dalam format persentase.
1. **Sisipkan dan Format Nilai**
   ```csharp
   // Tambahkan nilai numerik ke sel A2
   worksheet.Cells["A2"].PutValue(20);

   // Ambil gaya untuk pemformatan
   Style style = worksheet.Cells["A2"].GetStyle();

   // Terapkan format angka kustom sebagai persentase
   style.Custom = "0.0%";

   // Atur kembali gaya yang diformat ke sel A2
   worksheet.Cells["A2"].SetStyle(style);
   ```

### Menerapkan Format Mata Uang
**Áttekintés**: Menampilkan angka dalam format mata uang, dengan format khusus untuk nilai negatif.
1. **Masukkan dan Gaya Nilai Mata Uang**
   ```csharp
   // Tambahkan nilai ke sel A3
   worksheet.Cells["A3"].PutValue(2546);

   // Mengakses objek gaya
   Style style = worksheet.Cells["A3"].GetStyle();

   // Atur format mata uang khusus
   style.Custom = "\u00a3#,##0;[Red]$-#,##0";

   // Terapkan ke sel A3
   worksheet.Cells["A3"].SetStyle(style);
   ```

## Gyakorlati alkalmazások

Pemformatan angka khusus sangat berharga dalam skenario seperti:
1. **Pénzügyi jelentések**: Memformat nilai mata uang agar jelas.
2. **Dasbor Penjualan**: Menampilkan angka penjualan sebagai persentase untuk menyoroti metrik kinerja.
3. **Perencanaan Acara**: Menggunakan format tanggal untuk mengatur dan menyajikan jadwal acara dengan mulus.

## Teljesítménybeli szempontok
Saat bekerja dengan kumpulan data besar, optimalkan kinerja Aspose.Cells:
- Minimalkan penggunaan memori dengan membuang objek segera menggunakan `GC.Collect()` setelah menyimpan berkas.
- Memanfaatkan aliran untuk membaca/menulis file Excel alih-alih memuat seluruh dokumen ke dalam memori.
- Terapkan praktik terbaik dalam manajemen memori .NET untuk menjaga efisiensi.

## Következtetés
Dengan mengikuti panduan ini, Anda telah mempelajari cara menerapkan format angka kustom dalam aplikasi .NET Anda menggunakan Aspose.Cells. Kemampuan ini meningkatkan penyajian data dan memastikan keakuratan serta daya tarik visual dalam laporan dan spreadsheet.

**Következő lépések**Bereksperimenlah dengan opsi pemformatan lain yang tersedia dalam Aspose.Cells, seperti pemformatan bersyarat atau penyempurnaan bagan.

## GYIK szekció
1. **Hogyan szerezhetek ideiglenes licencet az Aspose.Cells-hez?**
   - Daftar di [Ideiglenes licencoldal](https://purchase.aspose.com/temporary-license/).
2. **Format apa yang didukung untuk gaya angka kustom di Aspose.Cells?**
   - Tanggal, persentase, mata uang, dan lainnya, menggunakan string format Excel standar.
3. **Bisakah saya menggunakan Aspose.Cells dengan bahasa .NET lain seperti VB.NET?**
   - Ya, pustaka ini kompatibel dengan semua bahasa yang didukung .NET.
4. **Apa yang harus saya lakukan jika angka yang diformat tidak ditampilkan dengan benar?**
   - Periksa kembali format angka kustom Anda untuk menemukan kesalahan ketik atau kesalahan sintaksis.
5. **Hol találok további példákat az Aspose.Cells használatára?**
   - Jelajahi dokumentasi terperinci dan contoh kode di [Aspose dokumentáció](https://reference.aspose.com/cells/net/).

## Erőforrás
- [Aspose.Cells .NET dokumentációhoz](https://reference.aspose.com/cells/net/)
- [Legújabb verzió letöltése](https://releases.aspose.com/cells/net/)
- [Licenc vásárlása](https://purchase.aspose.com/buy)
- [Ingyenes próbaverzió letöltése](https://releases.aspose.com/cells/net/)
- [Ideiglenes engedélykérelem](https://purchase.aspose.com/temporary-license/)
- [Aspose Támogatási Fórum](https://forum.aspose.com/c/cells/9)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}