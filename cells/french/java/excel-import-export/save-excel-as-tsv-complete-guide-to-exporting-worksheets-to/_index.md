---
category: general
date: 2026-06-27
description: Enregistrez rapidement un fichier Excel au format TSV avec Java. Apprenez
  à exporter une feuille de calcul en texte, à exporter la feuille en texte brut et
  à exporter la chaîne de données Excel avec Aspose.Cells.
draft: false
keywords:
- save excel as tsv
- export worksheet to text
- export sheet plain text
- export excel data string
language: fr
og_description: Enregistrez Excel au format TSV avec Java. Ce tutoriel montre comment
  exporter une feuille de calcul en texte, exporter la feuille en texte brut et exporter
  efficacement les données Excel sous forme de chaîne.
og_title: Enregistrer Excel au format TSV – Guide d'exportation étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-27'
  description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  headline: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  type: TechArticle
- description: Save Excel as TSV quickly using Java. Learn how to export worksheet
    to text, export sheet plain text, and export Excel data string with Aspose.Cells.
  name: Save Excel as TSV – Complete Guide to Exporting Worksheets to Text
  steps:
  - name: Pro tip
    text: If you’re dealing with password‑protected files, call `new Workbook("file.xlsx",
      new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.
  - name: 'Edge case: Custom delimiters'
    text: 'If your downstream system expects a pipe (`|`) instead of a tab, just change
      the delimiter:'
  - name: Pro tip
    text: 'After exporting, you can also capture the string directly:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Excel automation
title: Enregistrer Excel au format TSV – Guide complet pour exporter les feuilles
  de calcul en texte
url: /fr/java/excel-import-export/save-excel-as-tsv-complete-guide-to-exporting-worksheets-to/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Enregistrer Excel en TSV – Guide complet pour exporter les feuilles de calcul en texte

Vous avez déjà eu besoin de **save Excel as TSV** sans savoir quel appel d’API utiliser ? Vous n’êtes pas seul. De nombreux développeurs se heurtent à un mur lorsqu’ils essaient de transformer une feuille de calcul en fichier à délimitation par tabulations pour un traitement en aval. La bonne nouvelle ? En quelques lignes de Java et Aspose.Cells, vous pouvez exporter une feuille de calcul en texte, exporter la feuille en texte brut, et même exporter la chaîne de données Excel sans transpirer.

Dans ce tutoriel, nous parcourrons l’ensemble du flux de travail — du chargement d’un classeur à la configuration des options d’exportation, puis à l’écriture du fichier TSV sur le disque. À la fin, vous serez capable de **save Excel as TSV** dans n’importe quel projet Java, que vous manipuliez une seule feuille ou que vous traitiez des dizaines de fichiers en lot.

## Ce que couvre ce guide

* Chargement d’un classeur Excel depuis le disque  
* Sélection de la bonne feuille de calcul (ou itération sur plusieurs)  
* Configuration de `ExportTableOptions` pour produire une sortie texte brut  
* Écriture des données sous forme de fichier à valeurs séparées par des tabulations (TSV)  
* Astuces pour gérer de grandes plages, différents délimiteurs et les caractères Unicode  

Aucun outil externe requis — seulement Aspose.Cells pour Java et un runtime Java 8+.

---

## Étape 1 : Configurez votre projet et chargez le classeur

Avant de plonger dans le code, assurez‑vous d’avoir ajouté le JAR Aspose.Cells à votre classpath. Si vous utilisez Maven, la dépendance ressemble à ceci :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- Use the latest stable version -->
</dependency>
```

Nous pouvons maintenant charger le classeur :

```java
// Step 1: Load the workbook
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

// Quick sanity check – print the number of worksheets
System.out.println("Worksheets count: " + workbook.getWorksheets().getCount());
```

> **Pourquoi c’est important :** Le chargement du fichier est la première étape de tout workflow **export Excel data string**. Si le fichier ne peut pas être ouvert, rien d’autre ne fonctionnera.

### Astuce pro
Si vous traitez des fichiers protégés par mot de passe, appelez `new Workbook("file.xlsx", new LoadOptions(LoadFormat.XLSX) {{ setPassword("yourPassword"); }})`.

---

## Étape 2 : Choisissez la feuille de calcul à exporter

Vous pouvez récupérer la première feuille, une feuille par son nom, ou itérer sur toutes. Voici le cas le plus simple — exporter la première feuille :

```java
// Step 2: Access the first worksheet (or any specific sheet)
Worksheet ws = workbook.getWorksheets().get(0);
System.out.println("Exporting sheet: " + ws.getName());
```

Si vous devez **export worksheet to text** pour chaque feuille, encapsulez le code ci‑dessus dans une boucle `for` :

```java
for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    // Export each sheet separately...
}
```

---

## Étape 3 : Créez et configurez les options d’exportation

Le cœur de **export sheet plain text** réside dans `ExportTableOptions`. En basculant quelques propriétés, nous transformons la plage en une chaîne texte brute avec un délimiteur tabulation :

```java
// Step 3: Create export options for the table
ExportTableOptions exportOptions = new ExportTableOptions();

// Step 4: Configure the options – export as plain text and use a tab delimiter
exportOptions.setExportAsString(true);   // Returns a string instead of binary Excel format
exportOptions.setDelimiter('\t');        // Tab character makes it TSV
```

> **Pourquoi utiliser `setExportAsString(true)` ?**  
> Cela indique à Aspose.Cells de traiter la sortie comme du texte brut, exactement ce dont vous avez besoin lorsque vous voulez **save Excel as TSV**. L’alternative serait une exportation CSV ou HTML, qui ne donnent pas une séparation nette par tabulations.

### Cas particulier : délimiteurs personnalisés
Si votre système en aval attend un pipe (`|`) au lieu d’une tabulation, changez simplement le délimiteur :

```java
exportOptions.setDelimiter('|');
```

---

## Étape 4 : Exportez la plage souhaitée vers un fichier texte

Nous écrivons maintenant le fichier TSV. La méthode `exportTable` prend trois arguments : la plage de cellules, le chemin de sortie, et les `ExportTableOptions` que nous venons de configurer.

```java
// Step 5: Export the range A1:D20 to a text file using the configured options
ws.getCells().exportTable("A1:D20", "YOUR_DIRECTORY/out.tsv", exportOptions);
System.out.println("TSV file created successfully!");
```

Si vous voulez exporter la *plage utilisée* entière, remplacez `"A1:D20"` par `ws.getCells().getMaxDisplayRange()` :

```java
String fullRange = ws.getCells().getMaxDisplayRange();
ws.getCells().exportTable(fullRange, "out.tsv", exportOptions);
```

### Astuce pro
Après l’exportation, vous pouvez également récupérer directement la chaîne :

```java
String tsvContent = ws.getCells().exportTable("A1:D20", exportOptions);
System.out.println(tsvContent); // Handy for debugging or sending over a network
```

Cela vous donne la **export Excel data string** brute sans toucher au système de fichiers.

---

## Étape 5 : Gestion des gros fichiers et conseils de performance

Lorsque vous traitez des feuilles de calcul massives (des centaines de milliers de lignes), envisagez ces optimisations :

| Problème | Solution |
|----------|----------|
| Pression mémoire | Utilisez `WorkbookFactory.create(InputStream)` pour diffuser le fichier au lieu de le charger entièrement. |
| I/O lent | Écrivez dans un `BufferedWriter` ou utilisez NIO `Files.newBufferedWriter`. |
| Caractères Unicode | Assurez‑vous que le fichier de sortie est écrit en UTF‑8 : `exportTable(..., "out.tsv", exportOptions, Encoding.getUTF8())`. |

Voici un extrait qui combine diffusion et encodage UTF‑8 :

```java
try (InputStream is = Files.newInputStream(Paths.get("input.xlsx"));
     BufferedWriter writer = Files.newBufferedWriter(Paths.get("out.tsv"), StandardCharsets.UTF_8)) {

    Workbook wb = new Workbook(is);
    Worksheet sheet = wb.getWorksheets().get(0);
    ExportTableOptions opts = new ExportTableOptions();
    opts.setExportAsString(true);
    opts.setDelimiter('\t');

    String tsv = sheet.getCells().exportTable("A1:D20", opts);
    writer.write(tsv);
}
```

---

## Pièges courants et comment les éviter

1. **Oubli de `setExportAsString(true)`.**  
   Sans ce drapeau, Aspose générera un fichier Excel binaire, ce qui compromet votre objectif **export worksheet to text**.

2. **Mauvais délimiteur.**  
   Une virgule au lieu d’une tabulation vous donnera un CSV, pas un TSV. Vérifiez bien `setDelimiter('\t')`.

3. **Syntaxe de plage incorrecte.**  
   `"A1:D20"` est correct, mais `"A1:D20:"` (deux‑points supplémentaire) déclenchera une `IllegalArgumentException`.  

4. **Permissions de fichier.**  
   Assurez‑vous que le répertoire cible est accessible en écriture. Sous Linux, `chmod 755` résout souvent le problème.

---

## Récapitulatif – Exemple complet fonctionnel

Voici le programme complet, prêt à être exécuté, qui montre **save Excel as TSV** de bout en bout :

```java
import com.aspose.cells.*;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.nio.file.*;

public class ExcelToTsv {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // Choose worksheet (first sheet in this case)
        Worksheet ws = workbook.getWorksheets().get(0);

        // Set up export options for plain‑text TSV output
        ExportTableOptions exportOptions = new ExportTableOptions();
        exportOptions.setExportAsString(true);   // Export as string
        exportOptions.setDelimiter('\t');        // Tab delimiter for TSV

        // Define the range you want to export
        String range = "A1:D20"; // Change as needed or use ws.getCells().getMaxDisplayRange()

        // Export to a file
        ws.getCells().exportTable(range, "YOUR_DIRECTORY/out.tsv", exportOptions);
        System.out.println("Successfully saved Excel as TSV at YOUR_DIRECTORY/out.tsv");
    }
}
```

L’exécution de ce programme produit un fichier à séparations par tabulations (`out.tsv`) que n’importe quel système en aval — chargeur de base de données, script Unix `awk`, ou simple visionneur de feuilles de calcul — peut consommer.

---

## Conclusion

Nous avons couvert tout ce qu’il faut savoir pour **save Excel as TSV** avec Java et Aspose.Cells. En partant du chargement du classeur, en sélectionnant la bonne feuille, en configurant `ExportTableOptions`, puis en écrivant le fichier, vous disposez maintenant d’un modèle solide et prêt pour la production pour les scénarios **export worksheet to text**, **export sheet plain text** et **export Excel data string**.

Et après ? Essayez d’exporter plusieurs plages, de changer les délimiteurs à la volée, ou de diffuser la sortie directement vers une réponse HTTP pour des téléchargements web. Les mêmes principes s’appliquent, et vous constaterez que manipuler les données Excel en texte brut devient un jeu d’enfant une fois les bases acquises.

Des questions ou un cas particulier qui vous pose problème ? Laissez un commentaire ci‑dessous, et bon codage !

## Que devez‑vous apprendre ensuite ?


Les tutoriels suivants abordent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Export Excel Data to HTML5 Using Aspose.Cells Java](/cells/english/java/import-export/aspose-cells-java-export-excel-html5/)
- [Effortless Data Export from Excel using Aspose.Cells for Java](/cells/english/java/import-export/aspose-cells-java-excel-data-export/)
- [How to Export an Excel Worksheet to PNG Using Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}