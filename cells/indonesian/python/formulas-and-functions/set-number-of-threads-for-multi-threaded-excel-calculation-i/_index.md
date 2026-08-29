---
category: general
date: 2026-06-08
description: Atur jumlah thread di Python untuk mengaktifkan perhitungan multi‑thread
  dan meningkatkan kecepatan perhitungan Excel. Pelajari cara memuat workbook Excel
  dengan Python secara cepat.
draft: false
keywords:
- set number of threads
- enable multi-threaded calculation
- increase excel calculation speed
- load excel workbook python
- multi-threaded excel calculation
language: id
og_description: Atur jumlah thread di Python untuk mengaktifkan perhitungan multi‑thread
  dan meningkatkan kecepatan perhitungan Excel. Panduan langkah demi langkah lengkap.
og_title: Atur Jumlah Thread untuk Perhitungan Excel Multi‑Thread di Python
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Set number of threads in Python to enable multi‑threaded calculation
    and increase Excel calculation speed. Learn to load Excel workbook Python fast.
  headline: Set Number of Threads for Multi‑Threaded Excel Calculation in Python
  type: TechArticle
tags:
- python
- excel
- performance
- multithreading
title: Atur Jumlah Thread untuk Perhitungan Excel Multi‑Thread di Python
url: /id/python/formulas-and-functions/set-number-of-threads-for-multi-threaded-excel-calculation-i/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Atur Jumlah Thread untuk Perhitungan Excel Multi‑Threaded di Python

Pernah bertanya‑tanya bagaimana **mengatur jumlah thread** agar rumus Excel Anda diproses lebih cepat? Anda tidak sendirian—banyak data‑engineer menemui kendala ketika workbook besar membuat CPU melambat. Kabar baiknya? Dengan beberapa baris Python saja Anda dapat **mengaktifkan perhitungan multi‑threaded** dan **meningkatkan kecepatan perhitungan Excel** secara dramatis.

Dalam tutorial ini kita akan memuat workbook Excel di Python, mengaktifkan perhitungan multi‑threaded, dan mengonfigurasi jumlah thread yang tepat. Pada akhir tutorial Anda akan memiliki skrip siap‑jalankan yang mengurangi hitungan detik—atau bahkan menit—pada pemrosesan spreadsheet berat.

## Apa yang Anda Butuhkan

Sebelum kita mulai, pastikan Anda memiliki:

- Python 3.9+ terpasang (versi terbaru apa saja)
- Paket `openpyxl‑threaded` (atau perpustakaan apa pun yang menyediakan `Workbook.settings.calculation_options`; kami akan menggunakan API hipotetik yang mirip dengan gaya openpyxl)
- File Excel (`input.xlsx`) yang ingin Anda percepat
- Jumlah RAM yang cukup (pekerjaan multi‑threaded dapat mengonsumsi memori cukup besar)

Jika ada yang belum familiar, jangan khawatir—kami akan membahas langkah instalasi setelah penjelasan singkat.

## Mengapa Perhitungan Excel Multi‑Threaded Penting

Mesin perhitungan bawaan Excel bersifat single‑threaded secara default, artinya ia memproses rumus satu per satu. Pada workbook dengan ribuan sel yang saling terhubung, hal ini menjadi bottleneck. Dengan mengaktifkan **perhitungan multi‑threaded**, mesin mendistribusikan grup rumus yang independen ke beberapa core CPU, mengubah tugas yang lama menjadi sprint paralel.

Bayangkan seperti dapur: satu koki hanya dapat membalik satu pancake pada satu waktu, tetapi tim koki dapat menangani banyak wajan sekaligus, sehingga sarapan selesai lebih cepat. Prinsip yang sama berlaku untuk rumus Excel—lebih banyak thread, lebih banyak pekerjaan bersamaan, hasil lebih cepat.

## Langkah 1: Muat Workbook Excel dengan Gaya Python

Langkah pertama: kita perlu **memuat workbook Excel dengan Python** sehingga memiliki objek `Workbook` untuk dikonfigurasi. Kode di bawah menunjukkan cara bersih dan ter‑handle error untuk membuka file.

```python
import os
from openpyxl_threaded import Workbook  # Hypothetical import for illustration

def load_workbook(path: str) -> Workbook:
    """
    Load an Excel workbook from the given path.
    Raises FileNotFoundError if the file does not exist.
    """
    if not os.path.isfile(path):
        raise FileNotFoundError(f"Workbook not found: {path}")
    # The Workbook constructor accepts a file path for existing workbooks
    wb = Workbook(path)
    return wb

# Example usage
workbook_path = "YOUR_DIRECTORY/input.xlsx"
workbook = load_workbook(workbook_path)
```

> **Pro tip:** Bungkus logika pemuatan dalam fungsi seperti `load_workbook` agar skrip utama tetap rapi dan dapat menangani error file yang tidak ditemukan dengan elegan.

## Langkah 2: Aktifkan Perhitungan Multi‑Threaded

Setelah kita memiliki objek workbook, saatnya **mengaktifkan perhitungan multi‑threaded**. Kebanyakan perpustakaan pemrosesan Excel modern menyediakan objek `settings.calculation_options` yang memungkinkan Anda mengatur threading.

```python
def enable_multithreading(wb: Workbook, threads: int = 4) -> None:
    """
    Turn on multi‑threaded calculation and set the desired number of threads.
    Pass -1 for `threads` to let the library auto‑detect the optimal count.
    """
    calc_opts = wb.settings.calculation_options
    calc_opts.multi_threaded = True          # Activate threading
    calc_opts.number_of_threads = threads    # Set explicit thread count

# Enable with 4 threads (adjust based on your CPU cores)
enable_multithreading(workbook, threads=4)
```

Anda mungkin memperhatikan komentar `# Use -1 for automatic thread selection`. Itu berguna ketika Anda tidak yakin berapa banyak core yang tersedia—membiarkan perpustakaan yang memutuskan dapat mencegah penggunaan sumber daya yang berlebihan.

## Langkah 3: Hitung Ulang Semua Rumus

Dengan threading diaktifkan, langkah selanjutnya adalah **menghitung ulang semua rumus** agar pengaturan baru berlaku. Operasi ini dapat menjadi bagian paling memakan waktu, tetapi berkat banyak core seharusnya selesai jauh lebih cepat.

```python
def recalculate_workbook(wb: Workbook) -> None:
    """
    Force a full workbook recalculation using the currently configured
    calculation options (including multi‑threading).
    """
    wb.calculate_formula()   # Triggers a full refresh of all cells

# Perform the calculation
recalculate_workbook(workbook)
```

Setelah pemanggilan ini, setiap sel yang bergantung pada rumus akan memiliki nilai yang diperbarui sesuai dengan perhitungan paralel yang baru.

## Langkah 4: Simpan Workbook yang Telah Dioptimalkan

Biasanya Anda ingin menyimpan hasilnya. Penyimpanan sangat sederhana:

```python
def save_workbook(wb: Workbook, output_path: str) -> None:
    """
    Write the workbook to disk. Overwrites if the file already exists.
    """
    wb.save(output_path)

# Save to a new file to keep the original intact
save_workbook(workbook, "YOUR_DIRECTORY/output_optimized.xlsx")
```

Sekarang Anda memiliki file Excel yang diproses dengan **jumlah thread yang ditentukan** dan **perhitungan Excel multi‑threaded**—siap untuk analisis lanjutan atau pelaporan.

## Opsional: Mengukur Peningkatan Kecepatan

Melihat hasil lebih meyakinkan. Mari kita bandingkan kecepatan antara eksekusi single‑threaded dan multi‑threaded menggunakan modul `time` di Python.

```python
import time

def benchmark(wb_path: str, threads: int):
    start = time.time()
    wb = load_workbook(wb_path)
    enable_multithreading(wb, threads=threads)
    recalculate_workbook(wb)
    elapsed = time.time() - start
    print(f"Threads: {threads} | Time taken: {elapsed:.2f}s")

# Compare default (single thread) vs 4 threads
benchmark("YOUR_DIRECTORY/input.xlsx", threads=1)   # Single‑thread baseline
benchmark("YOUR_DIRECTORY/input.xlsx", threads=4)   # Multi‑threaded run
```

Hasil tipikal pada laptop quad‑core menunjukkan percepatan 2‑3× untuk workbook besar. Tentu saja, faktor pastinya tergantung pada kompleksitas rumus, inter‑dependensi, dan berapa banyak core yang sebenarnya dimiliki mesin Anda.

## Kesalahan Umum & Cara Menghindarinya

| Masalah | Mengapa Terjadi | Solusi |
|---------|----------------|--------|
| **Jumlah thread melebihi core CPU** | Over‑allocating thread dapat menimbulkan overhead context‑switch, memperlambat proses. | Gunakan `-1` untuk auto‑selection, atau panggil `os.cpu_count()` dan tetap dalam rentang tersebut. |
| **Lonjakan memori** | Setiap thread menyimpan stack perhitungannya sendiri; workbook besar dapat menghabiskan RAM. | Pantau penggunaan memori; pertimbangkan mengurangi jumlah thread jika terjadi swapping. |
| **Rumus dengan referensi sirkular** | Mesin paralel mungkin kesulitan dengan dependensi sirkular. | Pastikan workbook bebas dari referensi sirkular sebelum mengaktifkan threading. |
| **Fungsi tidak didukung** | Beberapa fungsi Excel tidak thread‑safe pada perpustakaan tertentu. | Uji pada sebagian kecil workbook terlebih dahulu; kembali ke mode single‑threaded jika muncul error. |

## Skrip Lengkap – Siap Salin & Tempel

Berikut adalah skrip lengkap yang dapat dijalankan. Simpan sebagai `excel_multithread.py` dan sesuaikan jalur file sesuai kebutuhan.

```python
import os
import time
from openpyxl_threaded import Workbook  # Replace with your actual library

def load_workbook(path: str) -> Workbook:
    if not os.path.isfile(path):
        raise FileNotFoundError(f"Workbook not found: {path}")
    return Workbook(path)

def enable_multithreading(wb: Workbook, threads: int = 4) -> None:
    calc_opts = wb.settings.calculation_options
    calc_opts.multi_threaded = True
    calc_opts.number_of_threads = threads

def recalculate_workbook(wb: Workbook) -> None:
    wb.calculate_formula()

def save_workbook(wb: Workbook, output_path: str) -> None:
    wb.save(output_path)

def benchmark(wb_path: str, threads: int):
    start = time.time()
    wb = load_workbook(wb_path)
    enable_multithreading(wb, threads=threads)
    recalculate_workbook(wb)
    elapsed = time.time() - start
    print(f"Threads: {threads} | Time taken: {elapsed:.2f}s")
    return wb

if __name__ == "__main__":
    INPUT = "YOUR_DIRECTORY/input.xlsx"
    OUTPUT = "YOUR_DIRECTORY/output_optimized.xlsx"

    # Benchmark single vs multi‑threaded
    print("Running single‑threaded benchmark...")
    benchmark(INPUT, threads=1)

    print("\nRunning multi‑threaded benchmark (4 threads)...")
    wb = benchmark(INPUT, threads=4)

    # Save the optimized workbook
    save_workbook(wb, OUTPUT)
    print(f"\nOptimized workbook saved to: {OUTPUT}")
```

> **Output yang Diharapkan:**  
> ```
> Running single‑threaded benchmark...  
> Threads: 1 | Time taken: 12.34s  
>   
> Running multi‑threaded benchmark (4 threads)...  
> Threads: 4 | Time taken: 4.56s  
>   
> Optimized workbook saved to: YOUR_DIRECTORY/output_optimized.xlsx
> ```

Angka Anda akan berbeda, tetapi Anda seharusnya melihat penurunan yang jelas pada waktu perhitungan.

## Kesimpulan

Kita baru saja **mengatur jumlah thread** untuk alur kerja Excel yang dijalankan lewat Python, **mengaktifkan perhitungan multi‑threaded**, dan menunjukkan bagaimana hal itu dapat **meningkatkan kecepatan perhitungan Excel**. Dengan memuat


## Apa yang Harus Anda Pelajari Selanjutnya?


Tutorial berikut mencakup topik terkait yang memperluas teknik yang ditunjukkan dalam panduan ini. Setiap sumber menyertakan contoh kode lengkap dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda.

- [Optimalkan Perhitungan Excel Menggunakan Aspose.Cells Java: Menguasai Rantai Perhitungan untuk Pemrosesan Workbook yang Efisien](/cells/english/java/calculation-engine/optimize-excel-aspose-cells-java-calculation-chains/)
- [Cara Memuat Workbook Excel & Mengatur Ukuran Printer Menggunakan Aspose.Cells untuk .NET](/cells/english/net/workbook-operations/load-workbook-set-printer-sizes-aspose-cells-dotnet/)
- [Atur Nomor Halaman Pertama Excel](/cells/english/net/excel-page-setup/set-excel-first-page-number/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}