---
category: general
date: 2026-07-03
description: Inclure l'exportation des formules en Java pour convertir les cellules
  Excel en texte à l'aide d'Aspose.Cells. Apprenez comment imprimer une plage Excel
  et récupérer efficacement les valeurs des cellules sous forme de chaîne.
draft: false
keywords:
- include formulas export
- convert excel cells text
- print excel range
- export table options
- get cell values string
language: fr
og_description: Inclure l'exportation des formules en Java pour convertir les cellules
  Excel en texte. Guide étape par étape montrant comment imprimer une plage Excel
  et récupérer les valeurs des cellules sous forme de chaîne.
og_title: Inclure l'exportation des formules en Java – Convertir les cellules Excel
  en texte
schemas:
- author: Aspose
  dateModified: '2026-07-03'
  description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  headline: Include Formulas Export in Java – Convert Excel Cells to Text
  type: TechArticle
- description: Include formulas export in Java to convert Excel cells to text using
    Aspose.Cells. Learn how to print Excel range and get cell values string efficiently.
  name: Include Formulas Export in Java – Convert Excel Cells to Text
  steps:
  - name: Prerequisites
    text: '- Java 17 or newer (the code compiles with older versions but we’ll stick
      to the latest LTS). - Aspose.Cells for Java 23.10 (or any recent release)—you
      can grab it from Maven Central. - A sample `input.xlsx` placed in a folder you
      control (the path is hard‑coded in the example for clarity).'
  - name: Optional Tweaks
    text: '- `eto.setExportHiddenRows(true);` – include rows hidden in Excel. - `eto.setExportHiddenColumns(true);`
      – same for columns. - `eto.setExportAsHTML(true);` – get HTML instead of plain
      text.'
  - name: Expected Output (sample)
    text: '``` =SUM(A2:A3) 42 Hello =IF(B1>10,"Yes","No") =AVERAGE(C1:C3) =VLOOKUP(A1,Sheet2!A:B,2,FALSE)
      ```'
  - name: What if the range contains merged cells?
    text: Merged cells are treated as the value of the top‑left cell. The rest of
      the merged area will appear as empty strings. If you need the merged region’s
      address, query `Cell.getMergedRange()` before export.
  - name: Can I export a massive sheet (hundreds of thousands of rows)?
    text: Yes, but beware of memory consumption. Use `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)`
      to let Aspose.Cells stream data to disk. Also, consider exporting in chunks
      (e.g., 10 000 rows at a time) to keep the string manageable.
  - name: How do I change the column delimiter?
    text: '`ExportTableOptions` exposes `setSeparator(char separator)`. For CSV‑style
      output, set it to `'',''`:'
  - name: Do formulas respect external references?
    text: If a formula points to another workbook, Aspose.Cells will keep the reference
      text (`='[Other.xlsx]Sheet1'!A1`). It won’t evaluate the external value unless
      you load that workbook as well.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel
- Export
title: Inclure l'exportation des formules en Java – Convertir les cellules Excel en
  texte
url: /fr/java/excel-import-export/include-formulas-export-in-java-convert-excel-cells-to-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Inclure l'exportation des formules en Java – Convertir les cellules Excel en texte

Vous avez déjà eu besoin d'**inclure l'exportation des formules** lors de l'extraction de données d'un classeur Excel ? Peut-être construisez‑vous un service de reporting qui doit préserver les formules originales tout en fournissant un bloc de texte propre. Dans ce cas, vous êtes au bon endroit. Ce guide vous montre comment convertir les cellules Excel en texte brut—*y compris* les formules intégrées—en utilisant Aspose.Cells for Java.

Nous aborderons également comment **imprimer une plage Excel**, ajuster les **options d'exportation de tableau**, et enfin **obtenir la chaîne des valeurs de cellule** que vous pouvez consigner, envoyer via une API, ou stocker dans une base de données. À la fin, vous disposerez d'un extrait de code entièrement exécutable et d'une compréhension solide du pourquoi de chaque appel.

## Ce que vous en retirerez

- Un programme Java complet, prêt à copier‑coller, qui lit un fichier `.xlsx`, sélectionne une plage et l'exporte sous forme de chaîne formatée.
- Une compréhension de la classe `ExportTableOptions` et pourquoi activer `setExportAsString` et `setIncludeFormula` est important.
- Des astuces pour gérer de grandes feuilles de calcul, traiter différents types de données et personnaliser le format de sortie.
- Une checklist rapide des pièges courants (par exemple les cellules fusionnées, les lignes masquées et les formats numériques spécifiques à la locale).

### Prérequis

- Java 17 ou plus récent (le code compile avec des versions antérieures mais nous resterons sur la dernière LTS).
- Aspose.Cells for Java 23.10 (ou toute version récente) — vous pouvez le récupérer depuis Maven Central.
- Un fichier d'exemple `input.xlsx` placé dans un dossier que vous contrôlez (le chemin est codé en dur dans l'exemple pour plus de clarté).

Si vous avez déjà tout cela, plongeons‑y.

## Étape 1 : Configurer le projet et ajouter les dépendances

Tout d'abord, créez un projet Maven (ou Gradle, si vous le préférez). Ajoutez la dépendance Aspose.Cells à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Astuce :** Si vous utilisez un proxy d'entreprise, assurez‑vous que le dépôt est accessible ; sinon la construction échouera avec l’erreur « Could not resolve dependencies ».

Une fois que Maven a fini de télécharger, vous êtes prêt à écrire du Java.

## Étape 2 : Charger le classeur et récupérer la feuille de calcul souhaitée

La première ligne de l'exemple de code montre comment ouvrir un classeur existant :

```java
// Step 1: Load the workbook
Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

Remplacez `YOUR_DIRECTORY` par le chemin absolu ou relatif vers votre fichier. Le constructeur `Workbook` détecte automatiquement le format du fichier (XLS, XLSX, CSV, etc.), vous n’avez donc pas besoin de le spécifier.

Ensuite, nous récupérons la première feuille :

```java
// Step 2: Get the first worksheet
Worksheet ws = wb.getWorksheets().get(0);
```

Pourquoi la première feuille ? Dans de nombreux modèles, les données se trouvent sur le premier onglet, mais vous pouvez passer n'importe quel indice ou même utiliser `get("SheetName")` si vous préférez une approche nommée.

## Étape 3 : Définir la plage que vous souhaitez exporter

Voici maintenant le cœur de l'opération **convert excel cells text**. Vous indiquez à Aspose.Cells quelles cellules extraire en créant un objet `Range` :

```java
// Step 3: Create a range covering cells A1 to C3
Range rng = ws.getCells().createRange("A1:C3");
```

La chaîne `"A1:C3"` est une adresse classique de style A1. Elle peut également être construite de façon programmatique :

```java
int firstRow = 0, firstCol = 0, totalRows = 3, totalCols = 3;
Range rng = ws.getCells().createRange(firstRow, firstCol, totalRows, totalCols);
```

Cette flexibilité est utile lorsque la taille de la plage est dynamique—par exemple, vous lisez la dernière ligne utilisée avec `ws.getCells().getMaxDataRow()`.

## Étape 4 : Configurer les options d'exportation de tableau pour inclure les formules

C’est ici que réside la magie de **include formulas export**. Par défaut, Aspose.Cells renvoie les valeurs *affichées*. Si une cellule contient `=SUM(A1:A3)`, vous obtiendrez le nombre calculé, pas le texte de la formule. Pour changer cela, configurez `ExportTableOptions` :

```java
// Step 4: Set up export options to return the range as a string and include formulas
ExportTableOptions eto = new ExportTableOptions();
eto.setExportAsString(true);      // Forces the result to be a single string
eto.setIncludeFormula(true);      // Includes the underlying formula instead of the evaluated value
```

Pourquoi ces deux indicateurs ? `setExportAsString(true)` indique à l'API de concaténer les cellules en utilisant le délimiteur par défaut (tabulation pour les colonnes, saut de ligne pour les lignes). `setIncludeFormula(true)` change la source de la valeur de « valeur affichée » à « formule brute ». Si vous ne voulez que les valeurs, laissez‑le à `false`.

### Ajustements optionnels

- `eto.setExportHiddenRows(true);` – inclure les lignes masquées dans Excel.
- `eto.setExportHiddenColumns(true);` – même chose pour les colonnes.
- `eto.setExportAsHTML(true);` – obtenir du HTML au lieu du texte brut.

N'hésitez pas à expérimenter ; la classe d'options est un terrain de jeu **export table options**.

## Étape 5 : Récupérer la plage sous forme de chaîne formatée

Nous extrayons maintenant les données :

```java
// Step 5: Retrieve the range values as a formatted string using the options
String txt = rng.getValueAsString(eto);
```

Le `txt` retourné ressemble à ceci (en supposant que A1:C3 contienne un mélange de valeurs et de formules) :

```
=SUM(A2:A3)	42	"Hello"
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Remarquez la tabulation (`\t`) séparant les colonnes et le saut de ligne (`\n`) séparant les lignes. Vous pouvez diviser la chaîne plus tard si vous avez besoin d'un tableau 2‑D :

```java
String[] rows = txt.split("\n");
for (String row : rows) {
    String[] cells = row.split("\t");
    // Process each cell...
}
```

## Étape 6 : Imprimer le résultat – « Print Excel Range » simplifié

Enfin, nous affichons la chaîne dans la console :

```java
// Step 6: Print the resulting string
System.out.println(txt);
```

L'exécution du programme affiche exactement la sortie montrée ci‑dessus. À partir de là, vous pouvez écrire la chaîne dans un fichier de log, l'envoyer via HTTP, ou la stocker dans un document NoSQL.

## Exemple complet, prêt à exécuter

En rassemblant le tout, voici le programme complet. Copiez, collez et cliquez sur **Run**—aucune importation manquante.

```java
import com.aspose.cells.*;

public class ExportFormulaRange {
    public static void main(String[] args) throws Exception {
        // Load the workbook
        Workbook wb = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Grab the first worksheet
        Worksheet ws = wb.getWorksheets().get(0);

        // Define the range A1:C3 (adjust as needed)
        Range rng = ws.getCells().createRange("A1:C3");

        // Configure export options: string output + include formulas
        ExportTableOptions eto = new ExportTableOptions();
        eto.setExportAsString(true);
        eto.setIncludeFormula(true);

        // Get the string representation of the range
        String txt = rng.getValueAsString(eto);

        // Print the resulting text
        System.out.println(txt);
    }
}
```

### Sortie attendue (exemple)

```
=SUM(A2:A3)	42	Hello
=IF(B1>10,"Yes","No")	=AVERAGE(C1:C3)	=VLOOKUP(A1,Sheet2!A:B,2,FALSE)
```

Si votre classeur contient des nombres formatés comme des dates, ils apparaîtront dans le format spécifique à la locale (par ex., `2026‑07‑03`). Pour forcer le format ISO, vous pouvez ajuster `ExportTableOptions` avec un `NumberFormat` personnalisé.

## Gestion des cas limites et questions fréquentes

### Que faire si la plage contient des cellules fusionnées ?

Les cellules fusionnées sont traitées comme la valeur de la cellule en haut à gauche. Le reste de la zone fusionnée apparaîtra comme des chaînes vides. Si vous avez besoin de l'adresse de la région fusionnée, interrogez `Cell.getMergedRange()` avant l'export.

### Puis‑je exporter une feuille massive (des centaines de milliers de lignes) ?

Oui, mais attention à la consommation de mémoire. Utilisez `Workbook.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE)` pour permettre à Aspose.Cells de diffuser les données sur le disque. En outre, envisagez d'exporter par morceaux (par ex., 10 000 lignes à la fois) pour garder la chaîne gérable.

### Comment changer le délimiteur de colonne ?

`ExportTableOptions` expose `setSeparator(char separator)`. Pour une sortie de type CSV, définissez‑le à `','` :

```java
eto.setSeparator(',');
```

### Les formules respectent‑elles les références externes ?

Si une formule pointe vers un autre classeur, Aspose.Cells conservera le texte de référence (`='[Other.xlsx]Sheet1'!A1`). Elle n'évaluera pas la valeur externe à moins que vous ne chargiez également ce classeur.

## Astuces pro pour un code prêt pour la production

- **Cachez le classeur** si vous lisez le

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment créer et exporter Excel en HTML avec Aspose.Cells Java | Guide des opérations de classeur](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Comment convertir Excel en PDF en Java avec Aspose.Cells&#58; Guide étape par étape](/cells/english/java/workbook-operations/convert-excel-to-pdf-aspose-cells-java/)
- [Exporter un classeur Excel en image avec Aspose.Cells for Java&#58; Guide étape par étape](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}