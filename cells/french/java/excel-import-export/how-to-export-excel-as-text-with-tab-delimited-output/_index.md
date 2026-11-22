---
category: general
date: 2026-11-22
description: Apprenez à exporter Excel en texte et à créer un fichier délimité par
  des tabulations. Ce guide montre comment activer l’option de mettre des guillemets
  autour de tous les champs et enregistrer le texte du tableau efficacement.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as text
- quote all fields
- create tab-delimited file
- save spreadsheet text
- export spreadsheet tab-delimited
language: fr
lastmod: 2026-11-22
og_description: Exportez Excel en texte et créez un fichier à délimitation par tabulations.
  Suivez ce tutoriel étape par étape pour mettre entre guillemets tous les champs
  et enregistrer le texte du tableau avec Java.
og_image_alt: Screenshot showing Java code that exports an Excel workbook as a tab‑delimited
  text file
og_title: Exporter Excel en texte – guide du fichier à délimitation par tabulation
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  headline: How to export Excel as text with tab‑delimited output
  type: TechArticle
- description: Learn how to export Excel as text and create a tab‑delimited file.
    This guide shows setting quote all fields and saving spreadsheet text efficiently.
  name: How to export Excel as text with tab‑delimited output
  steps:
  - name: Prepare the workbook and sample data
    text: Creating a workbook gives you something to export. In a real project you
      would load an existing file with `new Workbook("input.xlsx")`; here we generate
      a tiny sheet so the example runs out‑of‑the‑box.
  - name: Configure export options – delimiter, quoting, and output mode
    text: The core of **export spreadsheet tab‑delimited** lies in `ExportTableOptions`.
      You set the delimiter to a tab (`'\t'`) and enable `setQuoteAllFields(true)`
      so every cell is wrapped in double quotes. This eliminates ambiguity when a
      cell itself contains a tab or newline.
  - name: Save the workbook as a tab‑delimited text file
    text: Now you actually **export excel as text**. The `save` method takes the target
      path and the `ExportOptions` you configured.
  type: HowTo
tags:
- export excel as text
- quote all fields
- tab-delimited file
- spreadsheet export
- Java
title: Comment exporter Excel en texte avec une sortie délimitée par des tabulations
url: /fr/java/excel-import-export/how-to-export-excel-as-text-with-tab-delimited-output/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exporter Excel en texte avec une sortie à délimitation par tabulation

Si vous devez **exporter Excel en texte**, ce tutoriel vous guide à travers le processus complet de création d'un fichier à délimitation par tabulation à partir d'un classeur. Que vous construisiez un pipeline de migration de données ou que vous ayez besoin d'un export rapide de type CSV pour le traitement en aval, les étapes ci‑dessous vous permettent de **sauvegarder le texte d'une feuille de calcul** avec un contrôle total sur les délimiteurs et le quoting.

Exporter les données d'une feuille de calcul en texte brut est souvent plus portable que de conserver le format natif `.xlsx`. Dans ce guide, vous apprendrez également à **quote all fields**, ce qui garantit que les valeurs contenant des tabulations, des virgules ou des sauts de ligne sont correctement encapsulées.

## Ce dont vous aurez besoin

* Java 17 ou une version ultérieure installée.
* La bibliothèque Aspose.Cells for Java (le code utilise `ExportOptions` et `ExportTableOptions` de cette bibliothèque). Vous pouvez l'ajouter via Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version>
</dependency>
```

* Un IDE ou un éditeur de texte simple pour compiler et exécuter le programme Java.

## Exporter Excel en texte – étape par étape

Les sections suivantes divisent la tâche en trois étapes logiques. Chaque étape explique **pourquoi** elle est importante, pas seulement **quoi** taper.

### Étape 1 : Préparer le classeur et les données d'exemple

Créer un classeur vous fournit quelque chose à exporter. Dans un projet réel, vous chargeriez un fichier existant avec `new Workbook("input.xlsx")` ; ici nous générons une petite feuille afin que l'exemple fonctionne immédiatement.

```java
import com.aspose.cells.*;

public class ExportExcelAsText {
    public static void main(String[] args) throws Exception {
        // Load an existing workbook or create a new one
        Workbook wb = new Workbook();
        Worksheet sheet = wb.getWorksheets().get(0);

        // Populate sample data – this will be part of the exported text
        sheet.getCells().get("A1").setValue("Name");
        sheet.getCells().get("B1").setValue("Age");
        sheet.getCells().get("A2").setValue("Alice");
        sheet.getCells().get("B2").setValue(30);
        sheet.getCells().get("A3").setValue("Bob, Jr."); // contains a comma
        sheet.getCells().get("B3").setValue(25);
```

*Pourquoi cette étape ?*  
Un classeur est l'objet source pour toute opération d'exportation. En ajoutant quelques lignes, vous pouvez vérifier que l'option **quote all fields** protège réellement les virgules et autres caractères spéciaux.

### Étape 2 : Configurer les options d'exportation – délimiteur, quoting et mode de sortie

Le cœur de **export spreadsheet tab‑delimited** réside dans `ExportTableOptions`. Vous définissez le délimiteur sur une tabulation (`'\t'`) et activez `setQuoteAllFields(true)` afin que chaque cellule soit entourée de guillemets doubles. Cela élimine toute ambiguïté lorsqu'une cellule contient elle‑même une tabulation ou un saut de ligne.

```java
        // Step 2: Create table export options and configure delimiter and quoting
        ExportTableOptions tableExportOptions = new ExportTableOptions();
        tableExportOptions.setDelimiter('\t');            // Use a tab as the field separator
        tableExportOptions.setQuoteAllFields(true);      // Quote every field for safety

        // Create overall export options and attach the table options
        ExportOptions exportOptions = new ExportOptions();
        exportOptions.setExportTableOptions(tableExportOptions);
        exportOptions.setExportAsString(true);            // Produce plain‑text output
```

*Pourquoi cette étape ?*  
- **Delimiter** détermine comment les colonnes sont séparées. Une tabulation (`\t`) crée un **fichier à délimitation par tabulation** accepté par de nombreux outils de traitement de données.  
- **Quote all fields** garantit que même si une cellule contient un délimiteur, le texte résultant reste analysable.  
- Le paramètre `ExportAsString` indique à Aspose.Cells de générer une chaîne plutôt qu'un classeur binaire, ce qui est exactement ce dont vous avez besoin pour **save spreadsheet text**.

### Étape 3 : Enregistrer le classeur en tant que fichier texte à délimitation par tabulation

Vous **exportez maintenant Excel en texte**. La méthode `save` prend le chemin cible et les `ExportOptions` que vous avez configurés.

```java
        // Step 3: Save the workbook as a tab‑delimited text file
        wb.save("output/table.txt", exportOptions);
    }
}
```

Lorsque le programme se termine, vous trouverez `output/table.txt` contenant :

```
"Name"	"Age"
"Alice"	"30"
"Bob, Jr."	"25"
```

*Pourquoi cette étape ?*  
L'appel `save` écrit le **fichier à délimitation par tabulation** sur le disque, sauvegardant efficacement **spreadsheet text** dans un format qui peut être ouvert par Excel, Notepad ou tout outil d'importation de données qui comprend les tabulations.

## Comment citer tous les champs lors de l'exportation d'Excel en texte

Si vous omettez `setQuoteAllFields(true)`, les cellules contenant des tabulations, des virgules ou des sauts de ligne casseront la structure du fichier de sortie. Par exemple, la ligne `Bob, Jr.` serait divisée en deux colonnes, corrompant le jeu de données. Activez toujours le quoting lorsque :

* Vos données sources peuvent contenir des virgules, des tabulations ou des sauts de ligne.
* Les analyseurs en aval attendent des fichiers CSV/TSV cités.
* Vous avez besoin d'une exportation déterministe quel que soit le contenu des cellules.

## Créer un fichier à délimitation par tabulation sans Aspose.Cells (optionnel)

Si vous préférez une solution pure Java sans bibliothèques tierces, vous pouvez parcourir les lignes et les écrire manuellement :

```java
try (PrintWriter pw = new PrintWriter(new FileWriter("output/manual.txt"))) {
    for (int r = 0; r < sheet.getCells().getMaxDataRow() + 1; r++) {
        List<String> rowValues = new ArrayList<>();
        for (int c = 0; c < sheet.getCells().getMaxDataColumn() + 1; c++) {
            String value = sheet.getCells().get(r, c).getStringValue();
            // Quote all fields manually
            rowValues.add('"' + value.replace("\"", "\"\"") + '"');
        }
        pw.println(String.join("\t", rowValues));
    }
}
```

Cet extrait montre la même logique de **export spreadsheet tab‑delimited** : un délimiteur tabulation, le quoting de chaque champ, et l'écriture du résultat en texte brut. Cependant, l'utilisation d'Aspose.Cells simplifie la gestion de grands classeurs, préserve le formatage et réduit le code boilerplate.

## Pièges courants et astuces professionnelles

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Tabulations manquantes dans la sortie** | Le délimiteur est resté à la virgule par défaut. | Appelez explicitement `setDelimiter('\t')`. |
| **Les virgules non citées cassent les colonnes** | `quoteAllFields` n'est pas activé. | Utilisez `setQuoteAllFields(true)` ou citez manuellement. |
| **Fichier non créé** | Le répertoire de sortie n'existe pas. | Assurez‑vous que le dossier `output/` existe ou utilisez `Files.createDirectories`. |
| **Problèmes d'encodage** | L'encodage par défaut de la plateforme peut corrompre les caractères non ASCII. | Passez `ExportOptions.setEncoding(Encoding.getUTF8())` si nécessaire. |

## Tester le résultat

Après avoir exécuté le programme :

1. Ouvrez `output/table.txt` dans un éditeur de texte brut. Vous devriez voir chaque valeur entourée de guillemets doubles et les colonnes séparées par un seul caractère de tabulation.  
2. Importez le fichier dans Excel (`Données → À partir du texte/CSV`). Choisissez **Tab** comme délimiteur ; Excel placera correctement chaque valeur citée dans sa propre cellule.  
3. Vérifiez que les caractères spéciaux (virgules, sauts de ligne

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [comment exporter excel – Guide du texte à tabulation](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-tab-delimited-text-guide/)
- [Enregistrer Excel en fichier texte avec séparateur personnalisé utilisant Aspose.Cells](/cells/english/net/workbook-operations/save-excel-text-custom-separator-aspose-cells-net/)
- [Comment enregistrer Excel en texte avec Aspose.Cells – guide étape par étape](/cells/english/net/converting-excel-files-to-other-formats/how-to-save-excel-as-text-with-aspose-cells-step-by-step-gui/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}