---
category: general
date: 2026-09-27
description: Créer un classeur Excel en Java, importer des données SQL, définir le
  format numérique d’une colonne et enregistrer le classeur au format XLSX à l’aide
  d’Aspose.Cells en Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create excel workbook java
- save workbook as xlsx
- import sql data excel
- add number format excel
- set number format column
language: fr
lastmod: 2026-09-27
og_description: Créer un classeur Excel en Java, importer des données SQL, définir
  le format numérique d’une colonne et enregistrer le classeur au format XLSX avec
  un exemple Java complet et fonctionnel.
og_image_alt: Screenshot of a Java program creating an Excel workbook with styled
  numeric columns
og_title: Créer un classeur Excel en Java – importer des données SQL et définir les
  formats numériques des colonnes
schemas:
- author: Aspose
  dateModified: '2026-09-27'
  description: Create Excel workbook java, import SQL data, set number format column,
    and save workbook as XLSX using Aspose.Cells in Java.
  headline: Create Excel workbook java and apply column number formats
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Data import
title: Créer un classeur Excel en Java et appliquer des formats numériques aux colonnes
url: /fr/java/formatting/create-excel-workbook-java-and-apply-column-number-formats/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Créer un classeur Excel en Java et appliquer des formats numériques aux colonnes

Si vous devez **créer un classeur Excel en Java** et styliser des colonnes numériques, ce guide vous montre exactement comment faire. Vous apprendrez à importer des données SQL dans Excel, à définir un format numérique pour chaque colonne, et à **enregistrer le classeur au format XLSX** à l’aide de la bibliothèque Aspose.Cells.

Travailler avec des feuilles de calcul depuis Java semble souvent fragmenté — les développeurs copient‑collent des extraits, oublient de formater les nombres, ou se retrouvent avec des fichiers CSV au lieu de vrais fichiers Excel. Ce tutoriel élimine ces frictions en proposant une solution unique, de bout en bout, que vous pouvez intégrer à n’importe quel projet Java.

À la fin de l’article vous serez capable de :

* Vous connecter à une base de données et récupérer un `DataTable` (ou `ResultSet`)  
* Créer un nouveau classeur avec Aspose.Cells  
* Appliquer un style **add number format excel** cohérent à chaque colonne  
* **Enregistrer le classeur au format XLSX** à l’emplacement de votre choix  

Le seul prérequis est un environnement de développement Java (JDK 8+ recommandé) et le JAR Aspose.Cells for Java présent dans votre classpath.

---

## Prérequis

| Exigence | Pourquoi c’est important |
|----------|---------------------------|
| JDK 8 ou version supérieure | Fournit les fonctionnalités du langage utilisées dans l’exemple. |
| Aspose.Cells for Java (dernière version) | Gère la création, le style et l’enregistrement d’Excel sans besoin d’Office installé. |
| Une base de données compatible JDBC (ex. : MySQL, PostgreSQL) | Fournit les données SQL que nous allons importer. |
| Maven ou Gradle (optionnel) | Simplifie la gestion des dépendances. |

Ajoutez Aspose.Cells à votre `pom.xml` Maven :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- use the latest stable version -->
</dependency>
```

Ou téléchargez le JAR directement depuis le site Aspose et ajoutez‑le au classpath de votre projet.

---

## Étape 1 : Créer un classeur Excel en Java

Le premier bloc logique consiste à instancier un nouveau `Workbook`. Cet objet représente l’ensemble du fichier Excel en mémoire et vous donne accès aux feuilles, aux cellules et aux styles.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook();
```

Créer le classeur dès le départ nous fournit également une usine `Style` dont nous aurons besoin plus tard pour **set number format column**.

---

## Étape 2 : Récupérer les données depuis SQL (import sql data excel)

Ci‑dessous, nous ouvrons une connexion JDBC, exécutons une simple instruction `SELECT`, et chargeons le résultat dans un `DataTable` Aspose. La classe `DataTable` imite le `DataTable` .NET et fonctionne de façon transparente avec la méthode `importDataTable`.

```java
// Step 2: Pull data from a database and fill a DataTable
private static DataTable getDataTableFromDb() throws SQLException {
    // Replace with your actual connection string, user, and password
    String url = "jdbc:mysql://localhost:3306/yourdb";
    String user = "your_user";
    String password = "your_password";

    try (Connection conn = DriverManager.getConnection(url, user, password);
         Statement stmt = conn.createStatement();
         ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

        // Aspose.Cells provides a utility to convert ResultSet → DataTable
        return CellsHelper.getDataTableFromResultSet(rs);
    }
}
```

> **Astuce :** Si vous avez déjà un `DataTable` provenant d’une autre source (ex. : parsing CSV), vous pouvez ignorer le code JDBC et renvoyer directement cette table.

---

## Étape 3 : Préparer un style réutilisable (add number format excel)

Nous voulons que chaque colonne numérique affiche les nombres avec deux décimales et un séparateur de milliers. Au lieu de styliser chaque cellule individuellement, nous créons un objet `Style` une fois par colonne et le réutilisons pendant l’importation. C’est la façon la plus efficace d’**add number format excel**.

```java
// Step 3: Build a style array – one style per column
private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
    Style[] styles = new Style[columnCount];
    for (int i = 0; i < columnCount; i++) {
        styles[i] = workbook.createStyle();
        // "0.00" = two decimal places; "#,##0.00" adds thousands separator
        styles[i].setNumber("#,##0.00");
    }
    return styles;
}
```

Vous pouvez adapter la chaîne de format (`"#,##0.00"`) à tout format numérique Excel dont vous avez besoin. Pour les dates, utilisez `styles[i].setCustom("mm-dd-yyyy")`, etc.

---

## Étape 4 : Importer le DataTable et appliquer les styles de colonne

Nous rassemblons maintenant le tout. La surcharge `importDataTable` nous permet de passer le `DataTable`, de spécifier si la première ligne doit être traitée comme en‑têtes de colonne, et de fournir le tableau de styles. Cela applique automatiquement **set number format column** à chaque cellule de la colonne correspondante.

```java
// Step 4: Import data with styles into the first worksheet
private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
    // Build a style for each column based on the number of columns in the DataTable
    Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());

    // Import the DataTable starting at cell A1 (row 0, column 0)
    workbook.getWorksheets().get(0).getCells()
            .importDataTable(dataTable, true, 0, 0, columnStyles);
}
```

Comme nous avons passé `true` pour le drapeau `importColumnNames`, la première ligne de la feuille contient les noms de colonnes du `DataTable`. Chaque ligne suivante reçoit les données, déjà formatées selon le style que nous avons défini.

---

## Étape 5 : Enregistrer le classeur au format xlsx

L’étape finale consiste à persister le classeur en mémoire dans un fichier physique. Aspose.Cells prend en charge de nombreux formats ; nous utiliserons le format moderne XLSX, celui attendu par la plupart des applications aujourd’hui.

```java
// Step 5: Save the workbook to an .xlsx file
private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
    workbook.save(filePath, com.aspose.cells.SaveFormat.XLSX);
}
```

Vous pouvez modifier `filePath` pour indiquer n’importe quel emplacement valide sur votre système. La méthode lève une `IOException` si le répertoire n’existe pas ou si vous n’avez pas les droits d’écriture.

---

## Exemple complet, exécutable

Assembler toutes les pièces donne un programme autonome que vous pouvez compiler et exécuter immédiatement.

```java
import com.aspose.cells.*;
import java.sql.*;

public class CreateExcelWorkbookJava {
    public static void main(String[] args) {
        try {
            // 1️⃣ Obtain data from the database
            DataTable dataTable = getDataTableFromDb();

            // 2️⃣ Create a new workbook that will hold the imported data
            Workbook workbook = new Workbook();

            // 3️⃣ Import the DataTable with a numeric style per column
            importDataWithStyles(workbook, dataTable);

            // 4️⃣ Save the workbook as XLSX
            String outputPath = "DataTableWithNumberFormat.xlsx";
            saveWorkbook(workbook, outputPath);

            System.out.println("Workbook created successfully at: " + outputPath);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    // ---- Helper methods (see earlier sections) ----
    private static DataTable getDataTableFromDb() throws SQLException {
        String url = "jdbc:mysql://localhost:3306/yourdb";
        String user = "your_user";
        String password = "your_password";

        try (Connection conn = DriverManager.getConnection(url, user, password);
             Statement stmt = conn.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT Id, Amount, CreatedDate FROM Payments")) {

            return CellsHelper.getDataTableFromResultSet(rs);
        }
    }

    private static Style[] buildColumnStyles(Workbook workbook, int columnCount) {
        Style[] styles = new Style[columnCount];
        for (int i = 0; i < columnCount; i++) {
            styles[i] = workbook.createStyle();
            styles[i].setNumber("#,##0.00"); // two decimals with thousands separator
        }
        return styles;
    }

    private static void importDataWithStyles(Workbook workbook, DataTable dataTable) {
        Style[] columnStyles = buildColumnStyles(workbook, dataTable.getColumns().size());
        workbook.getWorksheets().get(0).getCells()
                .importDataTable(dataTable, true, 0, 0, columnStyles);
    }

    private static void saveWorkbook(Workbook workbook, String filePath) throws IOException {
        workbook.save(filePath, SaveFormat.XLSX);
    }
}
```

### Résultat attendu

L’exécution du programme crée un fichier nommé **DataTableWithNumberFormat.xlsx** dans le répertoire de travail. Ouvrez‑le avec Microsoft Excel, LibreOffice Calc ou tout visualiseur compatible XLSX et vous verrez :

| Id | Amount | CreatedDate |
|----|--------|-------------|
| 1  | 1 234,56 | 2023‑01‑15 |
| 2  | 78 900,00 | 2023‑02‑20 |
| …  | … | … |

*La colonne **Amount** affiche les nombres avec deux décimales et un séparateur de milliers, grâce au style **add number format excel** que nous avons appliqué.*

---

## Questions fréquentes et gestion des cas particuliers

| Question | Réponse |
|----------|----------|
| **Et si ma requête ne renvoie aucune ligne ?** | Le `DataTable` sera vide mais contiendra toujours les définitions de colonnes. Le classeur ne contiendra que la ligne d’en‑tête, ce qui est souvent suffisant pour les processus en aval. |
| **Comment appliquer des formats différents selon les colonnes ?** | Modifiez `buildColumnStyles` pour inspecter le nom de la colonne ou le type de données et attribuer un format personnalisé (ex. : dates, pourcentages). |
| **Puis‑je écrire directement dans un `ByteArrayOutputStream` ?** | Oui. Remplacez `workbook.save(filePath, SaveFormat.XLSX);` par


## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Create and Save an Excel Workbook as SVG using Aspose.Cells for Java](/cells/english/java/workbook-operations/create-save-workbook-svg-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/hindi/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)
- [Create Save Excel Workbook Aspose Cells Java](/cells/german/java/workbook-operations/create-save-excel-workbook-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}