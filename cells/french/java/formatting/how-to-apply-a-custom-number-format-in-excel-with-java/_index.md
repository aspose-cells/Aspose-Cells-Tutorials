---
category: general
date: 2026-11-22
description: Apprenez à utiliser un format de nombre personnalisé pour formater une
  colonne en devise dans Excel à l'aide de Java. Définissez rapidement le format de
  nombre d'Excel avec un style simple.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- custom number format
- format column as currency
- set excel number format
- set currency format
- style first column
language: fr
lastmod: 2026-11-22
og_description: Appliquer un format numérique personnalisé dans Excel avec Java. Ce
  tutoriel montre comment définir le format numérique d’Excel et mettre en forme la
  première colonne en tant que devise.
og_image_alt: Java code snippet that applies a custom number format to an Excel column
og_title: Appliquer un format de nombre personnalisé dans Excel avec Java – guide
  étape par étape
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to use a custom number format to format a column as currency
    in Excel using Java. Set Excel number format quickly with a simple style.
  headline: How to apply a custom number format in Excel with Java
  type: TechArticle
tags:
- Java
- Excel
- Apache POI
- Spreadsheet Automation
title: Comment appliquer un format de nombre personnalisé dans Excel avec Java
url: /fr/java/formatting/how-to-apply-a-custom-number-format-in-excel-with-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment appliquer un format de nombre personnalisé dans Excel avec Java

Si vous devez **custom number format** une colonne dans une feuille de calcul Excel, ce guide vous montre exactement comment le faire en utilisant Java. Que vous génériez des rapports financiers ou exportiez des données comptables, formater la première colonne en devise rend la sortie immédiatement lisible.

Dans l'exemple ci‑dessous, nous allons **format column as currency**, appliquer le style à la première colonne, puis importer un `DataTable` dans la feuille de calcul. La même approche fonctionne pour tout format numérique que vous souhaitez afficher.

## Ce que vous apprendrez

* Comment créer un **custom number format** avec l'objet `Style` d'Apache POI.  
* Comment **set Excel number format** pour une colonne spécifique, y compris le cas **set currency format**.  
* Comment **style first column** lors de l'importation d'un `DataTable`.  
* Comment enregistrer le classeur et vérifier que le formatage apparaît correctement.

### Prérequis

* Java 17 ou supérieur.  
* Apache POI 5.x (la bibliothèque qui fournit `Workbook`, `Worksheet` et `Style`).  
* Une implémentation de `DataTable` qui peut être itérée comme celle de l'exemple de code.  
* Familiarité de base avec les concepts Java et Excel.

---

## Étape 1 : Configurer le projet et importer les données

Tout d'abord, ajoutez Apache POI à votre projet. Si vous utilisez Maven, incluez la dépendance suivante :

```xml
<!-- pom.xml -->
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

Ensuite, obtenez les données source sous forme de `DataTable`. Dans un scénario réel, cela peut provenir d'une requête de base de données, d'un fichier CSV ou d'une réponse d'API.

```java
// Step 1: Obtain the source data as a DataTable
DataTable dataTable = getData();   // replace with your own data‑fetching logic
```

> **Conseil :** Assurez‑vous que les colonnes du `DataTable` ont les bons types Java (`Integer`, `Double`, etc.) car le format de nombre n'affecte que les cellules numériques.

---

## Étape 2 : Créer un **custom number format** pour la première colonne

Un **custom number format** indique à Excel comment afficher les valeurs numériques. Pour afficher les valeurs en devise, nous utilisons le format intégré `CURRENCY`, mais vous pouvez également définir des modèles tels que `"$#,##0.00"`.

```java
// Step 2: Prepare a Style array – one entry per column in the DataTable
Style[] columnStyles = new Style[dataTable.getColumns().size()];

// Step 3: Create a style for the first column and set it to display values as currency
// wb – existing Workbook instance (e.g., XSSFWorkbook for .xlsx files)
Workbook wb = new XSSFWorkbook();
columnStyles[0] = wb.createCellStyle();               // style first column
columnStyles[0].setDataFormat(
        wb.createDataFormat().getFormat(Style.CustomNumberFormat.CURRENCY));
```

**Pourquoi cela fonctionne :**  
* `createCellStyle()` renvoie un objet de style réutilisable.  
* `setDataFormat()` attache le **set currency format** au style, que Excel applique ensuite à chaque cellule utilisant ce style.  
* En stockant le style dans `columnStyles[0]`, nous garantissons que seule la première colonne reçoit le format de devise.

---

## Étape 3 : Importer le `DataTable` tout en appliquant les styles de colonne

Nous importons maintenant les données dans la feuille de calcul. La méthode `importDataTable` accepte le tableau de styles, nous permettant de **style first column** et de laisser les colonnes restantes avec le formatage par défaut.

```java
// Step 4: Import the DataTable into the worksheet, applying the column styles
// ws – existing Worksheet instance
Worksheet ws = wb.createSheet("Report");

// true  → import column headers
// 0,0   → start at cell A1
ws.getCells().importDataTable(dataTable, true, 0, 0, columnStyles);
```

L'appel ci‑dessus **sets Excel number format** uniquement pour la première colonne. Toutes les autres colonnes héritent du style par défaut du classeur, ce qui rend le code simple et efficace.

---

## Étape 4 : Enregistrer le classeur et vérifier le résultat

Enfin, écrivez le classeur dans un fichier et ouvrez‑le dans Excel pour confirmer que la première colonne affiche les symboles monétaires.

```java
// Step 5: Save the workbook to disk
try (FileOutputStream fileOut = new FileOutputStream("FormattedReport.xlsx")) {
    wb.write(fileOut);
}
System.out.println("Workbook saved as FormattedReport.xlsx");
```

**Résultat attendu :**  
Lorsque vous ouvrez *FormattedReport.xlsx*, les valeurs de la colonne A apparaissent avec le symbole monétaire approprié (par ex., `$1,234.00`). Toutes les autres colonnes conservent leur représentation numérique d'origine.

---

## Variantes courantes et cas limites

| Situation | Ajustement |
|-----------|------------|
| **Devise différente** (par ex., Euro) | Remplacez `Style.CustomNumberFormat.CURRENCY` par un modèle personnalisé : <br>`wb.createDataFormat().getFormat("\"€\"#,##0.00")` |
| **Plus d'une colonne stylisée** | Remplissez les entrées supplémentaires dans `columnStyles[]` avec leurs propres objets `CellStyle`. |
| **Ensembles de données volumineux** | Utilisez `importDataTable` par lots ou diffusez les lignes pour éviter `OutOfMemoryError`. |
| **Séparateurs spécifiques à la locale** | Utilisez `java.text.NumberFormat` pour générer un modèle sensible à la locale et le transmettre à `setDataFormat`. |

> **Attention :** Réutiliser un seul objet `CellStyle` sur de nombreuses colonnes peut entraîner un formatage inattendu car Excel limite le nombre de styles distincts par classeur. Créez un style séparé pour chaque format unique dont vous avez besoin.

---

## Exemple complet exécutable

Ci‑dessous se trouve un programme autonome qui démontre l’ensemble du flux de travail, de la création des données à l’enregistrement du classeur formaté.

```java
import java.io.FileOutputStream;
import java.util.ArrayList;
import java.util.List;

import org.apache.poi.ss.usermodel.*;
import org.apache.poi.xssf.usermodel.XSSFWorkbook;

/* Mock DataTable implementation for demonstration purposes */
class DataTable {
    private final List<String> columns = List.of("Amount", "Description");
    private final List<Object[]> rows = new ArrayList<>();

    public DataTable() {
        rows.add(new Object[]{1234.5, "Consulting"});
        rows.add(new Object[]{5678.9, "Licensing"});
    }

    public List<String> getColumns() { return columns; }
    public List<Object[]> getRows() { return rows; }
}

/* Helper that mimics the importDataTable method used in the original snippet */
class WorksheetHelper {
    private final Sheet sheet;
    private final Workbook wb;

    public WorksheetHelper(Workbook wb, Sheet sheet) {
        this.wb = wb;
        this.sheet = sheet;
    }

    public void importDataTable(DataTable dt, boolean includeHeaders,
                                int startRow, int startCol, Style[] styles) {
        int rowIdx = startRow;
        if (includeHeaders) {
            Row header = sheet.createRow(rowIdx++);
            for (int c = 0; c < dt.getColumns().size(); c++) {
                Cell cell = header.createCell(startCol + c);
                cell.setCellValue(dt.getColumns().get(c));
            }
        }
        for (Object[] rowData : dt.getRows()) {
            Row row = sheet.createRow(rowIdx++);
            for (int c = 0; c < rowData.length; c++) {
                Cell cell = row.createCell(startCol + c);
                Object value = rowData[c];
                if (value instanceof Number) {
                    cell.setCellValue(((Number) value).doubleValue());
                } else {
                    cell.setCellValue(value.toString());
                }
                // Apply custom style if provided
                if (styles != null && c < styles.length && styles[c] != null) {
                    cell.setCellStyle((CellStyle) styles[c]);
                }
            }
        }
    }
}

/* Main class that puts everything together */
public class CustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Obtain the source data
        DataTable dataTable = new DataTable();

        // 2️⃣ Create a workbook and a sheet
        Workbook wb = new XSSFWorkbook();
        Sheet ws = wb.createSheet("Report");

        // 3️⃣ Prepare a style array – one entry per column
        Style[] columnStyles = new Style[dataTable.getColumns().size()];

        // 4️⃣ Create a style for the first column (currency)
        CellStyle currencyStyle = wb.createCellStyle();
        DataFormat fmt = wb.createDataFormat();
        currencyStyle.setDataFormat(fmt.getFormat("$#,##0.00"));
        columnStyles[0] = currencyStyle;   // style first column

        // 5️⃣ Import the DataTable, applying the column styles
        WorksheetHelper helper = new WorksheetHelper(wb, ws);
        helper.importDataTable(dataTable, true, 0, 0, columnStyles);

        // 6️⃣ Save the workbook
        try (FileOutputStream out = new FileOutputStream("FormattedReport.xlsx")) {
            wb.write(out);
        }
        System.out.println("Workbook written to FormattedReport.xlsx");
    }
}
```

L’exécution du programme crée **FormattedReport.xlsx** où la colonne A (la colonne « Amount ») est affichée avec un **custom number format** qui montre le signe dollar et deux décimales.

---

## Conclusion

Vous savez maintenant comment **custom number format** une feuille de calcul Excel depuis Java, **format column as currency**, et **style first column** lors de l’importation de données. En créant un `CellStyle` réutilisable et en le passant à `importDataTable`, vous pouvez **set Excel number format** pour n’importe quelle colonne sans parcourir chaque cellule manuellement.

Ensuite, essayez :

* Utiliser `setDataFormat` avec des modèles spécifiques à la locale pour **set currency format**

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Définir le format de nombre Excel en Java – Guide complet](/cells/english/java/formatting/set-number-format-excel-in-java-complete-guide/)
- [Appliquer le format de nombre Excel en Java – Guide complet Aspose.Cells](/cells/english/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/)
- [Comment créer un classeur Excel avec un format de devise et une police en gras en Java](/cells/english/java/formatting/how-to-create-excel-workbook-with-currency-format-and-bold-f/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}