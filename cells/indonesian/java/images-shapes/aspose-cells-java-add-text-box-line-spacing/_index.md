---
"date": "2025-04-08"
"description": "Pelajari cara menggunakan Aspose.Cells untuk Java untuk menambahkan kotak teks dan mengatur spasi baris di buku kerja Excel. Sempurnakan presentasi buku kerja Anda dengan bentuk teks bergaya."
"title": "Menambahkan Kotak Teks & Mengatur Spasi Baris di Excel Menggunakan Aspose.Cells untuk Java"
"url": "/id/java/images-shapes/aspose-cells-java-add-text-box-line-spacing/"
"weight": 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}


# Menambahkan Kotak Teks dan Mengatur Spasi Baris di Excel Menggunakan Aspose.Cells untuk Java

## Perkenalan

Membuat laporan Excel yang dinamis sering kali memerlukan pemformatan teks khusus, seperti menambahkan kotak teks dengan spasi baris tertentu. Dengan Aspose.Cells untuk Java, hal ini menjadi sederhana dan efisien. Tutorial ini akan memandu Anda dalam menyempurnakan presentasi buku kerja menggunakan Aspose.Cells untuk Java untuk menambahkan bentuk teks bergaya.

Di akhir panduan ini, Anda akan mempelajari cara:
- Buat buku kerja Excel baru dan akses lembar kerjanya
- Tambahkan bentuk kotak teks ke lembar kerja
- Mengatur spasi baris khusus di dalam bentuk teks
- Simpan buku kerja Anda yang diformat dalam format XLSX

Mari kita mulai dengan menyiapkan lingkungan Anda.

### Prasyarat

Sebelum memulai, pastikan Anda memiliki hal berikut:
- Java Development Kit (JDK) terinstal di komputer Anda
- IDE atau editor untuk menulis kode Java
- Sistem build Maven atau Gradle dikonfigurasi untuk mengelola dependensi

Pemahaman dasar tentang pemrograman Java dan keakraban dengan struktur file Excel akan bermanfaat.

## Menyiapkan Aspose.Cells untuk Java

Sertakan Aspose.Cells dalam manajemen ketergantungan proyek Anda menggunakan Maven atau Gradle:

**Pakar**

Tambahkan blok dependensi berikut ke `pom.xml` mengajukan:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Bahasa Inggris Gradle**

Sertakan ini di dalam `build.gradle` mengajukan:

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

Selanjutnya, dapatkan lisensi untuk Aspose.Cells dengan memilih uji coba gratis, meminta lisensi sementara, atau membeli lisensi penuh.

### Menginisialisasi Aspose.Cells

Setelah pustaka disertakan dalam proyek Anda, inisialisasikan dalam aplikasi Java Anda:

```java
import com.aspose.cells.Workbook;

public class ExcelDemo {
    public static void main(String[] args) {
        // Inisialisasi contoh Buku Kerja (mewakili file Excel)
        Workbook workbook = new Workbook();
        
        System.out.println("Aspose.Cells for Java initialized successfully.");
    }
}
```

## Panduan Implementasi

### Membuat Buku Kerja dan Mengakses Lembar Kerja

Mulailah dengan membuat buku kerja Excel baru dan mengakses lembar kerja pertamanya. Di sinilah Anda akan menambahkan kotak teks.

#### Ringkasan

Membuat buku kerja baru menyediakan ruang kosong untuk menambahkan data, bentuk, dan pemformatan sesuai kebutuhan.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

public class ExcelDemo {
    public static void main(String[] args) {
        // Buat Buku Kerja baru (file Excel)
        Workbook workbook = new Workbook();
        
        // Akses lembar kerja pertama
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        System.out.println("Workbook and first worksheet accessed.");
    }
}
```

### Tambahkan Kotak Teks ke Lembar Kerja

Selanjutnya, tambahkan bentuk kotak teks ke lembar kerja yang Anda pilih. Bentuk ini dapat berisi konten tekstual apa pun yang Anda perlukan.

#### Ringkasan

Kotak teks adalah alat serbaguna untuk menyertakan teks khusus seperti catatan atau instruksi langsung dalam lembar Excel.

```java
import com.aspose.cells.Shape;
import com.aspose.cells.MsoDrawingType;

public class ExcelDemo {
    public static void main(String[] args) {
        // Buat Buku Kerja baru (file Excel)
        Workbook workbook = new Workbook();
        
        // Akses lembar kerja pertama
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Tambahkan bentuk kotak teks ke lembar kerja
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        System.out.println("Text box added.");
    }
}
```

### Atur Teks dalam Bentuk

Setelah kotak teks Anda siap, atur kontennya dan format teks di dalamnya.

```java
import com.aspose.cells.Shape;

public class ExcelDemo {
    public static void main(String[] args) {
        // Buat Buku Kerja baru (file Excel)
        Workbook workbook = new Workbook();
        
        // Akses lembar kerja pertama
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Tambahkan bentuk kotak teks ke lembar kerja
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Mengatur konten teks di dalam bentuk
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        System.out.println("Text set in shape.");
    }
}
```

### Akses Paragraf Teks dalam Bentuk

Anda dapat mengakses paragraf individual dalam kotak teks untuk menerapkan format tertentu.

```java
import com.aspose.cells.TextParagraph;

public class ExcelDemo {
    public static void main(String[] args) {
        // Buat Buku Kerja baru (file Excel)
        Workbook workbook = new Workbook();
        
        // Akses lembar kerja pertama
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Tambahkan bentuk kotak teks ke lembar kerja
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Mengatur konten teks di dalam bentuk
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Akses paragraf kedua dalam bentuk
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);
        
        System.out.println("Accessed second paragraph in text box.");
    }
}
```

### Mengatur Jarak Baris Paragraf

Menyesuaikan spasi baris dapat meningkatkan keterbacaan. Berikut cara mengaturnya:

```java
import com.aspose.cells.LineSpaceSizeType;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Buat Buku Kerja baru (file Excel)
        Workbook workbook = new Workbook();
        
        // Akses lembar kerja pertama
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Tambahkan bentuk kotak teks ke lembar kerja
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Mengatur konten teks di dalam bentuk
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Akses paragraf kedua dalam bentuk
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Atur spasi baris menjadi 20 poin
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Konfigurasikan spasi sebelum dan sesudah paragraf
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        System.out.println("Line spacing set.");
    }
}
```

### Simpan Buku Kerja

Terakhir, simpan buku kerja Anda dengan kotak teks yang baru ditambahkan dan diformat.

```java
import com.aspose.cells.SaveFormat;

public class ExcelDemo {
    public static void main(String[] args) throws Exception {
        // Buat Buku Kerja baru (file Excel)
        Workbook workbook = new Workbook();
        
        // Akses lembar kerja pertama
        Worksheet sheet = workbook.getWorksheets().get(0);
        
        // Tambahkan bentuk kotak teks ke lembar kerja
        Shape textBox = sheet.getShapes().addShape(MsoDrawingType.TEXT_BOX, 2, 0, 2, 0, 100, 200);
        
        // Mengatur konten teks di dalam bentuk
        textBox.setText("Sign up for your free phone number.\nCall and text online for free.");
        
        // Akses paragraf kedua dalam bentuk
        TextParagraph paragraph = textBox.getTextBody().getTextParagraphs().get(1);

        // Atur spasi baris menjadi 20 poin
        paragraph.setLineSpaceSizeType(LineSpaceSizeType.POINTS);
        paragraph.setLineSpace(20); 
        
        // Konfigurasikan spasi sebelum dan sesudah paragraf
        paragraph.setSpaceAfterSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceAfter(10);
        
        paragraph.setSpaceBeforeSizeType(LineSpaceSizeType.POINTS);
        paragraph.setSpaceBefore(10);

        // Simpan buku kerja
        workbook.save("StyledTextShape.xlsx", SaveFormat.XLSX);
    }
}
```

## Kesimpulan

Anda telah berhasil mempelajari cara menambahkan kotak teks dan mengatur spasi baris dalam buku kerja Excel menggunakan Aspose.Cells untuk Java. Ini meningkatkan kemampuan Anda untuk membuat laporan yang dinamis dan menarik secara visual.

## Rekomendasi Kata Kunci
- "Aspose.Cells untuk Java"
- "Menambahkan Kotak Teks di Excel"
- "Mengatur Spasi Baris di Excel"
- "Buku Kerja Excel dengan Teks Bergaya"
- "Java dan Aspose.Cells"


{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}