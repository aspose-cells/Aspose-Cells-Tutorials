---
title: Izinkan Pengguna Mengedit Rentang dalam Lembar Kerja menggunakan Aspose.Cells
linktitle: Izinkan Pengguna Mengedit Rentang dalam Lembar Kerja menggunakan Aspose.Cells
second_title: API Pemrosesan Excel Aspose.Cells .NET
description: Pelajari cara membuat rentang yang dapat diedit dalam lembar kerja Excel menggunakan Aspose.Cells untuk .NET, yang memungkinkan sel tertentu dapat diedit sambil mengamankan sisanya dengan perlindungan lembar kerja.
weight: 10
url: /id/net/worksheet-security/allow-edit-ranges/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Izinkan Pengguna Mengedit Rentang dalam Lembar Kerja menggunakan Aspose.Cells

## Perkenalan
Dokumen Excel sering kali berisi data sensitif atau konten terstruktur yang ingin Anda lindungi dari penyuntingan yang tidak diinginkan. Namun, mungkin ada sel atau rentang tertentu yang ingin Anda buat agar dapat diedit untuk pengguna tertentu. Di sinilah Aspose.Cells for .NET berperan sebagai alat canggih yang memungkinkan Anda melindungi seluruh lembar kerja sekaligus tetap memberikan izin edit ke rentang yang ditentukan. Bayangkan berbagi lembar kerja anggaran di mana hanya sel tertentu yang dapat diedit, dan sel lainnya tetap aman—Aspose.Cells mempermudah dan mengefisienkan hal ini.
## Prasyarat
Sebelum masuk ke bagian pengkodean, mari pastikan Anda memiliki semua yang dibutuhkan:
-  Aspose.Cells untuk .NET: Pastikan Anda telah menginstal pustaka Aspose.Cells untuk .NET. Anda dapat mengunduhnya[Di Sini](https://releases.aspose.com/cells/net/).
- Lingkungan Pengembangan: Visual Studio atau IDE apa pun yang kompatibel dengan C#.
- .NET Framework: Versi 4.0 atau yang lebih baru.
- Lisensi: Pertimbangkan untuk mendapatkan lisensi untuk menghindari batasan masa percobaan. Anda dapat memperoleh lisensi[lisensi sementara di sini](https://purchase.aspose.com/temporary-license/).
## Paket Impor
Pastikan untuk menyertakan namespace Aspose.Cells yang diperlukan di awal kode Anda:
```csharp
using System.IO;
using Aspose.Cells;
```
Ini akan memastikan bahwa Anda dapat mengakses semua kelas dan metode yang diperlukan untuk menyiapkan rentang yang dilindungi dalam file Excel.
Sekarang dasar-dasarnya sudah siap, mari kita bahas kodenya secara terperinci, selangkah demi selangkah.
## Langkah 1: Siapkan Direktori
Sebelum bekerja dengan file, Anda perlu menyiapkan direktori tempat Anda akan menyimpan file Excel. Ini memastikan file Anda terorganisasi dengan baik dan tersimpan dengan aman.
```csharp
// Tentukan jalur ke direktori dokumen Anda
string dataDir = "Your Document Directory";
// Periksa apakah direktori tersebut ada, jika tidak, buatlah
bool isExists = Directory.Exists(dataDir);
if (!isExists)
{
    Directory.CreateDirectory(dataDir);
}
```
Bagian kode ini memastikan bahwa direktori Anda siap untuk operasi berkas. Anggap saja ini sebagai dasar untuk semua hal yang mengikutinya.
## Langkah 2: Inisialisasi Buku Kerja dan Lembar Kerja
Sekarang, mari kita lanjutkan dengan membuat buku kerja baru dan mengakses lembar kerja default-nya.
```csharp
// Inisialisasi Buku Kerja baru
Workbook book = new Workbook();
// Akses lembar kerja pertama di buku kerja
Worksheet sheet = book.Worksheets[0];
```
Di sini, kita menginisialisasi buku kerja Excel dan memilih lembar kerja pertama di dalamnya. Lembar kerja ini akan menjadi kanvas tempat kita menerapkan pengaturan proteksi dan menentukan rentang yang dapat diedit.
## Langkah 3: Akses Koleksi Izinkan Edit Rentang
 Aspose.Cells memiliki fitur yang disebut`AllowEditRanges`, yang merupakan kumpulan rentang yang dapat diedit, bahkan saat lembar kerja diproteksi.
```csharp
// Mengakses koleksi Izinkan Edit Rentang
ProtectedRangeCollection allowRanges = sheet.AllowEditRanges;
```
Baris ini menyiapkan akses ke kumpulan rentang khusus yang dapat diedit. Anggap saja ini sebagai area "VIP" di lembar kerja Anda, tempat hanya rentang tertentu yang diizinkan melewati perlindungan.
## Langkah 4: Tentukan dan Buat Rentang Terlindungi
Sekarang, mari kita definisikan dan buat rentang terproteksi di lembar kerja kita. Kita akan tentukan sel awal dan akhir untuk rentang ini.
```csharp
// Tentukan variabel ProtectedRange
ProtectedRange protectedRange;
// Tambahkan rentang baru ke koleksi dengan nama dan posisi sel tertentu
int idx = allowRanges.Add("EditableRange", 1, 1, 3, 3);
protectedRange = allowRanges[idx];
```
Dalam blok kode ini:
- `EditableRange` adalah nama yang diberikan pada rentang tersebut.
- Angka (1, 1, 3, 3) menentukan koordinat rentang, yang berarti dimulai dari sel B2 (baris 1, kolom 1) hingga sel D4 (baris 3, kolom 3).
## Langkah 5: Tetapkan Kata Sandi untuk Rentang yang Dilindungi
Untuk keamanan tambahan, Anda dapat menetapkan kata sandi untuk rentang yang dilindungi. Langkah ini menambahkan lapisan perlindungan ekstra untuk memastikan bahwa hanya pengguna yang berwenang yang dapat mengedit rentang tersebut.
```csharp
// Tetapkan kata sandi untuk rentang yang dapat diedit
protectedRange.Password = "123";
```
Di sini, kami telah menambahkan kata sandi (`"123"`) ke rentang yang dilindungi. Persyaratan kata sandi ini memberikan tingkat kontrol ekstra atas siapa yang dapat membuat perubahan.
## Langkah 6: Lindungi Lembar Kerja
Setelah rentang yang dapat diedit ditetapkan, langkah berikutnya adalah melindungi seluruh lembar kerja. Pengaturan perlindungan ini akan memastikan bahwa semua sel di luar rentang yang ditentukan terkunci dan tidak dapat diedit.
```csharp
// Terapkan perlindungan ke lembar kerja, membuat semua sel lainnya tidak dapat diedit
sheet.Protect(ProtectionType.All);
```
 Itu`Protect`metode mengunci seluruh lembar kerja, kecuali untuk rentang yang telah kami tetapkan sebagai dapat diedit. Langkah ini pada dasarnya menciptakan lingkungan "hanya-baca" yang aman, dengan akses ke sel tertentu sesuai kebutuhan.
## Langkah 7: Simpan Buku Kerja
Langkah terakhir adalah menyimpan buku kerja, sehingga pengaturan Anda diterapkan dan disimpan.
```csharp
// Simpan file Excel ke direktori yang ditentukan
book.Save(dataDir + "protectedrange.out.xls");
```
Pada langkah ini, kita menyimpan buku kerja kita sebagai “protectedrange.out.xls” di direktori yang kita buat pada Langkah 1. Sekarang, Anda memiliki file Excel yang berfungsi penuh dan aman, di mana hanya rentang tertentu yang dapat diedit!
## Kesimpulan
Aspose.Cells untuk .NET menyediakan cara yang sangat baik untuk mengelola perlindungan dan izin dalam file Excel Anda. Dengan membuat rentang yang dapat diedit, Anda dapat mengamankan lembar kerja Anda sekaligus tetap mengizinkan area tertentu untuk tetap dapat diakses. Fungsionalitas ini sangat berguna untuk dokumen kolaboratif, di mana hanya beberapa sel yang boleh dibuka untuk diedit sementara yang lain tetap terkunci.
## Pertanyaan yang Sering Diajukan
### Bisakah saya menambahkan beberapa rentang yang dapat diedit ke lembar kerja?
Ya, Anda dapat menambahkan beberapa rentang hanya dengan mengulangi`allowRanges.Add()` metode untuk setiap rentang baru.
### Bagaimana jika saya ingin menghapus rentang yang dilindungi nanti?
 Gunakan`allowRanges.RemoveAt()` metode dengan indeks rentang yang ingin Anda hapus.
### Bisakah saya menetapkan kata sandi yang berbeda untuk setiap rentang?
 Tentu saja. Setiap`ProtectedRange` dapat memiliki kata sandinya sendiri yang unik, sehingga memberi Anda kontrol yang terperinci.
### Apa yang terjadi jika saya melindungi lembar kerja tanpa rentang yang dapat diedit?
Jika Anda tidak menentukan rentang yang dapat diedit, seluruh lembar kerja tidak akan dapat diedit lagi setelah diproteksi.
### Apakah jangkauan yang dilindungi terlihat oleh pengguna lain?
Tidak, perlindungannya bersifat internal. Pengguna hanya akan diminta memasukkan kata sandi jika mereka mencoba mengedit area yang dilindungi.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
