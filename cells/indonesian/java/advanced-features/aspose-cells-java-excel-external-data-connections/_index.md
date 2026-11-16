---
date: '2026-11-16'
description: Pelajari cara menambahkan dependensi Maven Aspose.Cells, mengambil, menampilkan,
  dan mengelola koneksi data Excel, serta menarik data SQL ke dalam Excel menggunakan
  Java.
keywords:
- create excel data connections
- pull sql data excel
- manage excel external connections
- Aspose.Cells
- Java Excel integration
lastmod: '2026-11-16'
og_description: Buat koneksi data Excel menggunakan Aspose.Cells untuk Java. Pelajari
  cara menambahkan dependensi Maven, mengambil koneksi, menarik data SQL ke dalam
  Excel, dan mengelola koneksi eksternal secara efisien.
og_image_alt: Guide showing how to create excel data connections using Aspose.Cells
  Java API
og_title: Buat koneksi data Excel dengan Aspose.Cells untuk Java
schemas:
- author: Aspose
  dateModified: '2026-11-16'
  description: Learn how to add Aspose.Cells Maven dependency, retrieve, list, and
    manage Excel data connections, and pull SQL data into Excel using Java.
  headline: Create excel data connections with Aspose.Cells for Java
  type: TechArticle
- description: Learn how to add Aspose.Cells Maven dependency, retrieve, list, and
    manage Excel data connections, and pull SQL data into Excel using Java.
  name: Create excel data connections with Aspose.Cells for Java
  steps:
  - name: load your workbook
    text: The `Workbook` class represents an entire Excel file in memory. Loading
      it is the first step before any connection work.
  - name: retrieve connections
    text: '`workbook.getDataConnections()` returns an `ExternalConnectionCollection`
      containing every defined connection.'
  - name: loop through connections
    text: '`DBConnection` is a subclass of `ExternalConnection` that represents a
      database connection and provides properties such as command text, connection
      string, and parameters. Iterate over the collection, cast each entry to `DBConnection`,
      and read its properties.'
  - name: access parameters
    text: Each `DBConnection` exposes a `getParameters()` method that returns a list
      of name/value pairs.
  type: HowTo
- questions:
  - answer: It is the Maven artifact (`com.aspose:aspose-cells`) that provides the
      Java APIs for reading, writing, and managing Excel files, including external
      data connections.
    question: What is Aspose.Cells Maven dependency?
  - answer: Call `workbook.getDataConnections()` and iterate over the returned `ExternalConnectionCollection`.
    question: How can I list excel data connections in my workbook?
  - answer: Cast each connection to `DBConnection` and use methods like `getCommand()`,
      `getConnectionDescription()`, and `getParameters()`.
    question: How do I extract database connection details from a DBConnection object?
  - answer: Yes, use a standard `for` loop over the collection, cast each to the appropriate
      type, and apply changes as needed.
    question: Can I loop through excel connections to modify them?
  - answer: A valid Aspose.Cells license removes evaluation limitations and enables
      full functionality.
    question: Do I need a license to use these features in production?
  type: FAQPage
tags:
- create excel data connections
- Aspose.Cells
- Java Excel data
- external data connections
title: Buat koneksi data Excel dengan Aspose.Cells untuk Java
url: /id/java/advanced-features/aspose-cells-java-excel-external-data-connections/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Buat koneksi data excel dengan Aspose.Cells untuk Java

Dalam aplikasi modern yang berfokus pada data, **create excel data connections** secara programatis sehingga Anda dapat menarik data langsung dari basis data ke dalam workbook. Menambahkan dependensi Maven Aspose.Cells memberi Anda satu API yang terdokumentasi dengan baik yang menangani segala hal mulai dari daftar koneksi yang ada hingga mengekstrak string koneksi lengkap—semua tanpa memerlukan Microsoft Office di server. Tutorial ini memandu Anda melalui penyiapan, pengambilan, dan penggunaan praktis, sehingga Anda dapat mengintegrasikan Excel dengan backend SQL Anda dengan percaya diri.

## Jawaban Cepat
- **Apa cara utama menambahkan Aspose.Cells ke proyek Java?** Include the `com.aspose:aspose-cells` Maven artifact in your `pom.xml`.  
- **Bisakah saya menampilkan semua koneksi data Excel?** Yes—call `workbook.getDataConnections()` and iterate over the returned collection.  
- **Bagaimana cara mengekstrak detail koneksi basis data?** Cast each `ExternalConnection` to `DBConnection` and read its properties such as command text and connection string.  
- **Apakah memungkinkan untuk melakukan loop melalui koneksi Excel?** Absolutely—use a standard `for` loop over the `ExternalConnectionCollection`.  
- **Apakah saya memerlukan lisensi untuk penggunaan produksi?** A valid Aspose.Cells license removes evaluation limitations and unlocks full functionality.

## Apa yang akan Anda pelajari
- Cara **create excel data connections** dan mengambilnya dari workbook yang ada menggunakan Aspose.Cells untuk Java.  
- Cara mengekstrak informasi terperinci tentang setiap koneksi, termasuk detail basis data dan parameter.  
- Skenario dunia nyata untuk menarik data SQL ke Excel dan mengotomatisasi pembuatan laporan.  
- Tips mengoptimalkan kinerja saat menangani workbook besar dalam Java.

## Mengapa menambahkan dependensi Maven Aspose.Cells? – manfaat & kasus penggunaan
**Anda menambahkan artefak Maven untuk mendapatkan kontrol programatik atas file Excel tanpa harus menginstal Office.** Aspose.Cells mendukung **lebih dari 50 format input dan output** dan dapat memproses workbook dengan **hingga 10.000 baris** sambil menjaga penggunaan memori di bawah 150 MB dengan memuat hanya bagian yang diperlukan. Ini menjadikannya ideal untuk alur kerja **pull sql data excel**, pelaporan otomatis, dan manajemen koneksi terpusat di seluruh lingkungan perusahaan.

## Prasyarat
- **Aspose.Cells for Java** (versi 25.3 atau lebih baru).  
- Lingkungan build Maven atau Gradle.  
- Java 8 atau lebih tinggi terinstal.  

### Perpustakaan yang Diperlukan
- **Aspose.Cells for Java** – perpustakaan inti yang memungkinkan manipulasi file Excel dan penanganan koneksi data.

### Penyiapan Lingkungan
- Pastikan IDE atau alat build Anda mendukung Maven atau Gradle.  
- Verifikasi Java 8 atau yang lebih baru ada di `PATH` Anda.

## Cara menambahkan dependensi Maven Aspose Cells
Muat perpustakaan dengan menambahkan satu baris dependensi ke `pom.xml` Anda. Ini memberi Anda akses langsung ke rangkaian lengkap API Excel.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Jika Anda lebih suka Gradle, deklarasi setara adalah:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Langkah-langkah memperoleh lisensi
- **Free trial** – Jelajahi perpustakaan tanpa biaya.  
- **Temporary license** – Perpanjang periode evaluasi Anda.  
- **Purchase** – Buka semua fitur untuk beban kerja produksi.

## Inisialisasi dasar dan penyiapan
Setelah dependensi teratasi, Anda dapat mulai menggunakan Aspose.Cells dalam kode Java Anda:

```java
import com.aspose.cells.Workbook;

// Load an Excel workbook
Workbook workbook = new Workbook("path_to_your_excel_file.xlsx");
```

## Panduan Implementasi

### Fitur 1: mengambil koneksi data eksternal
**Apa itu?** Fitur ini memungkinkan Anda **list excel data connections** sehingga Anda tahu persis sumber eksternal mana yang digunakan workbook Anda.

#### Langkah 1: muat workbook Anda
Kelas `Workbook` mewakili seluruh file Excel dalam memori. Memuatnya adalah langkah pertama sebelum melakukan pekerjaan koneksi apa pun.

```java
String sourceDir = "YOUR_DATA_DIRECTORY";
Workbook workbook = new Workbook(sourceDir + "/sampleRetrievingSQLConnectionData.xlsx");
```

#### Langkah 2: ambil koneksi
`workbook.getDataConnections()` mengembalikan `ExternalConnectionCollection` yang berisi semua koneksi yang didefinisikan.

```java
import com.aspose.cells.ExternalConnectionCollection;

ExternalConnectionCollection connections = workbook.getDataConnections();
int connectionCount = connections.getCount();
```

### Fitur 2: mengekstrak detail koneksi basis data
**Mengapa menggunakannya?** Untuk **extract database connection details** seperti perintah, deskripsi, dan string koneksi untuk audit atau modifikasi dinamis.

#### Langkah 1: loop melalui koneksi
`DBConnection` adalah subclass dari `ExternalConnection` yang mewakili koneksi basis data dan menyediakan properti seperti teks perintah, string koneksi, dan parameter.  
Iterasi koleksi, cast setiap entri ke `DBConnection`, dan baca propertinya.

```java
import com.aspose.cells.DBConnection;

for (int i = 0; i < connectionCount; i++) {
    Object connection = connections.get(i);
    if (connection instanceof DBConnection) {
        DBConnection dbConn = (DBConnection) connection;
        
        // Display details
        System.out.println("Command: " + dbConn.getCommand());
        System.out.println("Description: " + dbConn.getConnectionDescription());
        // Add more fields as needed...
    }
}
```

### Fitur 3: mengekstrak detail parameter koneksi
**Bagaimana ini membantu?** Ini memungkinkan Anda **integrate excel with database** dengan mengakses setiap parameter yang diperlukan untuk koneksi, seperti token otentikasi atau argumen kueri.

#### Langkah 1: akses parameter
Setiap `DBConnection` menyediakan metode `getParameters()` yang mengembalikan daftar pasangan nama/nilai.

```java
import com.aspose.cells.ConnectionParameterCollection;
import com.aspose.cells.ConnectionParameter;

for (int i = 0; i < connectionCount; i++) {
    Object connection = connections.get(i);
    if (connection instanceof DBConnection) {
        DBConnection dbConn = (DBConnection) connection;
        ConnectionParameterCollection parameters = dbConn.getParameters();
        
        for (int j = 0; j < parameters.getCount(); j++) {
            ConnectionParameter param = parameters.get(j);
            
            // Display parameter details
            System.out.println("Name: " + param.getName());
            System.out.println("Value: " + param.getValue());
            // Continue displaying other properties...
        }
    }
}
```

## Aplikasi Praktis
1. **Data integration** – Secara otomatis menyinkronkan data Excel dengan basis data eksternal.  
2. **Automated reporting** – Tarik data langsung untuk laporan terkini tanpa penyegaran manual.  
3. **System monitoring** – Lacak perubahan pada koneksi basis data untuk pemeriksaan kesehatan.  
4. **Data validation** – Validasi data eksternal sebelum mengimpornya ke dalam workbook.

## Pertimbangan Kinerja
- Muat workbook besar secara hemat untuk menjaga penggunaan memori tetap rendah.  
- Gunakan loop yang efisien (seperti yang ditunjukkan) dan hindari pembuatan objek yang tidak perlu.  
- Manfaatkan penyesuaian garbage‑collection Java untuk layanan yang berjalan lama.

## Masalah Umum & Pemecahan Masalah
- **Null connections** – Pastikan workbook memang berisi koneksi eksternal; jika tidak `getDataConnections()` mengembalikan koleksi kosong.  
- **License not set** – Tanpa lisensi yang valid, Anda mungkin melihat peringatan evaluasi atau fungsionalitas terbatas.  
- **Unsupported data source** – Beberapa koneksi ODBC lama mungkin memerlukan instalasi driver tambahan pada mesin host.

## Pertanyaan yang Sering Diajukan

**Q: Apa itu dependensi Maven Aspose.Cells?**  
A: Itu adalah artefak Maven (`com.aspose:aspose-cells`) yang menyediakan API Java untuk membaca, menulis, dan mengelola file Excel, termasuk koneksi data eksternal.

**Q: Bagaimana saya dapat menampilkan koneksi data excel dalam workbook saya?**  
A: Panggil `workbook.getDataConnections()` dan iterasi `ExternalConnectionCollection` yang dikembalikan.

**Q: Bagaimana cara mengekstrak detail koneksi basis data dari objek DBConnection?**  
A: Cast setiap koneksi ke `DBConnection` dan gunakan metode seperti `getCommand()`, `getConnectionDescription()`, dan `getParameters()`.

**Q: Bisakah saya melakukan loop melalui koneksi excel untuk memodifikasinya?**  
A: Ya, gunakan loop `for` standar atas koleksi, cast setiap ke tipe yang sesuai, dan terapkan perubahan sesuai kebutuhan.

**Q: Apakah saya memerlukan lisensi untuk menggunakan fitur ini dalam produksi?**  
A: Lisensi Aspose.Cells yang valid menghapus batasan evaluasi dan mengaktifkan fungsionalitas penuh.

## Sumber Daya
- [Dokumentasi](https://reference.aspose.com/cells/java/)
- [Unduh Versi Terbaru](https://releases.aspose.com/cells/java/)
- [Beli Lisensi](https://purchase.aspose.com/buy)
- [Akses Uji Coba Gratis](https://releases.aspose.com/cells/java/)
- [Informasi Lisensi Sementara](https://purchase.aspose.com/temporary-license/)
- [Forum Dukungan](https://forum.aspose.com/c/cells/9)

---

**Terakhir Diperbarui:** 2026-11-16  
**Diuji Dengan:** Aspose.Cells 25.3 (Java)  
**Penulis:** Aspose

## Tutorial Terkait

- [Ekstrak URL dari Excel dengan Aspose.Cells untuk Java – Muat Koneksi Data](/cells/java/advanced-features/aspose-cells-java-excel-data-connections/)
- [Aspose.Cells Java: Menguasai Koneksi Workbook Excel untuk Integrasi Data dan Analisis](/cells/java/import-export/aspose-cells-java-excel-connections/)
- [Modifikasi Koneksi Data Excel dengan Aspose.Cells untuk Java – Panduan Langkah demi Langkah](/cells/java/advanced-features/master-excel-data-connections-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}