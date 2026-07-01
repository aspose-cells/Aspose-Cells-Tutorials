---
category: general
date: 2026-06-30
description: Mettez le texte en gras lors de l'importation d'un DataTable vers Excel
  avec Java. Apprenez le code de mise en forme conditionnelle, importez un DataTable
  dans Excel et stylisez les tableaux sans effort.
draft: false
keywords:
- set font bold
- conditional formatting code
- import datatable excel
- how to import datatable
- import table with styles
language: fr
og_description: Définir la police en gras en Java lors de l'exportation d'un DataTable
  vers Excel. Ce guide couvre le code de mise en forme conditionnelle, l'importation
  d'un DataTable Excel et le style du tableau.
og_title: Définir le texte en gras dans l'export Excel Java – Tutoriel étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  headline: Set Font Bold in Java Excel Export – Complete Guide
  type: TechArticle
- description: Set font bold while importing a DataTable to Excel using Java. Learn
    conditional formatting code, import datatable excel and style tables effortlessly.
  name: Set Font Bold in Java Excel Export – Complete Guide
  steps:
  - name: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
    text: '**Create a mock `DataTable`** that mimics data you’d normally pull from
      a database.'
  - name: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
    text: '**Generate a `CellStyle` array** where every even column gets a bold font
      – that’s the core of **set font bold**.'
  - name: '**Grab the first worksheet** from the workbook.'
    text: '**Grab the first worksheet** from the workbook.'
  - name: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
    text: '**Import the `DataTable`** with column headers, starting at cell `A1`,
      and apply the prepared styles.'
  - name: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
    text: (Optional) **Add a conditional formatting rule** to illustrate the **conditional
      formatting code** keyword.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DataTable
title: Définir le texte en gras dans l'export Excel Java – Guide complet
url: /fr/java/formatting/set-font-bold-in-java-excel-export-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définir la police en gras dans l'exportation Excel Java – Guide complet

Vous vous êtes déjà demandé **comment mettre la police en gras** pour des colonnes spécifiques lors de l'**importation de fichiers Excel datatable** ? Vous n'êtes pas le seul. De nombreux développeurs se heurtent à un mur lorsqu'ils ont besoin d'une feuille de calcul bien stylisée sans ajuster manuellement chaque cellule. La bonne nouvelle ? En quelques lignes de Java, vous pouvez importer un `DataTable`, appliquer des polices en gras, et même ajouter un peu de **code de mise en forme conditionnelle** — le tout de manière programmatique.

Dans ce tutoriel, nous parcourrons un exemple complet et exécutable qui montre **comment importer un datatable** dans un classeur Excel, appliquer **set font bold** sur chaque colonne d'indice pair, et éventuellement ajouter un format conditionnel simple. À la fin, vous disposerez d'un extrait prêt à l'exécution et d'une compréhension claire de **import table with styles** pour tout projet.

## Prérequis

- Java 8 ou plus récent (le code fonctionne également avec Java 17)  
- Aspose.Cells for Java (la version d'essai gratuite suffit) – ajoutez la dépendance Maven ou le JAR à votre classpath.  
- Familiarité de base avec la conversion `java.sql` `ResultSet` → `DataTable` (nous simulerons une table pour simplifier).  
- Un IDE ou un outil de construction comme Maven/Gradle.

> **Astuce :** Si vous utilisez Maven, ajoutez ceci à votre `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- check for the latest version -->
</dependency>
```

## Vue d'ensemble de la solution

1. **Créer un `DataTable` factice** qui imite les données que vous extrairiez normalement d'une base de données.  
2. **Générer un tableau `CellStyle`** où chaque colonne paire reçoit une police en gras – c’est le cœur de **set font bold**.  
3. **Récupérer la première feuille de calcul** du classeur.  
4. **Importer le `DataTable`** avec les en‑têtes de colonnes, en commençant à la cellule `A1`, et appliquer les styles préparés.  
5. (Optionnel) **Ajouter une règle de mise en forme conditionnelle** pour illustrer le mot‑clé **conditional formatting code**.

Chaque étape est expliquée en anglais clair, et les blocs de code sont entièrement autonomes afin que vous puissiez copier‑coller et exécuter immédiatement.

---

## Étape 1 : Récupérer ou créer le DataTable à importer

Dans les applications réelles, vous appelleriez probablement des utilitaires de conversion `ResultSet` → `DataTable`. Pour ce guide, nous construirons manuellement un `DataTable` simple afin que vous puissiez vous concentrer sur la partie Excel.

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExportDemo {

    /** Creates a sample DataTable with three columns and a few rows. */
    private static DataTable getDataTable() {
        // Define column names
        List<String> columns = Arrays.asList("ID", "Name", "Score");

        // Create the DataTable and add columns
        DataTable table = new DataTable();
        for (String col : columns) {
            table.getColumns().add(col);
        }

        // Populate rows
        Object[][] rows = {
            {1, "Alice", 85},
            {2, "Bob", 92},
            {3, "Charlie", 78},
            {4, "Diana", 88}
        };

        for (Object[] row : rows) {
            DataRow dr = table.getRows().add();
            for (int i = 0; i < row.length; i++) {
                dr.get(i).setValue(row[i]);
            }
        }
        return table;
    }
```

> **Pourquoi c'est important :** Disposer d'un `DataTable` prêt nous permet de nous concentrer sur l'API **import datatable excel** et la logique de style. La méthode ci‑dessus est réutilisable — il suffit de remplacer les lignes codées en dur par une requête de base de données lorsque vous passez en production.

---

## Étape 2 : Préparer les styles – C’est ici que nous **Set Font Bold**

Nous allons maintenant construire un tableau d'objets `CellStyle`, un par colonne. La règle est simple : **set font bold** pour chaque colonne d'indice pair (0, 2, 4,…). Les colonnes impaires restent normales.

```java
    /** Creates a CellStyle array where even columns have a bold font. */
    private static CellStyle[] createColumnStyles(Workbook wb, DataTable table) {
        int columnCount = table.getColumns().size();
        CellStyle[] styles = new CellStyle[columnCount];

        for (int i = 0; i < columnCount; i++) {
            // Create a new style instance for the column
            styles[i] = wb.createStyle();

            // Set the font to bold if the column index is even
            Font font = styles[i].getFont();
            font.setBold(i % 2 == 0);   // <-- this line performs the set font bold action
        }
        return styles;
    }
```

### Pourquoi utiliser un tableau de styles ?

- **Performance :** Appliquer un style par colonne est plus rapide que de styliser chaque cellule individuellement.  
- **Cohérence :** Chaque cellule d'une colonne hérite du même formatage, garantissant un aspect uniforme.  
- **Scalabilité :** Ajouter plus de colonnes plus tard ne nécessite que d'étendre le tableau — aucune réécriture de code.

---

## Étape 3 : Accéder à la première feuille de calcul du classeur

Aspose.Cells crée une feuille de calcul par défaut pour nous, mais il est recommandé de la récupérer explicitement. Cela montre également **how to import datatable** dans une feuille spécifique.

```java
    /** Retrieves the first worksheet from the workbook. */
    private static Worksheet getFirstWorksheet(Workbook wb) {
        // Worksheets are zero‑based; index 0 is the first sheet.
        return wb.getWorksheets().get(0);
    }
```

---

## Étape 4 : Importer le DataTable avec styles – L'opération principale **Import Table With Styles**

La méthode `importDataTable` effectue le travail lourd. Elle copie les données, ajoute les en‑têtes de colonnes et applique le tableau de styles que nous avons construit précédemment.

```java
    /** Imports the DataTable into the worksheet, applying column styles. */
    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        // Parameters: (DataTable, import column headers?, start row, start column, styles)
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }
```

Lorsque vous exécuterez l'exemple, vous verrez **set font bold** appliqué aux colonnes `ID` et `Score`, tandis que `Name` reste normale.

---

## Étape 5 (Optionnel) : Ajouter une mise en forme conditionnelle – Un exemple rapide de **Conditional Formatting Code**

Si vous souhaitez mettre en évidence les lignes où le score dépasse 90, quelques lignes supplémentaires feront l'affaire. Cela met en avant le mot‑clé **conditional formatting code** sans perturber le flux principal.

```java
    /** Adds a simple conditional format that colors scores > 90 in green. */
    private static void addConditionalFormatting(Worksheet sheet) {
        // Define the range: rows 2‑5 (zero‑based), column C (index 2)
        int firstRow = 1;  // row after header
        int lastRow = sheet.getCells().getMaxDataRow();
        int scoreCol = 2;  // zero‑based index for "Score"

        // Build the range string, e.g., "C2:C5"
        String range = new StyleRegion(firstRow, scoreCol, lastRow, scoreCol).getRefersTo();

        // Create a new conditional formatting collection
        FormatConditionCollection fcc = sheet.getConditionalFormattings().add();

        // Add a condition: cell value > 90
        FormatCondition condition = fcc.addCondition(FormatConditionType.CELL_VALUE, OperatorType.GREATER_THAN, "90", null);
        condition.getStyle().setBackgroundColor(Color.getLightGreen());

        // Apply the condition to the range
        fcc.addArea(new CellArea(firstRow, scoreCol, lastRow, scoreCol));
    }
```

> **Note :** Le fragment ci‑dessus est optionnel mais montre comment vous pouvez superposer **conditional formatting code** sur la table déjà stylisée.

---

## Assemblage complet – Exemple complet et exécutable

```java
import com.aspose.cells.*;
import java.util.*;

public class ExcelExportDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Create a new workbook (in‑memory)
        Workbook wb = new Workbook();

        // 2️⃣ Retrieve the DataTable we want to export
        DataTable dataTable = getDataTable();

        // 3️⃣ Prepare column styles – this is where we set font bold
        CellStyle[] columnStyles = createColumnStyles(wb, dataTable);

        // 4️⃣ Grab the first worksheet
        Worksheet sheet = getFirstWorksheet(wb);

        // 5️⃣ Import the table with headers and our styles
        importTableWithStyles(sheet, dataTable, columnStyles);

        // 6️⃣ OPTIONAL: add a conditional formatting rule
        addConditionalFormatting(sheet);

        // 7️⃣ Save the workbook to disk
        String outPath = "StyledDataTable.xlsx";
        wb.save(outPath, SaveFormat.XLSX);
        System.out.println("Workbook saved to " + outPath);
    }

    // ----- Helper methods from earlier sections -----
    private static DataTable getDataTable() {
        List<String> columns = Arrays.asList("ID", "Name", "Score");
        DataTable table = new DataTable();
        for (String col : columns) {
            table.getColumns().add(col);
        }
        Object[][] rows = {
            {1, "Alice", 85},
            {2, "Bob", 92},
            {3, "Charlie", 78},
            {4, "Diana", 88}
        };
        for (Object[] row : rows) {
            DataRow dr = table.getRows().add();
            for (int i = 0; i < row.length; i++) {
                dr.get(i).setValue(row[i]);
            }
        }
        return table;
    }

    private static CellStyle[] createColumnStyles(Workbook wb, DataTable table) {
        int colCount = table.getColumns().size();
        CellStyle[] styles = new CellStyle[colCount];
        for (int i = 0; i < colCount; i++) {
            styles[i] = wb.createStyle();
            Font font = styles[i].getFont();
            font.setBold(i % 2 == 0);   // set font bold for even columns
        }
        return styles;
    }

    private static Worksheet getFirstWorksheet(Workbook wb) {
        return wb.getWorksheets().get(0);
    }

    private static void importTableWithStyles(Worksheet sheet, DataTable table, CellStyle[] styles) {
        sheet.getCells().importDataTable(table, true, 0, 0, styles);
    }

    private static void addConditionalFormatting(Worksheet sheet


## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Automatiser la mise en forme conditionnelle Excel avec Aspose.Cells pour Java : Guide complet](/cells/english/java/formatting/automate-conditional-formatting-excel-aspose-cells-java/)
- [Comment implémenter des paramètres de police personnalisés dans Aspose.Cells Java pour le formatage Excel](/cells/english/java/formatting/aspose-cells-java-custom-fonts/)
- [Définir la taille de police dans Excel avec Aspose.Cells Java – Guide complet](/cells/english/java/formatting/aspose-cells-java-set-font-size-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}