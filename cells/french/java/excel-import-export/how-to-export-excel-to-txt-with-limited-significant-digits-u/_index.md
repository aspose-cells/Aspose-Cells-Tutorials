---
category: general
date: 2026-08-17
description: Exporter Excel en TXT tout en limitant les chiffres significatifs – apprenez
  comment définir les chiffres et convertir Excel en texte en Java avec un exemple
  complet d’Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- how to set digits
- convert excel to text
- how to limit decimals
- limit significant digits
language: fr
lastmod: 2026-08-17
og_description: Exporter Excel en TXT tout en limitant les chiffres significatifs.
  Ce tutoriel montre comment définir le nombre de chiffres et convertir Excel en texte
  à l'aide d'Aspose.Cells pour Java.
og_image_alt: Java code exporting Excel to TXT with 4 significant digits
og_title: Exporter Excel en TXT avec un nombre limité de chiffres significatifs –
  Guide Java
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  headline: How to export Excel to TXT with limited significant digits using Java
  type: TechArticle
- description: Export Excel to TXT while limiting significant digits – learn how to
    set digits and convert Excel to text in Java with a complete Aspose.Cells example.
  name: How to export Excel to TXT with limited significant digits using Java
  steps:
  - name: Prerequisites
    text: '- Java 17 or later (the code compiles with Java 8 as well). - Aspose.Cells
      for Java 25.10 or newer. Download the JAR from the [Aspose website](https://products.aspose.com/cells/java)
      and add it to your project’s classpath. - An IDE or a simple text editor and
      command‑line build tool (Maven/Gradle).'
  - name: How the setting differs from “limit decimals”
    text: '- **limit decimals** (`setDecimalPlaces`) trims digits *after* the decimal
      point, regardless of the integer part. - **significant digits** (`setSignificantDigits`)
      counts digits from the first non‑zero digit, which is useful when numbers vary
      in magnitude.'
  - name: Expected output
    text: '| Cell | Original value | Exported (4 significant digits) | |------|----------------|---------------------------------|
      | A1 | 123.456789 | 123.5 |'
  - name: Exporting a whole range
    text: 'If you want to export more than one cell, simply fill the range before
      saving:'
  - name: Handling locale‑specific decimal separators
    text: 'Aspose.Cells respects the system locale when writing text. To force a dot
      (`.`) as the decimal separator, set the `TxtSaveOptions` culture:'
  - name: Overwriting existing files
    text: 'The `save` method overwrites the target file by default. If you need to
      avoid accidental data loss, check for file existence first:'
  - name: Large workbooks and memory usage
    text: 'When exporting very large worksheets, consider streaming the output:'
  - name: Next steps
    text: "- Explore other `TxtSaveOptions` properties such as `setDelimiter('\t')`
      to customize column separators. - Combine the exporter with `CsvSaveOptions`
      if you need comma‑separated values instead of plain text. - Integrate the routine
      into a web service that accepts uploaded Excel files and returns tri"
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel export
- TXT conversion
title: Comment exporter Excel en TXT avec un nombre limité de chiffres significatifs
  en Java
url: /fr/java/excel-import-export/how-to-export-excel-to-txt-with-limited-significant-digits-u/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Export Excel to TXT with limited significant digits using Java

Si vous devez **exporter Excel vers TXT** tout en contrôlant le nombre de chiffres significatifs, ce guide fournit une solution prête à l'emploi. Vous verrez comment définir les chiffres, convertir Excel en texte, et garder la sortie propre avec un seul changement de configuration.

L'exemple utilise Aspose.Cells for Java 25.10, qui introduit l'option `setSignificantDigits`. À la fin du tutoriel, vous pourrez générer un fichier TXT contenant uniquement les chiffres souhaités, sans code de arrondi supplémentaire.

## What you’ll achieve

- Créer un classeur (workbook) programmatique.
- Insérer une valeur numérique dans une cellule.
- Configurer les options d'enregistrement TXT pour limiter les chiffres significatifs.
- Enregistrer le classeur sous forme de fichier texte brut.
- Comprendre le fonctionnement du paramètre `significantDigits` et comment l'adapter à d'autres scénarios.

### Prerequisites

- Java 17 ou supérieur (le code se compile également avec Java 8).
- Aspose.Cells for Java 25.10 ou plus récent. Téléchargez le JAR depuis le [Aspose website](https://products.aspose.com/cells/java) et ajoutez‑le au classpath de votre projet.
- Un IDE ou un simple éditeur de texte et un outil de construction en ligne de commande (Maven/Gradle).

## Step 1: Set up the project and import Aspose.Cells

Créez un nouveau projet Java et ajoutez le JAR Aspose.Cells au chemin de construction. Si vous utilisez Maven, ajoutez la dépendance suivante dans `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.10</version>
    <classifier>jdk17</classifier>
</dependency>
```

> **Astuce :** Utilisez le classificateur `jdk17` pour le runtime Java le plus récent ; cela réduit le risque d’avertissements de compatibilité.

## Step 2: Create a workbook and write a value

Le classeur représente un fichier Excel en mémoire. Vous pouvez ajouter des données à n'importe quelle cellule en utilisant la méthode `putValue`.

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Put a numeric value into cell A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue(123.456789);
```

Le nombre `123.456789` sera la source de notre exportation TXT. Par défaut, Aspose.Cells écrirait toutes les décimales, ce qui produit souvent des fichiers texte bruyants.

## Step 3: Configure TXT save options to limit significant digits

Aspose.Cells fournit `TxtSaveOptions` pour un contrôle fin de la sortie texte brut. La méthode `setSignificantDigits` indique à l'exportateur combien de chiffres conserver **au total**, pas seulement après le point décimal.

```java
        // Configure TXT save options to keep only 4 significant digits
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4); // new option in 25.10
```

Lorsque `significantDigits` est fixé à `4`, l'exportateur arrondit la valeur `123.456789` à `123.5`. Ce comportement correspond à la définition mathématique des chiffres significatifs : les quatre premiers chiffres non nuls sont conservés.

### How the setting differs from “limit decimals”

- **limiter les décimales** (`setDecimalPlaces`) supprime les chiffres *après* le point décimal, quel que soit la partie entière.
- **chiffres significatifs** (`setSignificantDigits`) compte les chiffres à partir du premier chiffre non nul, ce qui est utile lorsque les nombres varient en magnitude.

Si vous avez besoin d'un nombre fixe de décimales à la place, remplacez la ligne ci‑dessus par :

```java
saveOptions.setDecimalPlaces(2); // keeps two digits after the decimal point
```

## Step 4: Save the workbook as a TXT file

Écrivez maintenant le classeur sur le disque en utilisant les options configurées.

```java
        // Save the workbook as a TXT file using the configured options
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

L'exécution du programme crée `significant_digits.txt` dans le répertoire de travail. Le fichier contient une seule ligne :

```
123.5
```

### Expected output

| Cellule | Valeur originale | Exporté (4 chiffres significatifs) |
|---------|------------------|------------------------------------|
| A1      | 123.456789       | 123.5                              |

Si vous changez `setSignificantDigits(4)` en `6`, le résultat devient `123.457`. Expérimentez avec différentes valeurs pour voir comment l'arrondi s'adapte.

## Step 5: Common variations and edge cases

### Exporting a whole range

Si vous souhaitez exporter plus d'une cellule, remplissez simplement la plage avant d'enregistrer :

```java
worksheet.getCells().get("B1").putValue(0.0012345);
worksheet.getCells().get("C1").putValue(98765.4321);
```

Le même paramètre `significantDigits` s'applique à chaque cellule numérique, garantissant une précision cohérente dans tout le fichier.

### Handling locale‑specific decimal separators

Aspose.Cells respecte la locale du système lors de l'écriture du texte. Pour forcer un point (`.`) comme séparateur décimal, définissez la culture de `TxtSaveOptions` :

```java
saveOptions.setCultureInfo(java.util.Locale.US);
```

Ceci est utile lorsque l'application cible attend un format spécifique, comme les analyseurs CSV qui n'acceptent que `.`.

### Overwriting existing files

La méthode `save` écrase le fichier cible par défaut. Si vous devez éviter une perte de données accidentelle, vérifiez d'abord l'existence du fichier :

```java
java.io.File outFile = new java.io.File("significant_digits.txt");
if (outFile.exists()) {
    throw new IllegalStateException("File already exists. Choose a different name or delete the existing file.");
}
workbook.save(outFile.getPath(), saveOptions);
```

### Large workbooks and memory usage

Lors de l'exportation de feuilles de calcul très volumineuses, envisagez de diffuser la sortie :

```java
saveOptions.setEnableMemorySaving(true);
```

Cette option réduit la consommation de heap en écrivant les lignes de façon incrémentielle.

## Full working example

Voici le programme complet que vous pouvez copier, coller et exécuter immédiatement :

```java
import com.aspose.cells.*;

public class SignificantDigitsDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Step 2: Put numeric values into cells
        worksheet.getCells().get("A1").putValue(123.456789);
        worksheet.getCells().get("B1").putValue(0.0012345);
        worksheet.getCells().get("C1").putValue(98765.4321);

        // Step 3: Configure TXT save options
        TxtSaveOptions saveOptions = new TxtSaveOptions();
        saveOptions.setSignificantDigits(4);          // limit to 4 significant digits
        saveOptions.setCultureInfo(java.util.Locale.US); // enforce dot as decimal separator
        saveOptions.setEnableMemorySaving(true);      // optional for large files

        // Step 4: Save the workbook as a TXT file
        workbook.save("significant_digits.txt", saveOptions);
    }
}
```

L'exécution de ce code produit `significant_digits.txt` avec le contenu suivant (colonnes séparées par des tabulations) :

```
123.5	0.001235	98770
```

Chaque nombre respecte la règle des **4 chiffres significatifs**, démontrant que le paramètre fonctionne sur différentes magnitudes.

## Conclusion

Vous savez maintenant comment **exporter Excel vers TXT** tout en contrôlant le nombre de chiffres significatifs. En utilisant `TxtSaveOptions.setSignificantDigits`, vous pouvez **définir les chiffres**, **limiter les décimales**, et **limiter les chiffres significatifs** en une seule ligne de code maintenable. L'approche fonctionne aussi bien pour des cellules uniques, des plages complètes que pour de grands classeurs.

### Next steps

- Explorez d'autres propriétés de `TxtSaveOptions` comme `setDelimiter('\t')` pour personnaliser les séparateurs de colonnes.
- Combinez l'exportateur avec `CsvSaveOptions` si vous avez besoin de valeurs séparées par des virgules au lieu de texte brut.
- Intégrez la routine dans un service web qui accepte des fichiers Excel téléchargés et renvoie une sortie TXT tronquée à la volée.

N'hésitez pas à expérimenter avec différentes limites de chiffres et locales. Si vous rencontrez un scénario où les options intégrées ne répondent pas à un besoin particulier, vous pouvez toujours post‑traiter le fichier TXT généré avec les utilitaires Java I/O standards.

Bon codage !

## What Should You Learn Next?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment convertir du texte en nombres dans Excel avec Aspose.Cells for Java](/cells/english/java/cell-operations/convert-text-to-numbers-excel-aspose-cells-java/)
- [Comment créer et exporter Excel en HTML avec Aspose.Cells Java | Guide des opérations de classeur](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Comment exporter des propriétés Excel personnalisées en PDF avec Aspose.Cells for Java](/cells/english/java/workbook-operations/export-excel-custom-properties-pdf-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}