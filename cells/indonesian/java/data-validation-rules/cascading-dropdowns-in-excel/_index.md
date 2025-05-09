---
"description": "Pelajari cara membuat dropdown bertingkat di Excel menggunakan Aspose.Cells untuk Java. Panduan langkah demi langkah ini menyediakan kode sumber dan kiat ahli untuk manipulasi spreadsheet Excel yang efisien."
"linktitle": "Dropdown Berjenjang di Excel"
"second_title": "API Pemrosesan Java Excel Aspose.Cells"
"title": "Dropdown Berjenjang di Excel"
"url": "/id/java/data-validation-rules/cascading-dropdowns-in-excel/"
"weight": 13
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Dropdown Berjenjang di Excel


## Pengenalan Dropdown Berjenjang di Excel

Dalam dunia manipulasi spreadsheet, Aspose.Cells for Java merupakan perangkat canggih yang memberdayakan pengembang untuk bekerja dengan file Excel secara efisien. Salah satu fitur menarik yang ditawarkannya adalah kemampuan untuk membuat dropdown berjenjang di Excel, yang memungkinkan pengguna untuk memilih opsi secara dinamis berdasarkan pilihan sebelumnya. Dalam panduan langkah demi langkah ini, kita akan menyelami proses penerapan dropdown berjenjang menggunakan Aspose.Cells for Java. Jadi, mari kita mulai!

## Előfeltételek

Sebelum kita memulai perjalanan ini, pastikan Anda memiliki prasyarat berikut:

- Aspose.Cells untuk Java: Unduh dan instal dari [itt](https://releases.aspose.com/cells/java/).
- Lingkungan Pengembangan Java: Anda harus menyiapkan lingkungan pengembangan Java di komputer Anda.
- Pemahaman Dasar tentang Excel: Keakraban dengan Excel dan konsep dasarnya akan sangat membantu.

## Menyiapkan Panggung

Tujuan kami adalah membuat lembar Excel dengan dropdown bertingkat. Bayangkan skenario di mana Anda memiliki daftar negara, dan saat Anda memilih suatu negara, daftar kota di negara tersebut akan tersedia untuk dipilih. Mari kita uraikan langkah-langkah untuk mencapainya.

## Langkah 1: Membuat Buku Kerja Excel

Pertama, mari kita buat buku kerja Excel menggunakan Aspose.Cells untuk Java. Kita akan menambahkan dua lembar: satu untuk daftar negara dan satu lagi untuk daftar kota.

```java
// Kode Java untuk membuat buku kerja Excel
Workbook workbook = new Workbook();
Worksheet countrySheet = workbook.getWorksheets().get(0);
countrySheet.setName("Countries");
Worksheet citySheet = workbook.getWorksheets().add("Cities");
```

## Langkah 2: Mengisi Data

Sekarang, kita perlu mengisi lembar kerja kita dengan data. Di lembar "Negara", kita akan mencantumkan negara-negara, dan di lembar "Kota", kita akan membiarkannya kosong terlebih dahulu, karena kita akan mengisinya secara dinamis nanti.

```java
// Kode Java untuk mengisi lembar "Negara"
countrySheet.getCells().get("A1").putValue("Country");
countrySheet.getCells().get("A2").putValue("USA");
countrySheet.getCells().get("A3").putValue("Canada");
countrySheet.getCells().get("A4").putValue("UK");
// Tambahkan lebih banyak negara sesuai kebutuhan
```

## Langkah 3: Membuat Dropdown

Selanjutnya, kita akan membuat daftar dropdown untuk kolom negara dan kota. Dropdown ini akan ditautkan sedemikian rupa sehingga saat negara dipilih, dropdown kota akan diperbarui sesuai dengan pilihan.

```java
// Kode Java untuk membuat daftar dropdown
DataValidationCollection validations = countrySheet.getDataValidations();
DataValidation validation = validations.get(validations.add(1, 1, countrySheet.getCells().getMaxDataRow(), 1));
validation.setType(DataValidationType.LIST);
validation.setFormula1("Countries!$A$2:$A$4"); // Referensi ke daftar negara
```

## Langkah 4: Menerapkan Dropdown Berjenjang

Sekarang tibalah bagian yang menarik: menerapkan dropdown berjenjang. Kita akan menggunakan Aspose.Cells untuk Java untuk memperbarui dropdown kota secara dinamis berdasarkan negara yang dipilih.

```java
// Kode Java untuk mengimplementasikan dropdown berjenjang
countrySheet.getCells().setCellObserver(new ICellObserver() {
    @Override
    public void cellChanged(Cell cell) {
        if (cell.getName().equals("B2")) {
            // Hapus dropdown kota sebelumnya
            citySheet.getCells().get("B2").setValue("");
            
            // Tentukan negara yang dipilih
            String selectedCountry = cell.getStringValue();
            
            // Berdasarkan negara yang dipilih, isi dropdown kota
            switch (selectedCountry) {
                case "USA":
                    validation.setFormula1("Cities!$A$2:$A$4"); // Isi dengan kota-kota di AS
                    break;
                case "Canada":
                    validation.setFormula1("Cities!$B$2:$B$4"); // Isi dengan kota-kota Kanada
                    break;
                case "UK":
                    validation.setFormula1("Cities!$C$2:$C$4"); // Isi dengan kota-kota di Inggris
                    break;
                // Tambahkan lebih banyak kasus untuk negara lain
            }
        }
    }
});
```

## Következtetés

Dalam panduan lengkap ini, kami menjajaki cara membuat dropdown bertingkat di Excel menggunakan Aspose.Cells untuk Java. Kami mulai dengan menyiapkan prasyarat, membuat buku kerja Excel, mengisi data, lalu mendalami seluk-beluk pembuatan dropdown dan penerapan perilaku bertingkat yang dinamis. Sebagai pengembang, kini Anda memiliki pengetahuan dan alat untuk menyempurnakan file Excel Anda dengan dropdown interaktif, yang memberikan pengalaman pengguna yang lancar.

## GYIK

### Bagaimana cara menambahkan lebih banyak negara dan kota ke menu dropdown?

Untuk menambahkan lebih banyak negara dan kota, Anda perlu memperbarui lembar kerja masing-masing di buku kerja Excel Anda. Cukup perluas daftar di lembar "Negara" dan "Kota", dan menu tarik-turun akan secara otomatis menyertakan entri baru.

### Dapatkah saya menggunakan teknik ini bersama-sama dengan fitur Excel lainnya?

Tentu saja! Anda dapat menggabungkan dropdown bertingkat dengan berbagai fitur Excel seperti pemformatan bersyarat, rumus, dan diagram untuk membuat lembar kerja yang canggih dan interaktif yang disesuaikan dengan kebutuhan spesifik Anda.

### Apakah Aspose.Cells untuk Java cocok untuk proyek skala kecil dan besar?

Ya, Aspose.Cells untuk Java bersifat serbaguna dan dapat digunakan dalam berbagai proyek dengan skala apa pun. Baik Anda mengerjakan utilitas kecil atau aplikasi perusahaan yang kompleks, Aspose.Cells untuk Java dapat menyederhanakan tugas-tugas terkait Excel Anda.

### Apakah saya memerlukan keterampilan pemrograman tingkat lanjut untuk mengimplementasikan dropdown berjenjang dengan Aspose.Cells untuk Java?

Meskipun pemahaman dasar tentang Java sangat membantu, Aspose.Cells untuk Java menyediakan dokumentasi dan contoh yang lengkap untuk memandu Anda melalui prosesnya. Dengan sedikit dedikasi dan latihan, Anda dapat menguasai fitur ini.

### Di mana saya dapat menemukan lebih banyak sumber daya dan dokumentasi untuk Aspose.Cells untuk Java?

Anda dapat mengakses dokumentasi dan sumber daya yang komprehensif untuk Aspose.Cells untuk Java di [itt](https://reference.aspose.com/cells/java/).

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}