---
category: general
date: 2026-03-01
description: Copier un tableau croisé dynamique en Java tout en préservant le pivot,
  puis exporter Excel en PPTX, désactiver le filtre automatique d’Excel et utiliser
  Smart Marker pour les tableaux JSON – guide complet étape par étape.
draft: false
keywords:
- copy pivot table
- preserve pivot table
- use smart marker
- disable excel autofilter
- export excel to pptx
language: fr
og_description: Copier un tableau croisé dynamique en Java, conserver la définition
  du tableau croisé, exporter en PPTX, désactiver l’AutoFilter et utiliser Smart Marker
  – guide complet pour les développeurs.
og_title: Copier le tableau croisé dynamique en Java – le conserver, l'exporter en
  PPTX
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Copier le tableau croisé dynamique en Java – le préserver, l’exporter en PPTX
url: /fr/java/excel-pivot-tables/copy-pivot-table-in-java-preserve-it-export-to-pptx/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Copier un tableau croisé dynamique en Java – le préserver, l'exporter en PPTX

Vous avez déjà eu besoin de **copier un tableau croisé dynamique** d’un classeur à un autre sans perdre la définition sous‑jacente du tableau croisé dynamique ? Vous n'êtes pas le seul à vous creuser la tête à ce sujet. Dans de nombreux projets réels, vous vous retrouverez à déplacer des données, et la dernière chose que vous voulez est un tableau croisé dynamique cassé qui génère des erreurs à l’exécution.  

Dans ce tutoriel, nous parcourrons une solution complète qui non seulement **copie un tableau croisé dynamique**, mais vous montre également comment **préserver le tableau croisé dynamique** lors de la copie, **exporter Excel vers PPTX**, **désactiver le filtre automatique d’Excel**, et **utiliser les smart markers** pour insérer un tableau JSON dans une seule cellule. À la fin, vous disposerez d’un programme Java unique et exécutable couvrant les quatre scénarios.

## Prérequis

- Java 8 ou plus récent (le code fonctionne également avec Java 11)  
- Bibliothèque Aspose.Cells for Java (version 23.9 ou ultérieure) – vous pouvez la récupérer depuis Maven Central  
- Familiarité de base avec les concepts Excel tels que les tableaux croisés dynamiques, les tables et les zones de texte  

Si le JAR Aspose.Cells vous manque, ajoutez ceci à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

Maintenant, plongeons‑y.

## Étape 1 : Copier le tableau croisé dynamique – préserver la définition du tableau croisé dynamique

Lorsque vous copiez simplement la plage de cellules qui contient un tableau croisé dynamique, les métadonnées du tableau sont souvent laissées de côté. Aspose.Cells nous offre une méthode pratique pour conserver la définition intacte en utilisant `copyRange` avec une instance de `CopyOptions`.

```java
import com.aspose.cells.*;

public class PivotCopyDemo {

    public static void main(String[] args) throws Exception {
        // 1️⃣ Load the source workbook that contains the pivot table
        Workbook sourceWorkbook = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet sourceSheet = sourceWorkbook.getWorksheets().get(0);

        // 2️⃣ Define the range that includes the pivot (A1:G20 is just an example)
        Range pivotRange = sourceSheet.getCells().createRange("A1:G20");

        // 3️⃣ Prepare the destination workbook
        Workbook destWorkbook = new Workbook();
        Worksheet destSheet = destWorkbook.getWorksheets().get(0);

        // 4️⃣ Copy the range – the pivot definition travels with it
        destSheet.getCells().copyRange(pivotRange,
                new CellArea(0, 0, 19, 6), // destination area (rows 0‑19, cols 0‑6)
                new CopyOptions());

        // 5️⃣ Save the result
        destWorkbook.save("YOUR_DIRECTORY/dest.xlsx");
    }
}
```

**Pourquoi cela fonctionne :** `CopyOptions` indique à Aspose.Cells de transférer tout, y compris le cache du tableau croisé dynamique et les paramètres de champ. Sans cela, vous vous retrouverez avec des valeurs simples et perdrez la capacité de rafraîchir le tableau croisé dynamique.

**Cas particulier :** Si votre tableau croisé dynamique source s’étend au‑delà de la plage codée en dur `A1:G20`, ajustez la plage en conséquence ou utilisez `sourceSheet.getPivotTables().get(0).getDataRange()` pour la récupérer dynamiquement.

![Exemple de copie de tableau croisé dynamique](image.png "Copier un tableau croisé dynamique en Java")

*Texte alternatif de l’image : diagramme de copie de tableau croisé dynamique en Java*

## Étape 2 : Exporter une feuille de calcul avec une zone de texte éditable vers PPTX

Il arrive souvent que vous deviez transformer une feuille Excel en diapositive PowerPoint—pensez aux tableaux de bord hebdomadaires à présenter. Aspose.Cells peut enregistrer directement une feuille de calcul au format PPTX tout en préservant les formes telles que les zones de texte.

```java
import com.aspose.cells.*;

public class ExportToPptxDemo {

    public static void main(String[] args) throws Exception {
        // Load workbook that contains a TextBox shape
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Export the first worksheet to PPTX
        wb.save("YOUR_DIRECTORY/output.pptx", SaveFormat.PPTX);

        System.out.println("Worksheet exported to PPTX successfully.");
    }
}
```

**Ce qui se passe :** La méthode `save` avec `SaveFormat.PPTX` convertit toute la feuille, y compris toute zone de texte éditable, en une diapositive PowerPoint. Le texte à l’intérieur de la zone reste éditable lorsque vous ouvrez le PPTX dans PowerPoint.

**Astuce :** Si vous avez plusieurs feuilles et que vous ne voulez qu’une feuille spécifique, appelez `wb.getWorksheets().removeAt(index)` pour les autres avant d’enregistrer.

## Étape 3 : Désactiver le filtre automatique d’Excel d’une table

Le filtre automatique est pratique pour les utilisateurs finaux, mais il faut parfois le désactiver par programme—peut‑être avant d’exporter des données ou lors de la génération d’un rapport propre. Voici comment **désactiver le filtre automatique d’Excel** sur une table Excel.

```java
import com.aspose.cells.*;

public class DisableAutoFilterDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");
        Worksheet sheet = wb.getWorksheets().get(0);

        // Assume the first table in the sheet is the target
        Table table = sheet.getTables().get(0);

        // Turn off the AutoFilter arrows
        table.setShowAutoFilter(false);

        // Save the modified workbook
        wb.save("YOUR_DIRECTORY/noFilter.xlsx");
        System.out.println("AutoFilter disabled and workbook saved.");
    }
}
```

**Pourquoi cela peut être nécessaire :** L’exportation vers des formats qui ne prennent pas en charge le filtre automatique (comme CSV ou PDF) peut faire apparaître des icônes de filtre parasites. Le désactiver garantit une sortie propre.

**Erreur fréquente :** Si la feuille ne contient aucune table, `getTables().get(0)` lèvera une `IndexOutOfBoundsException`. Vérifiez toujours d’abord `sheet.getTables().size()` dans le code de production.

## Étape 4 : Utiliser Smart Marker – Insérer un tableau JSON comme valeur d’une seule cellule

Smart Marker est le moteur de templating d’Aspose. Une astuce pratique consiste à traiter un tableau JSON complet comme valeur d’une seule cellule, ce qui est parfait pour la journalisation ou le passage de données structurées en aval. Utilisons **Smart Marker** pour y parvenir.

```java
import com.aspose.cells.*;

public class SmartMarkerDemo {

    public static void main(String[] args) throws Exception {
        Workbook wb = new Workbook("YOUR_DIRECTORY/textbox.xlsx");

        // Initialise the SmartMarker processor with the workbook
        SmartMarkerProcessor processor = new SmartMarkerProcessor(wb);

        // JSON array we want to embed
        String jsonArray = "[{\"Name\":\"John\",\"Age\":30},{\"Name\":\"Anna\",\"Age\":28}]";

        // Configure the processor to treat arrays as a single cell
        processor.setOptions(SmartMarkerOptions.ArrayAsSingle);

        // Apply the marker – assume cell A1 contains the marker ${json}
        processor.apply(jsonArray);

        // Save the result
        wb.save("YOUR_DIRECTORY/smartMarkerResult.xlsx");
        System.out.println("JSON array inserted via Smart Marker.");
    }
}
```

**Comment cela fonctionne :** Le marqueur `${json}` dans le classeur est remplacé par la chaîne JSON complète car nous avons défini `ArrayAsSingle`. Sans cette option, Aspose tenterait d’étendre chaque élément du tableau en lignes séparées.

**Variation :** Si vous avez besoin que le tableau soit réparti sur plusieurs lignes, omettez simplement `ArrayAsSingle` et laissez Smart Marker gérer automatiquement l’expansion.

## Exemple complet fonctionnel – Toutes les étapes combinées

Voici une classe Java unique qui enchaîne toutes les opérations que nous avons couvertes. Exécutez‑la comme une méthode `main` ordinaire ; ajustez simplement les chemins de fichiers pour correspondre à votre environnement.

```java
import com.aspose.cells.*;

public class CompleteExcelAutomation {

    public static void main(String[] args) throws Exception {
        // ----------- Step 1: Copy Pivot Table -----------
        Workbook srcWb = new Workbook("YOUR_DIRECTORY/src.xlsx");
        Worksheet srcSheet = srcWb.getWorksheets

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}