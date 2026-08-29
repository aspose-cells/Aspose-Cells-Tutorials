---
category: general
date: 2026-07-16
description: Définir un séparateur de cellules personnalisé lors de l'exportation
  d'un tableau Excel vers TXT avec Aspose.Cells. Apprenez comment exporter les formules
  Excel en texte et enregistrer la feuille de calcul au format txt.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- set custom cell separator
- export excel table to txt
- export excel formulas to text
- save worksheet as txt file
- export excel data as plain text
language: fr
lastmod: 2026-07-16
og_description: Définir un séparateur de cellules personnalisé dans Aspose.Cells vous
  permet d'exporter un tableau Excel au format TXT avec un formatage exact. Exportez
  les formules Excel en texte et enregistrez facilement la feuille de calcul au format
  TXT.
og_image_alt: Screenshot showing set custom cell separator option in Aspose.Cells
  export settings
og_title: Définir un séparateur de cellules personnalisé – Exporter le tableau Excel
  en TXT
schemas:
- author: Aspose
  dateModified: '2026-07-16'
  description: Set custom cell separator when exporting Excel table to TXT using Aspose.Cells.
    Learn how to export Excel formulas to text and save worksheet as txt file.
  headline: Set Custom Cell Separator – Export Excel Table to TXT
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel Export
title: Définir un séparateur de cellules personnalisé – Exporter le tableau Excel
  en TXT
url: /fr/java/excel-import-export/set-custom-cell-separator-export-excel-table-to-txt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définir un séparateur de cellule personnalisé – Exporter un tableau Excel en TXT

Définir un séparateur de cellule personnalisé est la sauce secrète dont vous avez besoin lorsque vous voulez obtenir un dump texte propre à partir d’une feuille Excel. Vous êtes-vous déjà demandé comment **exporter excel table to txt** sans vous retrouver avec un fouillis de virgules et de sauts de ligne ? Dans ce tutoriel, nous parcourrons l’ensemble du processus avec Aspose.Cells for Java, du chargement d’un classeur à **save worksheet as txt file** avec le délimiteur de votre choix.

## Ce que vous allez apprendre

- Comment **set custom cell separator** pour les exportations texte.
- Les étapes exactes pour **export excel formulas to text** afin que les valeurs évaluées vous accompagnent.
- Les différentes manières d’**export excel data as plain text** tout en conservant la mise en page.
- Un exemple de code complet, prêt à être copié‑collé dans votre projet.

À la fin de ce guide, vous pourrez prendre n’importe quel classeur Excel, choisir un pipe (`|`), une tabulation (`\t`) ou tout autre caractère, et produire un fichier texte délimité propre que les systèmes en aval adoreront.

### Prérequis

- Java 8 ou version supérieure installé.
- Maven (ou tout autre outil de construction) pour récupérer la bibliothèque Aspose.Cells for Java.
- Un classeur d’exemple (`TableDemo.xlsx`) contenant un tableau avec des formules.

Si vous avez tout cela, plongeons‑y—pas de blabla supplémentaire, juste des étapes pratiques.

## Étape 1 : Ajouter Aspose.Cells à votre projet

Avant de pouvoir **set custom cell separator**, vous devez placer le JAR Aspose.Cells sur le classpath. La façon la plus simple est via Maven :

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Si vous préférez Gradle, remplacez le XML par l’équivalent `implementation 'com.aspose:aspose-cells:24.10'`. Une fois la dépendance résolue, vous êtes prêt à écrire du code Java qui interagit avec les fichiers Excel.

## Étape 2 : Charger le classeur – Préparer l’exportation du tableau Excel en TXT

La première vraie ligne de code est toujours la même : ouvrir le classeur qui contient le tableau que vous souhaitez exporter.

```java
import com.aspose.cells.*;

public class ExportTableWithOptions {
    public static void main(String[] args) throws Exception {
        // Load the workbook containing the table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/TableDemo.xlsx");
        Worksheet worksheet = workbook.getWorksheets().get(0);
```

Ici nous récupérons la première feuille (`get(0)`). Si vos données se trouvent sur une autre feuille, changez simplement l’indice ou utilisez `get("SheetName")`. Cette partie est essentielle pour **export excel table to txt** car l’exportateur travaille au niveau de la feuille.

## Étape 3 : Définir le séparateur de cellule personnalisé – Le cœur de l’exportation

Voici la star du spectacle : configurer `ExportTableOptions`. Cet objet vous permet de décider exactement comment chaque cellule apparaît dans le fichier texte final.

```java
        // Define how the table should be exported
        ExportTableOptions exportTableOptions = new ExportTableOptions();

        // 1️⃣ Export cell contents as plain strings (no rich formatting)
        exportTableOptions.setExportAsString(true);

        // 2️⃣ Include the evaluated formula result, not the formula itself
        exportTableOptions.setFormulaValueInCell(true);

        // 3️⃣ Set the custom separator – this is where we set custom cell separator
        exportTableOptions.setCellValueSeparator("|"); // you can use any char you like
```

Pourquoi **set custom cell separator** ? Parce que le séparateur par défaut est une tabulation, ce qui peut entrer en conflit avec des données contenant déjà des tabulations. En choisissant un pipe (`|`) ou un point‑virgule, vous garantissez que chaque colonne reste distincte lorsqu’un analyseur en aval lit le fichier.

### Exporter les formules Excel en texte

La ligne `setFormulaValueInCell(true)` indique à Aspose.Cells d’écrire les **export excel formulas to text** sous forme de *résultat* de la formule, et non la chaîne de la formule elle‑même. Si vous omettez cela, une cellule contenant `=SUM(A1:A5)` apparaîtrait comme `=SUM(A1:A5)` dans le TXT, ce qui est rarement souhaité.

## Étape 4 : Attacher les options d’exportation aux options de sauvegarde TXT

Nous associons maintenant ces options de tableau à la configuration globale d’exportation TXT.

```java
        // Attach the table export options to TXT save options
        TxtSaveOptions txtSaveOptions = new TxtSaveOptions();
        txtSaveOptions.setExportTableOptions(exportTableOptions);
```

`TxtSaveOptions` est l’objet qui contrôle la façon dont toute la feuille est écrite. En branchant `exportTableOptions` dedans, vous vous assurez que chaque tableau de la feuille respecte la règle **set custom cell separator**.

## Étape 5 : Enregistrer la feuille en fichier TXT – Finaliser l’exportation

Enfin, nous écrivons le fichier sur le disque.

```java
        // Save the worksheet as a TXT file using the configured options
        workbook.save("YOUR_DIRECTORY/TableExported.txt", txtSaveOptions);
    }
}
```

L’exécution de ce programme crée `TableExported.txt`. Chaque ligne du tableau Excel original apparaîtra maintenant comme une ligne de valeurs séparées par des pipes, par exemple :

```
Name|Quantity|Price|Total
Apple|10|0.50|5.00
Banana|5|0.30|1.50
```

Remarquez comment la formule de la colonne **Total** a été évaluée avant d’être écrite—grâce à `setFormulaValueInCell(true)`. C’est l’essence de **export excel data as plain text** tout en conservant les résultats calculés.

## Étape 6 : Vérifier la sortie – Est‑ce correct ?

Ouvrez le `TableExported.txt` généré dans n’importe quel éditeur de texte. Vous devriez voir :

- Une ligne par ligne Excel.
- Des colonnes séparées par le caractère pipe que vous avez défini avec `setCellValueSeparator`.
- Aucun virgule ou tabulation parasite, sauf si elles faisaient partie des valeurs de cellules d’origine.
- Les résultats des formules, et non les formules elles‑elles.

Si vous repérez des caractères inattendus, revérifiez le séparateur choisi. Certains caractères (comme le pipe) sont sûrs pour la plupart des analyseurs de type CSV, mais si vos données contiennent déjà des pipes, envisagez un délimiteur différent tel que `~` ou une tabulation (`\t`).

## Astuces, cas limites et bonnes pratiques – Exporter les données Excel en texte brut

| Situation | What to Do |
|-----------|------------|
| **Data already contains your chosen separator** | Switch to a less common character (`^`, `~`, or Unicode non‑printing chars). |
| **You need UTF‑8 encoding** |  |

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Save Excel as Text File with Custom Separator using Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Save Excel Text Custom Separator Aspose Cells Net](/cells/german/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Save Excel Text Custom Separator Aspose Cells Net](/cells/french/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}