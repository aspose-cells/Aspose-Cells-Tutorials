---
"date": "2025-04-08"
"description": "Pelajari cara mengisi lembar Excel secara efisien dengan data bertingkat menggunakan Aspose.Cells untuk Java. Panduan ini mencakup pengaturan buku kerja, penerapan penanda cerdas, dan pemrosesan kumpulan data yang kompleks."
"title": "Mengisi Excel dengan Data Bertingkat Menggunakan Aspose.Cells untuk Java; Panduan Lengkap"
"url": "/id/java/data-manipulation/populate-excel-nested-data-aspose-cells-java/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}


# Mengisi Excel dengan Data Bertingkat Menggunakan Aspose.Cells untuk Java

## Bevezetés

Mengelola struktur data bersarang secara efisien di Excel dapat menjadi tantangan. **Aspose.Cells untuk Java** menyediakan solusi yang hebat untuk mengisi buku kerja Excel secara dinamis menggunakan penanda cerdas. Tutorial ini akan memandu Anda melalui proses tersebut, memastikan Anda dapat menangani kumpulan data yang rumit seperti individu dan anggota keluarga mereka dengan mudah.

Dengan mengikuti panduan ini, Anda akan mempelajari cara:
- Siapkan buku kerja dan lembar kerja baru.
- Terapkan penanda pintar untuk pengisian data yang efisien.
- Buat struktur objek bersarang di Java untuk kumpulan data yang komprehensif.
- Proses buku kerja menggunakan kelas WorkbookDesigner Aspose.Cells.

Sebelum terjun ke implementasi, mari pastikan lingkungan Anda telah disiapkan dengan benar dan dilengkapi dengan semua prasyarat yang diperlukan.

## Előfeltételek

Sebelum melanjutkan, pastikan Anda memiliki:
- **Kit Pengembangan Java (JDK)**Pastikan JDK 8 atau yang lebih baru terinstal di sistem Anda.
- **Aspose.Cells untuk Java**: Tambahkan pustaka Aspose.Cells ke proyek Anda menggunakan Maven atau Gradle seperti yang dijelaskan di bawah ini.
- **Fejlesztői környezet**: Gunakan editor teks atau IDE seperti IntelliJ IDEA, Eclipse, atau NetBeans.

### Szükséges könyvtárak és függőségek

Untuk menyertakan Aspose.Cells dalam proyek Anda:

**Pakar:**
```xml
<dependency>
  <groupId>com.aspose</groupId>
  <artifactId>aspose-cells</artifactId>
  <version>25.3</version>
</dependency>
```

**Gradasi:**
```gradle
implementation group: 'com.aspose', name: 'aspose-cells', version: '25.3'
```

### Licencszerzés

Untuk menggunakan Aspose.Cells, Anda dapat:
- **Ingyenes próbaverzió**: Unduh pustaka dan mulai dengan lisensi evaluasi sementara.
- **Vásárlás**: Dapatkan lisensi penuh untuk penggunaan produksi.

Látogatás [Aspose vásárlás](https://purchase.aspose.com/buy) untuk mempelajari lebih lanjut tentang cara memperoleh lisensi. Untuk uji coba gratis, kunjungi [Aspose kiadások](https://releases.aspose.com/cells/java/).

## Menyiapkan Aspose.Cells untuk Java

Mulailah dengan menambahkan dependensi Aspose.Cells ke proyek Anda seperti yang dijelaskan di bagian prasyarat. Setelah Anda menyertakan pustaka, inisialisasikan pustaka tersebut dalam aplikasi Java Anda.

Berikut ini adalah pengaturan dasar:
```java
import com.aspose.cells.Workbook;

public class AsposeCellsSetup {
    public static void main(String[] args) {
        // Új munkafüzet objektum inicializálása.
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java is set up and ready to use!");
    }
}
```

Cuplikan ini menunjukkan betapa mudahnya memulai bekerja dengan Aspose.Cells. Pastikan lingkungan Anda mengenali pustaka tersebut sebelum menjalankan kode lebih lanjut.

## Megvalósítási útmutató

Mari kita uraikan implementasi kita ke dalam beberapa bagian yang dapat dikelola, masing-masing berfokus pada fungsionalitas spesifik Aspose.Cells untuk Java.

### Menyiapkan Buku Kerja dengan Data Awal

#### Áttekintés

Bagian ini melibatkan inisialisasi buku kerja baru dan pengaturan tajuk awal pada lembar kerja pertama menggunakan penanda pintar.

**Langkah-langkah Implementasi:**
1. **Munkafüzet és munkalap inicializálása**:
   - Hozz létre egy példányt a következőből: `Workbook`.
   - Akses lembar kerja pertama dari buku kerja.
2. **Mengatur Header Kolom**:
   - Tentukan tajuk untuk kolom A, B, C, dan D.
3. **Terapkan Penanda Cerdas**:
   - Gunakan penanda pintar untuk menyiapkan tempat penampung data.

**Implementasi Kode:**
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class InitializeWorkbook {
    public static void main(String[] args) throws Exception {
        // Inisialisasi buku kerja baru dan dapatkan lembar kerja pertama.
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Tetapkan tajuk untuk kolom A, B, C, dan D.
        worksheet.getCells().get("A1").putValue("Person Name");
        worksheet.getCells().get("B1").putValue("Person Age");
        worksheet.getCells().get("C1").putValue("Wife Name");
        worksheet.getCells().get("D1").putValue("Wife Age");

        // Tetapkan penanda pintar untuk populasi data.
        worksheet.getCells().get("A2").putValue("&=Individual.Name");
        worksheet.getCells().get("B2").putValue("&=Individual.Age");
        worksheet.getCells().get("C2").putValue("&=Individual.Wife.Name");
        worksheet.getCells().get("D2").putValue("&=Individual.Wife.Age");

        // Jalur tempat penampung untuk menyimpan buku kerja.
        String outDir = "YOUR_OUTPUT_DIRECTORY";
        workbook.save(outDir + "/UsingNestedObjects-out.xlsx");
    }
}
```

### Membuat Daftar Objek Bertingkat untuk Sumber Data

#### Áttekintés

Langkah ini melibatkan pembuatan kelas Java untuk merepresentasikan struktur data bersarang, yang akan digunakan sebagai sumber data dalam buku kerja Excel kita.

**Langkah-langkah Implementasi:**
1. **Definisi Struktur Kelas**:
   - Teremt `Individual` és `Person` kelas.
   - Sertakan bidang dan konstruktor yang diperlukan.
2. **Buat Daftar Data**:
   - Membuat instance objek dari `Individual`, masing-masing berisi bersarang `Person`.

**Implementasi Kode:**
```java
import java.util.ArrayList;

// Tentukan struktur kelas untuk Individu dan Orang.
class Individual {
    String name;
    int age;
    Person wife;

    public Individual(String name, int age, Person wife) {
        this.name = name;
        this.age = age;
        this.wife = wife;
    }
}

class Person {
    String name;
    int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }
}

// Buat daftar objek Individual dengan detail Istri yang bersarang.
public class CreateDataList {
    public static void main(String[] args) {
        ArrayList<Individual> individuals = new ArrayList<>();
        individuals.add(new Individual("John", 23, new Person("Jill", 20)));
        individuals.add(new Individual("Jack", 25, new Person("Hilly", 21)));
        individuals.add(new Individual("James", 26, new Person("Hally", 22)));
        individuals.add(new Individual("Baptist", 27, new Person("Newly", 23)));

        System.out.println("Data list created successfully!");
    }
}
```

### Memproses Buku Kerja dengan Penanda Cerdas dan Sumber Data

#### Áttekintés

Di sini, Anda akan memanfaatkan `WorkbookDesigner` untuk memproses buku kerja Anda menggunakan penanda pintar dan sumber data.

**Langkah-langkah Implementasi:**
1. **Inisialisasi WorkbookDesigner**:
   - Hozz létre egy példányt a következőből: `WorkbookDesigner`.
2. **Tetapkan Sumber Data**:
   - Tetapkan daftar individu sebagai sumber data untuk memproses penanda pintar.
3. **Memproses Buku Kerja**:
   - Használd a `process` metode untuk mengisi buku kerja dengan data bersarang Anda.

**Implementasi Kode:**
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookDesigner;

public class ProcessWorkbook {
    public static void main(String[] args) throws Exception {
        // Siapkan WorkbookDesigner untuk memproses buku kerja.
        Workbook workbook = new Workbook("YOUR_OUTPUT_DIRECTORY/UsingNestedObjects-out.xlsx");
        WorkbookDesigner designer = new WorkbookDesigner();
        designer.setWorkbook(workbook);

        // Dengan asumsi 'individu' sudah diisi dari langkah sebelumnya
        ArrayList<Individual> individuals = new ArrayList<>();
        individuals.add(new Individual("John", 23, new Person("Jill", 20)));
        individuals.add(new Individual("Jack", 25, new Person("Hilly", 21)));
        individuals.add(new Individual("James", 26, new Person("Hally", 22)));
        individuals.add(new Individual("Baptist", 27, new Person("Newly", 23)));

        // Tetapkan daftar individu sebagai sumber data untuk penanda pintar.
        designer.setDataSource("Individual", individuals);

        // Memproses buku kerja menggunakan sumber data yang ditetapkan dengan penanda pintar.
        designer.process();

        // Simpan buku kerja yang telah diproses ke dalam sebuah berkas.
        String outDir = "YOUR_OUTPUT_DIRECTORY";
        workbook.save(outDir + "/PopulatedUsingNestedObjects.xlsx");
    }
}
```

## Következtetés

Dengan mengikuti panduan ini, Anda telah mempelajari cara mengelola dan mengisi buku kerja Excel secara efisien dengan data bertingkat menggunakan Aspose.Cells untuk Java. Pendekatan ini tidak hanya menyederhanakan penanganan kumpulan data yang kompleks tetapi juga meningkatkan fleksibilitas proses manajemen data Anda.

Untuk penjelajahan lebih jauh, pertimbangkan untuk mendalami fitur Aspose.Cells yang lebih canggih atau bereksperimen dengan berbagai jenis struktur data.

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}