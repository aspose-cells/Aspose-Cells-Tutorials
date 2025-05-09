---
"date": "2025-04-05"
"description": "Pelajari cara mengganti sistem tanggal default Excel dari 1899 ke 1904 dengan mudah menggunakan Aspose.Cells .NET. Panduan ini menyediakan petunjuk langkah demi langkah dan contoh kode untuk integrasi yang lancar."
"title": "Ubah Sistem Tanggal Excel ke 1904 menggunakan Aspose.Cells .NET"
"url": "/id/net/calculation-engine/change-excel-date-system-aspose-cells-net/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Ubah Sistem Tanggal Excel ke 1904 menggunakan Aspose.Cells .NET

## Bevezetés

Apakah Anda kesulitan dengan sistem tanggal default 1899 di buku kerja Excel Anda? Beralih ke sistem tanggal 1904 sering kali diperlukan untuk kompatibilitas atau persyaratan regional tertentu. Tutorial ini akan memandu Anda menggunakan Aspose.Cells .NET untuk mengubah sistem tanggal buku kerja Anda dengan mudah.

### Amit tanulni fogsz:
- Cara mengganti sistem tanggal Excel dari 1899 ke 1904.
- Langkah-langkah untuk memuat dan menyimpan buku kerja Excel dengan pengaturan baru.
- Fitur utama Aspose.Cells .NET untuk menangani file Excel.

Mari kita bahas cara menerapkan perubahan ini dengan lancar. Pastikan Anda memenuhi semua prasyarat sebelum kita melanjutkan.

## Előfeltételek

Sebelum memulai, pastikan Anda memiliki hal berikut:
- **Aspose.Cells könyvtár**: Instal versi 21.11 atau yang lebih baru.
- **Környezet beállítása**: Tutorial ini mengasumsikan lingkungan .NET (sebaiknya .NET Core atau .NET Framework).
- **C# alapismeretek**Kemampuan membaca dan menulis berkas dalam .NET akan sangat membantu.

## Az Aspose.Cells beállítása .NET-hez

Untuk menggunakan Aspose.Cells, Anda perlu menginstalnya melalui metode pilihan Anda. Berikut caranya:

### Instalasi menggunakan .NET CLI
```bash
dotnet add package Aspose.Cells
```

### Instalasi menggunakan Package Manager
```powershell
PM> Install-Package Aspose.Cells
```

#### Licencszerzés

Mulailah dengan uji coba gratis atau minta lisensi sementara untuk menjelajahi semua fitur tanpa batasan. Untuk pembelian, kunjungi situs web resmi [Aspose weboldal](https://purchase.aspose.com/buy).

Setelah instalasi, inisialisasi proyek Anda dengan menyertakan namespace Aspose.Cells dalam file Anda:

```csharp
using Aspose.Cells;
```

## Megvalósítási útmutató

Kami akan membagi panduan ini menjadi dua bagian utama berdasarkan fungsionalitas.

### Mengubah Sistem Tanggal Buku Kerja Excel

#### Áttekintés
Fitur ini mengubah sistem tanggal buku kerja Excel dari default (1899) ke 1904, diperlukan untuk kompatibilitas atau persyaratan regional tertentu.

##### Lépésről lépésre történő megvalósítás:

**1. Buka File Excel**
```csharp
string SourceDir = "YOUR_SOURCE_DIRECTORY";
Workbook workbook = new Workbook(SourceDir + "sampleImplement1904DateSystem.xlsx");
```
Itt, `Workbook` diinisialisasi dengan jalur file yang ada untuk memuat dokumen Excel Anda.

**2. Ubah Sistem Tanggal**
```csharp
workbook.Settings.Date1904 = true;
```
Baris ini mengatur sistem tanggal buku kerja menjadi 1904 dengan memodifikasi `Date1904` ingatlan.

**3. Simpan Buku Kerja yang Diperbarui**
```csharp
string outputDir = "YOUR_OUTPUT_DIRECTORY";
workbook.Save(outputDir + "outputImplement1904DateSystem_1904DateSystem.xlsx");
```
Buku kerja disimpan dengan nama baru, yang mencerminkan konfigurasi sistem tanggal yang diperbarui.

### Memuat dan Menyimpan Buku Kerja

#### Áttekintés
Pelajari cara memuat file Excel secara efisien dari direktori dan menyimpannya di tempat lain menggunakan Aspose.Cells.

##### Lépésről lépésre történő megvalósítás:

**1. Buka File Excel**
```csharp
Workbook workbook = new Workbook(SourceDir + "sampleImplement1904DateSystem.xlsx");
```
Langkah ini serupa dengan contoh kita sebelumnya, di mana kita membuka buku kerja untuk manipulasi.

**2. Simpan Buku Kerja**
```csharp
workbook.Save(outputDir + "outputSaveWorkbook.xlsx");
```
Di sini, buku kerja disimpan ke lokasi baru dengan nama file yang ditentukan.

## Gyakorlati alkalmazások

1. **Kepatuhan Regional**: Mengganti sistem tanggal untuk memenuhi standar dan peraturan setempat.
2. **Adatmigráció**: Memastikan konsistensi data selama migrasi antara versi Excel yang berbeda atau pengaturan regional.
3. **Interoperabilitas**Meningkatkan kompatibilitas saat berbagi file dengan pengguna di wilayah yang menggunakan sistem tanggal 1904 secara default.

## Teljesítménybeli szempontok

- **Erőforrás-felhasználás optimalizálása**: Tutup buku kerja segera setelah diproses untuk mengosongkan memori.
- **Bevált gyakorlatok**: Gunakan Aspose.Cells dalam blok try-catch untuk menangani pengecualian dengan baik dan memastikan kinerja aplikasi yang lancar.

## Következtetés

Dalam panduan ini, kami membahas cara mengubah sistem tanggal buku kerja Excel menggunakan Aspose.Cells .NET. Dengan mengikuti langkah-langkah ini, Anda dapat memodifikasi buku kerja secara efisien untuk memenuhi kebutuhan atau standar tertentu.

### Következő lépések:
- Jelajahi fitur Aspose.Cells lainnya untuk manipulasi Excel tingkat lanjut.
- Pertimbangkan untuk mengintegrasikan Aspose.Cells dengan layanan cloud untuk meningkatkan kemampuan pemrosesan data.

Siap untuk mencobanya? Terapkan solusinya dalam proyek Anda dan saksikan peningkatan kompatibilitas secara langsung!

## GYIK szekció

**Q1. Dapatkah saya beralih kembali dari sistem penanggalan 1904 ke 1899 menggunakan Aspose.Cells .NET?**
A1. Ya, atur `workbook.Settings.Date1904` hogy `false` untuk mengembalikan perubahan.

**Q2. Apa saja kesalahan umum saat mengubah sistem tanggal di buku kerja Excel?**
A2. Masalah umum meliputi kesalahan jalur file atau ekstensi file yang salah. Pastikan jalur dan format sudah benar.

**Q3. Bagaimana Aspose.Cells menangani file Excel berukuran besar selama konversi?**
A3. Mengelola memori secara efisien, tetapi untuk file yang sangat besar, pertimbangkan untuk membaginya menjadi bagian-bagian yang lebih kecil.

**Q4. Apakah ada perbedaan kinerja antara sistem tanggal 1899 dan 1904?**
A4. Kinerjanya serupa; namun, kompatibilitas dapat ditingkatkan tergantung pada pengaturan regional.

**Q5. Bisakah Aspose.Cells mengotomatiskan tugas Excel lebih dari sekadar mengubah sistem tanggal?**
A5. Tentu saja! Program ini menawarkan fitur untuk membuat, mengedit, mengonversi, dan menganalisis file Excel secara terprogram.

## Erőforrás
- **Dokumentáció**: [Aspose.Cells .NET API referencia](https://reference.aspose.com/cells/net/)
- **Legújabb verzió letöltése**: [Kiadások oldala](https://releases.aspose.com/cells/net/)
- **Licenc vásárlása**: [Aspose Vásárlási Oldal](https://purchase.aspose.com/buy)
- **Ingyenes próbaverzió**: [Ingyenes próbaverziók kipróbálása](https://releases.aspose.com/cells/net/)
- **Ideiglenes engedély**: [Ideiglenes engedély igénylése](https://purchase.aspose.com/temporary-license/)
- **Támogatási fórum**: [Aspose támogató közösség](https://forum.aspose.com/c/cells/9)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}