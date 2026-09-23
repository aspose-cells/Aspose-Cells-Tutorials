---
category: general
date: 2026-03-29
description: Pelajari cara menyisipkan baris di GridJs dengan cepat. Panduan ini juga
  mencakup cara menambahkan baris dan menambahkan beberapa baris ke grid dengan operasi
  batch.
draft: false
keywords:
- how to insert rows
- how to add rows
- add multiple rows grid
- batch row insertion
- large grid performance
language: id
og_description: Pelajari cara menyisipkan baris di GridJs dengan cepat. Panduan ini
  menunjukkan cara menambahkan baris, menambahkan beberapa baris ke grid, dan menangani
  penyisipan batch besar.
og_title: Cara Menyisipkan Baris di GridJs – Tambahkan Banyak Baris ke Grid dengan
  Efisien
tags:
- GridJs
- C#
- data‑grid
title: Cara Menyisipkan Baris di GridJs – Tambahkan Beberapa Baris ke Grid Secara
  Efisien
url: /id/net/row-and-column-management/how-to-insert-rows-in-gridjs-add-multiple-rows-grid-efficien/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Cara Menyisipkan Baris di GridJs – Tambahkan Banyak Baris Grid Secara Efisien

Pernah bertanya‑tanya **cara menyisipkan baris** ke dalam tabel GridJs yang sangat besar tanpa membekukan UI? Mungkin Anda pernah menemui kesulitan saat **menambahkan baris** satu per satu dan kinerjanya menjadi buruk. Kabar baiknya, GridJs menyediakan API batch yang memungkinkan Anda **menambahkan banyak baris grid** dalam satu panggilan, sehingga tetap cepat bahkan ketika menangani jutaan entri.

Dalam tutorial ini kita akan membahas contoh lengkap yang dapat dijalankan, yang menunjukkan **cara menyisipkan baris** menggunakan `InsertRowsBatch`. Anda akan melihat mengapa batching penting, cara memverifikasi hasilnya, dan hal‑hal yang perlu diwaspadai ketika indeks target sangat besar. Pada akhir tutorial Anda akan dapat menambahkan seribu catatan baru ke instansi GridJs mana pun dengan percaya diri.

## Prasyarat

Sebelum kita mulai, pastikan Anda memiliki:

- .NET 6.0 atau lebih baru (kode dapat dikompilasi dengan SDK terbaru apa pun)
- Referensi ke paket NuGet `GridJs` (atau DLL jika Anda menggunakan build khusus)
- Pengetahuan dasar C# – tidak perlu menjadi ahli, cukup nyaman dengan kelas dan metode
- IDE atau editor pilihan Anda (Visual Studio, Rider, VS Code… semuanya dapat digunakan)

> **Pro tip:** Jika Anda berencana bekerja dengan grid yang sangat besar (puluhan juta baris), aktifkan `gridJs.EnableVirtualization = true;` untuk menjaga rendering UI tetap ringan.

## Langkah 1: Buat dan Konfigurasikan Instansi GridJs

Hal pertama yang perlu dilakukan: Anda memerlukan objek `GridJs` yang aktif. Anggaplah ini sebagai kanvas tempat Anda akan melukis baris.

```csharp
using System;
using GridJsLibrary;   // Assume this is the namespace for GridJs

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1 – Initialize the grid
            GridJs gridJs = new GridJs();

            // Optional: turn on virtualization for huge data sets
            gridJs.EnableVirtualization = true;

            // Populate the grid with some dummy data so we can see the effect
            SeedInitialData(gridJs);

            // Now we’re ready to insert rows in bulk
            InsertRowsInBatch(gridJs);
        }

        // Helper: add 2 000 000 rows so our batch lands at index 2 000 001
        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }
```

> **Mengapa langkah ini penting:** Menginisialisasi grid dan, bila perlu, menyiapkan data awal mencerminkan skenario dunia nyata di mana grid sudah berisi banyak informasi. Penyisipan batch yang akan kita lakukan nanti harus menghormati indeks berbasis nol, sehingga kami mengisi data sebelumnya untuk memperlihatkan titik penyisipan yang tepat.

## Langkah 2: Gunakan `InsertRowsBatch` untuk **Menambahkan Banyak Baris Grid**

Sekarang inti tutorial – pemanggilan yang sebenarnya **menambahkan baris** secara massal. Tanda tangan metodenya adalah `InsertRowsBatch(int startIndex, int count)`. Pada contoh kami, kami akan memulai pada indeks 2 000 000 (yang merupakan baris ke‑2 000 001) dan menambahkan sepuluh baris.

```csharp
        // Step 2 – Insert a batch of rows
        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based, so this is row 2 000 001
            int rowsToAdd = 10;

            // The batch call creates placeholder rows; you can later populate them
            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Verify by reading back a few rows
            VerifyInsertion(grid, startIndex, rowsToAdd);
        }
```

> **Cara kerjanya:** `InsertRowsBatch` mengalokasikan jumlah baris yang diminta secara internal dan menggeser baris yang ada ke bawah. Karena operasi ini dilakukan dalam satu transaksi, UI hanya menyegarkan sekali, itulah mengapa metode ini direkomendasikan untuk **cara menambahkan baris** secara efisien.

## Langkah 3: Verifikasi Penyisipan – Apakah Baris-Baris Sudah Di Tempat yang Diharapkan?

Setelah operasi batch, Anda ingin memastikan baris‑baris berada di lokasi yang tepat. Helper berikut membaca baris pertama dan terakhir dari blok yang baru ditambahkan serta mencetaknya ke konsol.

```csharp
        // Step 3 – Simple verification
        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

**Output yang diharapkan**

```
Initial seed completed – 2 000 000 rows present.
Inserted 10 rows starting at index 2000001.
Verifying inserted rows:
Row 2000001: , 
Row 2000002: , 
...
Row 2000010: , 
```

Sel sel kosong menunjukkan bahwa baris‑baris tersebut masih placeholder yang menunggu data. Anda kini dapat mengisi mereka satu per satu atau menjalankan batch pembaruan lain.

> **Catatan kasus tepi:** Jika `startIndex` melebihi jumlah baris saat ini, GridJs secara otomatis akan menambahkan baris baru di akhir. Sebaliknya, indeks negatif akan melempar `ArgumentOutOfRangeException`, jadi selalu validasi indeks yang diberikan pengguna.

## Langkah 4: Isi Baris Baru (Opsional tetapi Umum)

Seringkali Anda tidak hanya menginginkan baris kosong; Anda perlu mengisinya dengan nilai yang bermakna. Anda dapat melakukan loop pada rentang yang baru dibuat dan memanggil `SetCell` atau API serupa.

```csharp
        // Optional: fill the newly added rows with sample data
        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }
```

Anda dapat memanggil `PopulateNewRows(gridJs, startIndex, rowsToAdd);` tepat setelah batch insert jika Anda memerlukan baris siap ditampilkan segera.

## Langkah 5: Tips Kinerja untuk Grid yang Sangat Besar

Ketika Anda menangani **menambahkan banyak baris grid** dalam jutaan, ingat trik‑trik berikut:

1. **Ukuran batch penting** – Menyisipkan 10 000 baris sekaligus dapat lebih cepat daripada sepuluh batch terpisah masing‑masing 1 000 baris karena setiap batch hanya memicu satu penyegaran UI.
2. **Matikan pembaruan UI** – Beberapa versi GridJs menyediakan `grid.SuspendLayout()` / `grid.ResumeLayout()`. Bungkus batch Anda dengan pemanggilan ini jika Anda merasakan lag.
3. **Gunakan virtualisasi** – Seperti yang ditunjukkan sebelumnya, `EnableVirtualization` secara dramatis mengurangi konsumsi memori dan waktu rendering.
4. **Hindari salinan mendalam** – Kirim tipe nilai sederhana atau objek ringan ke grid; objek berat memaksa grid menyalin data, yang memperlambat kinerja.

## Contoh Lengkap yang Dapat Dijalankan

Menggabungkan semua bagian, berikut program lengkap yang dapat Anda salin‑tempel ke proyek konsol baru:

```csharp
using System;
using GridJsLibrary;   // Replace with the actual namespace of your GridJs library

namespace GridJsDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            GridJs gridJs = new GridJs
            {
                EnableVirtualization = true
            };

            SeedInitialData(gridJs);
            InsertRowsInBatch(gridJs);
        }

        static void SeedInitialData(GridJs grid)
        {
            for (int i = 0; i < 2_000_000; i++)
            {
                grid.InsertRow(i, new object[] { $"Row {i + 1}", DateTime.Now });
            }
            Console.WriteLine("Initial seed completed – 2 000 000 rows present.");
        }

        static void InsertRowsInBatch(GridJs grid)
        {
            int startIndex = 2_000_000; // zero‑based index for row 2 000 001
            int rowsToAdd = 10;

            grid.InsertRowsBatch(startIndex, rowsToAdd);
            Console.WriteLine($"Inserted {rowsToAdd} rows starting at index {startIndex + 1}.");

            // Optional: fill them with data
            PopulateNewRows(grid, startIndex, rowsToAdd);

            VerifyInsertion(grid, startIndex, rowsToAdd);
        }

        static void PopulateNewRows(GridJs grid, int startIdx, int count)
        {
            for (int i = 0; i < count; i++)
            {
                int rowIdx = startIdx + i;
                grid.SetCell(rowIdx, 0, $"New Item {i + 1}");
                grid.SetCell(rowIdx, 1, DateTime.UtcNow);
            }
            Console.WriteLine("Populated the new rows with sample data.");
        }

        static void VerifyInsertion(GridJs grid, int startIdx, int count)
        {
            Console.WriteLine("Verifying inserted rows:");
            for (int i = 0; i < count; i++)
            {
                var row = grid.GetRow(startIdx + i);
                Console.WriteLine($"Row {startIdx + i + 1}: {string.Join(", ", row)}");
            }
        }
    }
}
```

Jalankan program, dan Anda akan melihat output konsol yang mengonfirmasi bahwa sepuluh baris telah disisipkan pada lokasi yang benar dan kemudian diisi.

## Kesimpulan

Kami telah membahas **cara menyisipkan baris** di GridJs menggunakan API batch, mendemonstrasikan **cara menambahkan baris** secara efisien, dan mengeksplorasi cara **menambahkan banyak baris grid** tanpa membuat UI terhambat. Poin penting yang dapat diambil:

- Gunakan `InsertRowsBatch(startIndex, count)` untuk operasi bulk apa pun.
- Validasi indeks dan pertimbangkan virtualisasi untuk dataset yang sangat besar.
- Isi baris setelah batch jika Anda memerlukan konten segera.

Selanjutnya, Anda mungkin ingin mengeksplorasi **cara menghapus baris**, mengimplementasikan **undo/redo** untuk edit batch, atau mengintegrasikan GridJs dengan layanan back‑end yang mengalirkan data sesuai permintaan. Semua topik tersebut dibangun langsung di atas konsep yang baru saja Anda pelajari.

Jangan ragu untuk bereksperimen—ubah ukuran batch, coba sisipkan di awal grid, atau gabungkan beberapa batch dalam satu transaksi. Semakin banyak Anda bermain, semakin nyaman Anda akan menjadi dengan grid yang besar.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}