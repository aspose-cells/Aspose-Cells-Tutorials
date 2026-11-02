---
category: general
date: 2026-08-14
description: Intégrer les polices dans le SVG lors de l'exportation d'Excel vers SVG
  avec Aspose.Cells. Apprenez comment définir la zone d’impression, définir les options
  d’impression et utiliser la fonction WRAPCOLS.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- embed fonts in svg
- export excel to svg
- set print area
- set print options
- use wrapcols function
language: fr
lastmod: 2026-08-14
og_description: Intégrer les polices dans le SVG lors de l'exportation d'Excel vers
  SVG avec Aspose.Cells. Ce guide vous montre comment définir la zone d’impression,
  configurer les options d’impression et appliquer la fonction WRAPCOLS.
og_image_alt: Screenshot of Java code exporting an Excel sheet to SVG with embedded
  fonts
og_title: Intégrer les polices dans le SVG lors de l’exportation d’Excel vers SVG
  – étape par étape
schemas:
- author: Aspose
  dateModified: '2026-08-14'
  description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  headline: Embed fonts in SVG while exporting Excel to SVG
  type: TechArticle
- description: Embed fonts in SVG while exporting Excel to SVG using Aspose.Cells.
    Learn how to set print area, set print options, and use WRAPCOLS function.
  name: Embed fonts in SVG while exporting Excel to SVG
  steps:
  - name: Run the program.
    text: Run the program.
  - name: Open `output.svg` in a web browser.
    text: Open `output.svg` in a web browser.
  - name: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
    text: Confirm that the text uses the same typeface as the original Excel file
      (fonts are embedded).
  - name: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
    text: Verify that only the cells within `A1:H30` appear and that the data from
      `A2:A10` is displayed in three columns.
  type: HowTo
tags:
- Aspose.Cells
- Java
- SVG
title: Intégrer les polices dans le SVG lors de l'exportation d'Excel vers SVG
url: /fr/java/excel-import-export/embed-fonts-in-svg-while-exporting-excel-to-svg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Intégrer les polices dans SVG lors de l'exportation d'Excel vers SVG

Si vous devez **intégrer les polices dans SVG lors de l'exportation d'Excel vers SVG**, ce tutoriel vous montre exactement comment le faire avec Aspose.Cells for Java. Nous couvrirons également comment **définir la zone d'impression**, **configurer les options d'impression**, et **utiliser la fonction WRAPCOLS** pour formater les données sans perdre la mise en page.

Vous suivrez un exemple complet et exécutable qui charge un classeur existant, applique la formule `WRAPCOLS`, configure les options d'image spécifiques à SVG, définit la région d'impression, puis enregistre le fichier au format SVG avec les polices intégrées. Aucune documentation externe n'est requise — copiez simplement le code, exécutez‑le et inspectez le SVG résultant.

## Intégrer les polices dans SVG – configuration de ImageOrPrintOptions

L’intégration des polices garantit que le SVG s’affiche exactement comme dans Excel, même sur des machines qui n’ont pas les polices d’origine installées.

```java
// Create ImageOrPrintOptions for SVG output
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);          // Target format
imgOptions.setEmbedFonts(true);                     // <-- embed fonts in SVG
imgOptions.setFontVariationSelectors(true);        // Preserve variation selectors
```

*Pourquoi c’est important* : lorsque `setEmbedFonts(true)` est activé, Aspose.Cells écrit les données de police directement dans la section `<defs>` du SVG. Le résultat est un fichier autonome qui apparaît identique sur tous les navigateurs et plateformes.

## Exporter Excel vers SVG – flux de travail complet

Les étapes suivantes illustrent le processus de bout en bout, du chargement du classeur à l’enregistrement du fichier SVG.

```java
// Step 1: Load a workbook and access the first worksheet
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
Worksheet ws = workbook.getWorksheets().get(0);

// Step 2: Apply the WRAPCOLS formula to cell A1
Cell cell = ws.getCells().get("A1");
cell.setFormula("=WRAPCOLS(A2:A10,3)");

// Step 3: Configure image options (see previous section)
ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
imgOptions.setImageFormat(ImageFormat.SVG);
imgOptions.setEmbedFonts(true);
imgOptions.setFontVariationSelectors(true);

// Step 4: Define the print area and assign the image options
ws.getPageSetup().setPrintArea("A1:H30");           // <-- set print area
ws.getPageSetup().setPrintOptions(imgOptions);     // <-- set print options

// Step 5: Save the worksheet as an SVG file
ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);
```

**Résultat attendu** : `output.svg` apparaît dans `YOUR_DIRECTORY`. L’ouvrir dans un navigateur montre la feuille de calcul avec toutes les polices intégrées, les données réparties sur trois colonnes (grâce à `WRAPCOLS`), et seules les cellules situées dans `A1:H30` sont rendues.

## Définir la zone d’impression pour la feuille de calcul

Définir une zone d’impression limite le SVG exporté à une plage spécifique, ce qui réduit la taille du fichier et concentre le visualiseur sur les données pertinentes.

```java
// Define a rectangular region that will be exported
ws.getPageSetup().setPrintArea("A1:H30");   // you can change the range as needed
```

*Astuce* : la plage suit la notation A1 d’Excel. Si vous avez besoin d’une plage dynamique, vous pouvez la calculer programmatiquement avec `ws.getCells().getMaxDisplayRange()`.

## Configurer les options d’impression pour la sortie SVG

Les options d’impression contrôlent la façon dont Aspose.Cells traduit la feuille de calcul en image. En plus d’intégrer les polices, vous pouvez ajuster la résolution, le redimensionnement et la mise en page.

```java
// Assign the previously configured ImageOrPrintOptions
ws.getPageSetup().setPrintOptions(imgOptions);
```

*Pourquoi vous devez définir les options d’impression* : sans options explicites, Aspose.Cells utilise les valeurs par défaut qui peuvent omettre l’intégration des polices ou appliquer un facteur de mise à l’échelle indésirable, entraînant des SVG flous ou mal stylisés.

## Utiliser la fonction WRAPCOLS pour envelopper les données de colonne

`WRAPCOLS` est une formule Excel qui répartit une plage verticale en un nombre spécifié de colonnes. Elle est pratique lorsque vous souhaitez afficher une longue liste dans une grille compacte.

```java
// Insert the WRAPCOLS formula into cell A1
cell.setFormula("=WRAPCOLS(A2:A10,3)");
```

Lorsque le classeur est enregistré, Aspose.Cells évalue la formule, produisant une mise en page à trois colonnes à l’intérieur de la zone d’impression définie. Cette technique fonctionne pour toute plage de taille — il suffit d’ajuster le deuxième argument au nombre de colonnes souhaité.

## Exemple complet et exécutable

Voici le programme Java complet que vous pouvez coller dans n’importe quel IDE. Assurez‑vous que la bibliothèque Aspose.Cells for Java se trouve sur votre classpath.

```java
import com.aspose.cells.*;

public class ExportExcelToSvg {
    public static void main(String[] args) throws Exception {
        // Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
        Worksheet ws = workbook.getWorksheets().get(0);

        // Apply WRAPCOLS to reorganize data
        Cell wrapCell = ws.getCells().get("A1");
        wrapCell.setFormula("=WRAPCOLS(A2:A10,3)");

        // Configure SVG options with embedded fonts
        ImageOrPrintOptions imgOptions = new ImageOrPrintOptions();
        imgOptions.setImageFormat(ImageFormat.SVG);
        imgOptions.setEmbedFonts(true);
        imgOptions.setFontVariationSelectors(true);

        // Set the region that will appear in the SVG
        ws.getPageSetup().setPrintArea("A1:H30");

        // Attach the image options to the worksheet
        ws.getPageSetup().setPrintOptions(imgOptions);

        // Export the worksheet as an SVG file
        ws.getPageSetup().save("YOUR_DIRECTORY/output.svg", SaveFormat.SVG);

        System.out.println("SVG exported successfully with embedded fonts.");
    }
}
```

**Étapes de vérification**

1. Exécutez le programme.  
2. Ouvrez `output.svg` dans un navigateur web.  
3. Confirmez que le texte utilise la même police que le fichier Excel original (polices intégrées).  
4. Vérifiez que seules les cellules comprises entre `A1:H30` apparaissent et que les données de `A2:A10` sont affichées en trois colonnes.

## Problèmes courants et comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| Les polices sont absentes dans le SVG | `setEmbedFonts(false)` ou le fichier de police n’est pas accessible | Assurez‑vous que `setEmbedFonts(true)` est activé et que la police est installée sur la machine exécutant le code |
| WRAPCOLS ne s’évalue pas | Moteur de calcul désactivé | Appelez `workbook.calculateFormula()` avant l’exportation, ou laissez Aspose.Cells évaluer lors de l’enregistrement |
| Le SVG exporté est vide | La zone d’impression ne comprend aucune donnée | Revérifiez la plage passée à `setPrintArea` |
| Le fichier SVG est volumineux | Aucun redimensionnement appliqué, résolution d’image élevée | Ajustez `imgOptions.setResolution(96)` ou une valeur similaire pour contrôler le DPI |

## Astuce pro : réutiliser ImageOrPrintOptions pour plusieurs feuilles

Si votre classeur contient plusieurs feuilles qui nécessitent les mêmes paramètres SVG, créez une seule instance de `ImageOrPrintOptions` et affectez‑la à chaque `PageSetup` de feuille. Cela réduit la consommation de mémoire et garantit une intégration cohérente des polices dans tous les fichiers exportés.

```java
ImageOrPrintOptions sharedOptions = new ImageOrPrintOptions();
sharedOptions.setImageFormat(ImageFormat.SVG);
sharedOptions.setEmbedFonts(true);
sharedOptions.setFontVariationSelectors(true);

for (int i = 0; i < workbook.getWorksheets().getCount(); i++) {
    Worksheet sheet = workbook.getWorksheets().get(i);
    sheet.getPageSetup().setPrintOptions(sharedOptions);
    sheet.getPageSetup().setPrintArea("A1:H30");
    sheet.getPageSetup().save("YOUR_DIRECTORY/sheet" + i + ".svg", SaveFormat.SVG);
}
```

## Prochaines étapes

* **Exporter vers d’autres formats vectoriels** – Remplacez `ImageFormat.SVG` par `ImageFormat.PDF` pour obtenir des PDF de haute qualité.  
* **Traitement par lots** – Parcourez un dossier de fichiers `.xlsx` et générez automatiquement les SVG.  
* **Gestion personnalisée des polices** – Utilisez `FontSettings` pour charger des polices depuis un répertoire spécifique lorsque les polices système sont insuffisantes.  

En maîtrisant **embed fonts in SVG**, **export excel to svg**, **set print area**, **set print options**, et **use WRAPCOLS function**, vous pouvez automatiser la génération de SVG haute fidélité pour des rapports, tableaux de bord et visualisations web directement à partir des données Excel. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques présentées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [How to Set a Print Area in Excel Using Aspose.Cells for .NET](/cells/english/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/german/net/headers-footers/set-print-area-excel-aspose-cells-net/)
- [Set Print Area Excel Aspose Cells Net](/cells/french/net/headers-footers/set-print-area-excel-aspose-cells-net/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}