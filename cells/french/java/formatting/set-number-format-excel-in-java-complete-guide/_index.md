---
category: general
date: 2026-06-18
description: Définir le format numérique Excel avec Java, apprendre la notation scientifique
  en Java, écrire une valeur dans une cellule, définir le nombre de chiffres significatifs
  et exporter les données en xlsx en quelques minutes.
draft: false
keywords:
- set number format excel
- scientific notation java
- write value to cell
- set significant digits
- export data to xlsx
language: fr
og_description: Définir le format de nombre Excel avec Java. Apprenez à utiliser la
  notation scientifique en Java, écrire une valeur dans une cellule, définir le nombre
  de chiffres significatifs et exporter les données au format xlsx efficacement.
og_title: Définir le format de nombre Excel en Java – Tutoriel étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-18'
  description: Set number format Excel using Java and learn scientific notation java,
    write value to cell, set significant digits, and export data to xlsx in minutes.
  headline: Set Number Format Excel in Java – Complete Guide
  type: TechArticle
- description: Set number format Excel using Java and learn scientific notation java,
    write value to cell, set significant digits, and export data to xlsx in minutes.
  name: Set Number Format Excel in Java – Complete Guide
  steps:
  - name: Expected Output
    text: '| A (Formatted) | |---------------| | 1.235E7 |'
  - name: How do I change the number of significant digits?
    text: Just edit the format string. For three digits use `"0.###E0"`; for six digits
      use `"0.######E0"`.
  - name: What if I need a different locale (comma as decimal separator)?
    text: Add a locale‑aware format, e.g., `df.getFormat("0,####E0")`. Excel respects
      the user’s regional settings, so the comma will appear only if the workbook
      is opened on a system that uses it.
  - name: Can I apply the same style to an entire column?
    text: Absolutely. Create the style once (as shown) and then loop through rows,
      applying `cell.setCellStyle(sciStyle)` each time. For large sheets, consider
      using `sheet.setDefaultColumnStyle(columnIndex, sciStyle)` – it’s faster and
      keeps the code tidy.
  - name: What if I’m stuck with an older Java version that doesn’t support `var`?
    text: Replace `var` with the explicit type (`Workbook workbook = new XSSFWorkbook();`).
      The rest of the code stays identical.
  type: HowTo
tags:
- Java
- Excel
- Data Export
title: Définir le format de nombre Excel en Java – Guide complet
url: /fr/java/formatting/set-number-format-excel-in-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définir le format de nombre Excel en Java – Guide complet

Vous vous êtes déjà demandé comment **définir le format de nombre Excel** depuis un programme Java sans vous arracher les cheveux ? Vous n'êtes pas seul. Que vous génériez des rapports financiers ou que vous exportiez des journaux de capteurs, afficher correctement ces gros nombres dans un fichier *.xlsx* est une compétence indispensable.

Dans ce tutoriel, nous allons parcourir une solution pratique, de bout en bout : créer un classeur, configurer **scientific notation java**, limiter **set significant digits**, écrire une valeur dans une cellule, et enfin **export data to xlsx**. À la fin, vous disposerez d’un extrait autonome que vous pourrez coller directement dans votre projet.

## Ce que vous allez apprendre

- Comment initialiser un classeur avec JExcel‑API (ou Apache POI) en Java.  
- Les appels exacts pour **set number format excel** afin d’imposer la notation scientifique.  
- Comment **write value to cell** tout en préservant la précision.  
- Ajuster les paramètres du classeur pour **set significant digits** à un nombre personnalisé.  
- Enregistrer le fichier afin qu’il puisse être ouvert dans n’importe quelle application de feuille de calcul moderne (**export data to xlsx**).  

Aucun service externe, aucune magie. Juste du Java pur et quelques classes bien documentées.

---

## Prérequis

- JDK 17 ou supérieur (le code fonctionne aussi avec des versions antérieures, mais les exemples utilisent la syntaxe moderne `var` pour plus de concision).  
- Maven ou Gradle pour récupérer la dépendance `org.apache.poi:poi-ooxml`.  
- Une compréhension de base des collections Java – si vous avez déjà écrit une boucle `for`, vous êtes prêt.

---

## Étape 1 : Ajouter la dépendance Apache POI

Si vous utilisez Maven, collez ceci dans votre `pom.xml`. Les utilisateurs de Gradle peuvent le traduire en syntaxe `implementation`.

```xml
<dependency>
    <groupId>org.apache.poi</groupId>
    <artifactId>poi-ooxml</artifactId>
    <version>5.2.3</version>
</dependency>
```

> **Astuce :** Gardez POI à jour. La branche 5.x apporte un meilleur support des formats de nombre et des feuilles de calcul volumineuses.

---

## Étape 2 : Créer un classeur et accéder à ses paramètres  

La première chose dont nous avons besoin est un nouvel objet classeur. Apache POI n’expose pas de classe `WorkbookSettings` comme le faisait JExcel, mais nous pouvons obtenir le même effet en créant un `CellStyle` plus tard.

```java
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
import org.apache.poi.ss.usermodel.Workbook;

public class ExcelNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialise a new workbook (this is where we "set number format excel")
        Workbook workbook = new XSSFWorkbook();   // XSSFWorkbook -> .xlsx format
        // No explicit WorkbookSettings, we'll configure a CellStyle later
```

Pourquoi commencer avec un **nouveau classeur** ? Pensez-y comme une toile vierge ; chaque décision de formatage que nous prendrons plus tard sera appliquée à cette toile.  

---

## Étape 3 : Définir un CellStyle pour la notation scientifique et les chiffres significatifs  

Apache POI vous permet de créer une chaîne de format de données. Pour imposer **scientific notation java** et limiter le nombre de chiffres, nous utilisons le motif `"0.####E0"` – les symboles `#` contrôlent le nombre de chiffres significatifs affichés.

```java
import org.apache.poi.ss.usermodel.CellStyle;
import org.apache.poi.ss.usermodel.DataFormat;

// Inside main(), after workbook creation:
DataFormat df = workbook.createDataFormat();
CellStyle sciStyle = workbook.createCellStyle();

// "0.####E0" -> 0 before the decimal, up to 4 significant digits after, exponent part
sciStyle.setDataFormat(df.getFormat("0.####E0"));
```

*Que se passe-t-il ici ?* Le format indique à Excel : « Afficher le nombre en notation scientifique, mais ne garder que jusqu’à quatre chiffres significatifs ». Si vous avez besoin d’une précision différente, ajoutez ou retirez simplement des symboles `#`.  

---

## Étape 4 : Écrire un grand nombre dans une cellule  

Nous allons maintenant **write value to cell** *A1* en utilisant le style que nous venons de créer. Les objets `Sheet` et `Row` sont légers, donc les créer à la volée est peu coûteux.

```java
import org.apache.poi.ss.usermodel.Sheet;
import org.apache.poi.ss.usermodel.Row;
import org.apache.poi.ss.usermodel.Cell;

// Continue inside main():
Sheet sheet = workbook.createSheet("Numbers");

// Row 0 (first row), Cell 0 (column A)
Row row = sheet.createRow(0);
Cell cell = row.createCell(0);
cell.setCellValue(12345678.9);   // The raw value we want to store
cell.setCellStyle(sciStyle);    // Apply our scientific notation style
```

Remarquez que nous n’avons pas eu besoin de caster le nombre ; POI gère automatiquement le `double`. En appliquant `sciStyle`, nous garantissons que, lorsque l’utilisateur ouvrira le fichier, Excel affichera `1.235E7` (arrondi à quatre chiffres significatifs) plutôt que la chaîne brute à 8 chiffres.

---

## Étape 5 : Enregistrer le classeur – Export Data to XLSX  

La dernière étape consiste à **export data to xlsx**. Nous écrirons le classeur dans un fichier du répertoire courant, mais vous pouvez le placer où vous le souhaitez.

```java
import java.io.FileOutputStream;

// Still inside main():
try (FileOutputStream out = new FileOutputStream("sigDigits.xlsx")) {
    workbook.write(out);
}
workbook.close();   // Free resources
System.out.println("Workbook saved as sigDigits.xlsx");
    }
}
```

Lorsque vous double‑cliquerez sur `sigDigits.xlsx`, vous verrez la colonne **A** afficher `1.235E7` – exactement ce que nous avions demandé.

### Résultat attendu

| A (Formaté) |
|-------------|
| 1.235E7     |

Si vous ouvrez le fichier et modifiez le format de la cellule manuellement, vous constaterez que la valeur sous‑jacente reste `12345678.9`. C’est la magie de **set number format excel** : l’affichage change, les données restent intactes.

---

## Questions fréquentes & cas particuliers

### Comment changer le nombre de chiffres significatifs ?

Modifiez simplement la chaîne de format. Pour trois chiffres, utilisez `"0.###E0"` ; pour six chiffres, `"0.######E0"`.

### Et si j’ai besoin d’une locale différente (virgule comme séparateur décimal) ?

Ajoutez un format sensible à la locale, par exemple `df.getFormat("0,####E0")`. Excel respecte les paramètres régionaux de l’utilisateur, ainsi la virgule n’apparaîtra que si le classeur est ouvert sur un système qui l’utilise.

### Puis‑je appliquer le même style à toute une colonne ?

Absolument. Créez le style une fois (comme montré) puis parcourez les lignes en appliquant `cell.setCellStyle(sciStyle)` à chaque fois. Pour de grandes feuilles, envisagez `sheet.setDefaultColumnStyle(columnIndex, sciStyle)` – c’est plus rapide et cela garde le code propre.

### Que faire si je suis bloqué avec une version Java plus ancienne qui ne supporte pas `var` ?

Remplacez `var` par le type explicite (`Workbook workbook = new XSSFWorkbook();`). Le reste du code reste identique.

---

## Exemple complet fonctionnel (prêt à copier‑coller)

```java
import org.apache.poi.xssf.usermodel.XSSFWorkbook;
import org.apache.poi.ss.usermodel.*;

import java.io.FileOutputStream;

public class ExcelNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook (set number format excel)
        Workbook workbook = new XSSFWorkbook();

        // Define a style for scientific notation with 4 significant digits
        DataFormat df = workbook.createDataFormat();
        CellStyle sciStyle = workbook.createCellStyle();
        sciStyle.setDataFormat(df.getFormat("0.####E0")); // set significant digits

        // Access the first worksheet and write a large number into cell A1
        Sheet sheet = workbook.createSheet("Numbers");
        Row row = sheet.createRow(0);
        Cell cell = row.createCell(0);
        cell.setCellValue(12345678.9);   // write value to cell
        cell.setCellStyle(sciStyle);    // apply scientific notation

        // Save the workbook – export data to xlsx
        try (FileOutputStream out = new FileOutputStream("sigDigits.xlsx")) {
            workbook.write(out);
        }
        workbook.close();

        System.out.println("Workbook saved as sigDigits.xlsx");
    }
}
```

Exécutez la classe, ouvrez `sigDigits.xlsx`, et vous verrez le nombre affiché en notation scientifique avec exactement quatre chiffres significatifs. Voilà tout le workflow **set number format excel** en Java.

---

## Conclusion

Nous venons de couvrir tout ce qu’il faut pour **set number format excel** depuis Java : créer un classeur, concevoir un style en notation scientifique qui **set significant digits**, **write value to cell**, et enfin **export data to xlsx**. L’approche est légère, n’utilise que Apache POI, et fonctionne sur n’importe quelle plateforme supportant Java.

Ensuite, vous pourriez :

- Ajouter une mise en forme conditionnelle pour mettre en évidence les valeurs hors‑plage.  
- Générer plusieurs feuilles avec différents styles numériques (par ex., devise vs. scientifique).  
- Diffuser de grands ensembles de données avec `SXSSFWorkbook` pour des exportations économes en mémoire.

Essayez ces suggestions, et vous deviendrez la référence en automatisation Excel dans votre équipe. Des questions ou un cas d’usage particulier ? Laissez un commentaire ci‑dessous—bon codage ! 

*Image illustrant le flux de travail (alt text: “diagramme du workflow set number format excel montrant le code Java, la notation scientifique et l’exportation vers xlsx”)*
  

## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Set an Active Cell in Excel Using Aspose.Cells for Java: A Complete Guide](/cells/english/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Aspose Cells Java Set Active Cell Excel](/cells/german/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Aspose Cells Java Set Active Cell Excel](/cells/french/java/cell-operations/aspose-cells-java-set-active-cell-excel/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}