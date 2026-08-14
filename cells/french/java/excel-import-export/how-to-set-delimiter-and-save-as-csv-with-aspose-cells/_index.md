---
category: general
date: 2026-08-14
description: Comment définir le séparateur et enregistrer en CSV avec Aspose.Cells,
  limiter le nombre de chiffres, exporter des chaînes CSV et recalculer les formules
  en Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set delimiter
- save as csv
- recalculate formulas
- how to export csv
- how to limit digits
language: fr
lastmod: 2026-08-14
og_description: Comment définir le délimiteur et enregistrer en CSV avec Aspose.Cells,
  limiter les chiffres, exporter des chaînes CSV et recalculer les formules en Java.
og_image_alt: Screenshot of Java code that sets a CSV delimiter and saves an Excel
  workbook as CSV using Aspose.Cells
og_title: Comment définir le délimiteur et enregistrer en CSV – Guide Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  headline: How to set delimiter and save as CSV with Aspose.Cells
  type: TechArticle
- description: How to set delimiter and save as CSV using Aspose.Cells, limit digits,
    export CSV strings, and recalculate formulas in Java.
  name: How to set delimiter and save as CSV with Aspose.Cells
  steps:
  - name: Why this works
    text: "- `CsvSaveOptions.setDelimiter(char)` tells Aspose.Cells which character
      separates fields. By default it’s a comma, but any character (tab `'\t'`, pipe
      `'|'`, etc.) works. - `setSignificantDigits(int)` limits numeric precision,
      satisfying the **how to limit digits** requirement without manually form"
  - name: When to use this
    text: '- Returning CSV from a REST endpoint (`@RestController` in Spring) - Embedding
      CSV data into an email attachment without writing to disk - Performing quick
      sanity checks during unit tests'
  - name: Why recalculate?
    text: '- Formulas may reference external data or volatile functions (`NOW()`,
      `RAND()`) that need fresh values. - Dynamic‑array formulas (e.g., `=SORT(A1:A10)`)
      are evaluated automatically, but calling `calculateFormula()` guarantees consistency
      across all sheets.'
  - name: Verifying the result
    text: 1. Open `output.csv` in a text editor – you should see a semicolon (`;`)
      separating each column. 2. Confirm that numeric columns display at most five
      significant digits. 3. The console output will print the CSV string generated
      in step 4. 4. Open `japan_updated.xlsx` in Excel – any formulas that pre
  type: HowTo
tags:
- Aspose.Cells
- Java
- CSV export
- Excel automation
title: Comment définir le délimiteur et enregistrer en CSV avec Aspose.Cells
url: /fr/java/excel-import-export/how-to-set-delimiter-and-save-as-csv-with-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment définir le délimiteur et enregistrer en CSV avec Aspose.Cells

Si vous avez besoin de **définir le délimiteur** lors de l'exportation de données depuis un classeur Excel, ce guide vous présente une solution complète, de bout en bout, utilisant Aspose.Cells pour Java. Vous apprendrez comment configurer le délimiteur CSV, limiter le nombre de chiffres significatifs, exporter une chaîne CSV et actualiser les formules à tableau dynamique après le chargement d'un classeur.

Le tutoriel couvre tout ce dont vous avez besoin pour exécuter le code sur votre machine, y compris la gestion de calendriers spéciaux tels que le règne de l'empereur japonais. À la fin, vous serez capable de générer des fichiers CSV précis, de contrôler la précision numérique et de garantir que les formules sont à jour.

## Prérequis

- Java 17 ou version ultérieure (le code se compile également avec JDK 11+)
- Aspose.Cells pour Java 23.9 ou plus récent – téléchargez depuis le [site Aspose](https://products.aspose.com/cells/java/)
- Familiarité de base avec Maven ou Gradle pour la gestion des dépendances
- Un IDE (IntelliJ IDEA, Eclipse, VS Code) ou un simple éditeur de texte et la ligne de commande

> **Astuce :** Utilisez un dossier `libs` dédié ou Maven Central pour garder le JAR Aspose.Cells sur votre classpath. Les exemples ci‑dessus supposent un projet Maven.

## Étape 1 : Configurer le projet Maven

Créez un `pom.xml` contenant la dépendance Aspose.Cells :

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" 
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>aspose-csv-demo</artifactId>
    <version>1.0.0</version>
    <properties>
        <maven.compiler.source>17</maven.compiler.source>
        <maven.compiler.target>17</maven.compiler.target>
    </properties>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>23.9</version>
            <classifier>jdk17</classifier>
        </dependency>
    </dependencies>
</project>
```

Exécutez `mvn clean compile` pour télécharger la bibliothèque et vérifier que la construction réussit.

## Étape 2 : Définir le délimiteur et enregistrer en CSV

L'objectif principal est de remplacer le délimiteur virgule par défaut par un caractère personnalisé (par ex., le point‑virgule) lors de l'enregistrement d'un classeur Excel au format CSV. Aspose.Cells fournit `CsvSaveOptions` à cet effet.

```java
package com.example;

import com.aspose.cells.*;

public class CsvDelimiterDemo {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook (replace the path with your file)
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Configure CSV save options
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        // Primary requirement: set a custom delimiter
        csvOptions.setDelimiter(';');               // <-- how to set delimiter
        // Optional: limit the number of significant digits
        csvOptions.setSignificantDigits(5);         // <-- how to limit digits

        // Save the workbook as CSV using the configured options
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);

        System.out.println("CSV file saved with ';' delimiter and 5‑digit precision.");
    }
}
```

### Pourquoi cela fonctionne

- `CsvSaveOptions.setDelimiter(char)` indique à Aspose.Cells quel caractère sépare les champs. Par défaut, c’est une virgule, mais tout caractère (tabulation `'\t'`, pipe `'|'`, etc.) fonctionne.
- `setSignificantDigits(int)` limite la précision numérique, répondant à la exigence **comment limiter les chiffres** sans formater manuellement chaque cellule.

#### Résultat attendu

Le fichier `output.csv` contiendra des lignes comme :

```
Name;Amount;Date
Alice;123.46;2024-01-15
Bob;78.90;2024-01-16
```

Remarquez que les nombres sont arrondis à cinq chiffres significatifs (par ex., `123.45678` → `123.46`).

## Étape 3 : Limiter les chiffres lors de l'enregistrement en CSV

Si vous avez besoin d’un contrôle plus strict sur le formatage numérique, vous pouvez également utiliser une instance `CsvSaveOptions` pour spécifier une chaîne de format de nombre personnalisée.

```java
CsvSaveOptions csvOptions = new CsvSaveOptions();
csvOptions.setDelimiter(',');                // standard comma delimiter
csvOptions.setNumberFormat("0.####");        // up to 4 decimal places
csvOptions.setSignificantDigits(6);          // overall significant digits
```

- `setNumberFormat` suit les modèles de style .NET, que Aspose.Cells respecte.
- Combiner `setNumberFormat` et `setSignificantDigits` vous offre un arrondi prévisible selon les différentes locales.

## Étape 4 : Exporter le CSV en tant que chaîne avec un délimiteur personnalisé

Parfois, vous ne voulez pas de fichier physique ; vous avez besoin des données CSV en mémoire (par ex., pour les envoyer comme réponse HTTP). La classe `ExportTableOptions` vous permet d’exporter une plage sous forme de chaîne.

```java
// Export a range (rows 0‑9, columns 0‑4) as a CSV string
ExportTableOptions exportOptions = new ExportTableOptions();
exportOptions.setExportAsString(true);   // return a string instead of a file
exportOptions.setDelimiter(',');         // <-- how to set delimiter for export
exportOptions.setIncludeColumnNames(true);

String csvData = workbook.getWorksheets()
                         .get(0)                     // first worksheet
                         .getCells()
                         .exportDataTableAsString(0, 0, 10, 5, exportOptions);

System.out.println("Exported CSV string:");
System.out.println(csvData);
```

### Quand l’utiliser

- Retourner le CSV depuis un point d’accès REST (`@RestController` dans Spring)
- Intégrer les données CSV dans une pièce jointe d’email sans écrire sur le disque
- Effectuer des vérifications rapides lors de tests unitaires

## Étape 5 : Recalculer les formules après le chargement d’un classeur

Si votre classeur contient des formules—en particulier les **formules à tableau dynamique** introduites dans les versions récentes d’Excel—vous devez les recalculer après le chargement du fichier. Aspose.Cells rafraîchit automatiquement les résultats des tableaux dynamiques, mais vous devez tout de même appeler `calculateFormula()` pour les formules classiques.

```java
// Load a workbook that uses the Japanese Emperor calendar (optional step)
LoadOptions loadOptions = new LoadOptions();
loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

// Recalculate all formulas in the workbook
japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

// Save the refreshed workbook (preserves the original calendar)
japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
System.out.println("Formulas recalculated and workbook saved.");
```

### Pourquoi recalculer ?

- Les formules peuvent référencer des données externes ou des fonctions volatiles (`NOW()`, `RAND()`) qui nécessitent des valeurs actualisées.
- Les formules à tableau dynamique (par ex., `=SORT(A1:A10)`) sont évaluées automatiquement, mais appeler `calculateFormula()` garantit la cohérence sur toutes les feuilles.

## Étape 6 : Exemple complet de bout en bout

Ci‑dessous se trouve une classe unique qui démontre **comment définir le délimiteur**, **enregistrer en CSV**, **limiter les chiffres**, **exporter une chaîne CSV**, **charger un classeur avec un calendrier spécial**, et **recalculer les formules**. Le code est prêt à être copié‑collé dans votre projet.

```java
package com.example;

import com.aspose.cells.*;

public class AsposeCsvFullDemo {
    public static void main(String[] args) throws Exception {
        // -----------------------------------------------------------------
        // 1. Load an existing workbook
        // -----------------------------------------------------------------
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // -----------------------------------------------------------------
        // 2. Configure CSV save options (delimiter + digit limit)
        // -----------------------------------------------------------------
        CsvSaveOptions csvOptions = new CsvSaveOptions();
        csvOptions.setDelimiter(';');          // <-- how to set delimiter
        csvOptions.setSignificantDigits(5);    // <-- how to limit digits

        // -----------------------------------------------------------------
        // 3. Save the workbook as CSV
        // -----------------------------------------------------------------
        workbook.save("YOUR_DIRECTORY/output.csv", csvOptions);
        System.out.println("Saved CSV with ';' delimiter.");

        // -----------------------------------------------------------------
        // 4. Export a range as a CSV string (custom delimiter)
        // -----------------------------------------------------------------
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);
        exportOptions.setDelimiter(',');       // <-- how to set delimiter for export
        exportOptions.setIncludeColumnNames(true);

        String csvString = workbook.getWorksheets()
                                   .get(0)
                                   .getCells()
                                   .exportDataTableAsString(0, 0, 10, 5, exportOptions);
        System.out.println("CSV string exported:");
        System.out.println(csvString);

        // -----------------------------------------------------------------
        // 5. Load a workbook that uses the Japanese Emperor calendar
        // -----------------------------------------------------------------
        LoadOptions loadOptions = new LoadOptions();
        loadOptions.setCalendar(CalendarType.JAPANESE_EMPEROR_REIGN);
        Workbook japaneseWorkbook = new Workbook("YOUR_DIRECTORY/japan.xlsx", loadOptions);

        // -----------------------------------------------------------------
        // 6. Recalculate formulas (including dynamic‑array formulas)
        // -----------------------------------------------------------------
        japaneseWorkbook.calculateFormula();   // <-- recalculate formulas

        // -----------------------------------------------------------------
        // 7. Save the refreshed workbook
        // -----------------------------------------------------------------
        japaneseWorkbook.save("YOUR_DIRECTORY/japan_updated.xlsx");
        System.out.println("Japanese workbook refreshed and saved.");
    }
}
```

### Vérification du résultat

1. Ouvrez `output.csv` dans un éditeur de texte – vous devriez voir un point‑virgule (`;`) séparant chaque colonne.
2. Confirmez que les colonnes numériques affichent au maximum cinq chiffres significatifs.
3. La sortie console affichera la chaîne CSV générée à l’étape 4.
4. Ouvrez `japan_updated.xlsx` dans Excel – toutes les formules qui affichaient auparavant `#REF!` ou des valeurs obsolètes afficheront maintenant les résultats corrects.

## Pièges courants et comment les éviter

| Problème | Cause | Solution |
|----------|-------|----------|
| Le CSV affiche des guillemets supplémentaires | Les cellules contiennent des virgules alors que le délimiteur est également une virgule | Utilisez un délimiteur différent (`;` ou `\t`) via `setDelimiter` |
| Les nombres sont arrondis de façon incorrecte | `setSignificantDigits` appliqué après le format de nombre personnalisé | Appliquez `setNumberFormat` **avant** `setSignificantDigits` |

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment charger et enregistrer Excel en CSV avec Aspose.Cells pour Java : Guide complet](/cells/english/java/workbook-operations/aspose-cells-java-load-save-excel-csv/)
- [Comment charger un fichier CSV avec Aspose.Cells pour Java : Guide complet](/cells/english/java/workbook-operations/load-csv-aspose-cells-java-tutorial/)
- [Comment charger des fichiers CSV avec des analyseurs personnalisés en Java avec Aspose.Cells](/cells/english/java/import-export/load-csv-files-custom-parsers-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}