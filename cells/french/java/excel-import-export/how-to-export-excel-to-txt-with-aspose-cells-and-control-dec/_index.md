---
category: general
date: 2026-08-20
description: Apprenez à exporter Excel en TXT tout en limitant les décimales, en conservant
  les chiffres significatifs et en enregistrant le classeur au format TXT avec Java.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel to txt
- limit decimal places
- keep significant digits
- save workbook as txt
language: fr
lastmod: 2026-08-20
og_description: Exporter Excel vers TXT avec Aspose.Cells. Ce guide montre comment
  limiter le nombre de décimales, conserver les chiffres significatifs et enregistrer
  le classeur au format TXT en Java.
og_image_alt: Result of export excel to txt showing limited decimal places and kept
  significant digits
og_title: Exporter Excel vers TXT en Java – contrôler les décimales et les chiffres
  significatifs
schemas:
- author: Aspose
  dateModified: '2026-08-20'
  description: Learn to export Excel to TXT while limiting decimal places, keeping
    significant digits, and saving workbook as TXT using Java.
  headline: How to export Excel to TXT with Aspose.Cells and control decimal precision
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel
- Text export
title: Comment exporter Excel en TXT avec Aspose.Cells et contrôler la précision décimale
url: /fr/java/excel-import-export/how-to-export-excel-to-txt-with-aspose-cells-and-control-dec/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exporter Excel vers TXT avec Aspose.Cells et contrôler la précision décimale

Si vous devez **exporter Excel vers TXT** et garantir que la sortie respecte un nombre précis de décimales, ce guide fournit une solution complète. Vous verrez comment limiter les décimales, conserver les chiffres significatifs et **enregistrer le classeur au format TXT** à l’aide de la bibliothèque Aspose.Cells pour Java.

Le tutoriel parcourt la création d’un classeur, l’insertion d’une valeur à haute précision, la configuration des options d’enregistrement TXT, et l’écriture du fichier sur le disque. À la fin, vous pourrez générer un fichier texte contenant exactement la précision requise, sans post‑traitement manuel.

## Ce dont vous avez besoin

- Java 17 (ou tout JDK supporté)
- Aspose.Cells for Java 23.10 ou plus récent
- Un IDE ou un outil de construction (Maven/Gradle) pour gérer les dépendances
- Permission d’écriture sur le répertoire de sortie

## Étape 1 : Créer un classeur et accéder à la première feuille

Créer un classeur est la première étape lorsque vous voulez **exporter Excel vers TXT**. La classe `Workbook` représente le fichier Excel complet, et `Worksheet` vous donne accès aux cellules.

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Initialize a new workbook
        Workbook workbook = new Workbook();

        // Get the first worksheet (index 0)
        Worksheet sheet = workbook.getWorksheets().get(0);
```

*Pourquoi c’est important* : L’objet classeur contient toutes les données, styles et métadonnées. Commencer avec un classeur vierge garantit qu’aucun formatage caché n’interfère avec l’exportation texte.

## Étape 2 : Ajouter une valeur numérique et limiter les décimales

Insérez un nombre comportant de nombreuses décimales afin de démontrer comment **limiter les décimales** lors de l’exportation.

```java
        // Put a high‑precision number into cell A1
        sheet.getCells().putValue("A1", 0.000123456789);
```

*Pourquoi c’est important* : Excel stocke la pleine précision, mais lors de l’exportation, vous pouvez vouloir tronquer ou arrondir la valeur. Le paramètre **limit decimal places** gérera cela automatiquement.

## Étape 3 : Configurer les options d’enregistrement TXT pour conserver les chiffres significatifs

Aspose.Cells fournit `TxtSaveOptions`. Définir `significantDigits` indique à l’exportateur de ne garder que le nombre requis de chiffres significatifs, en ignorant les zéros non significatifs.

```java
        // Configure TXT export options
        TxtSaveOptions txtOptions = new TxtSaveOptions();

        // Keep exactly 5 significant digits (e.g., 0.00012346)
        txtOptions.setSignificantDigits(5);
```

*Pourquoi c’est important* : L’option **keep significant digits** assure que le fichier de sortie contient une quantité prévisible de précision, ce qui est essentiel pour les systèmes en aval qui attendent un format numérique à largeur fixe.

## Étape 4 : Enregistrer le classeur au format TXT

Enfin, écrivez le classeur dans un fichier texte. La méthode `save` respecte les options que vous avez configurées, de sorte que le fichier résultant contiendra la représentation décimale limitée.

```java
        // Define the output path (replace with your own directory)
        String outputPath = "output/SignificantDigits.txt";

        // Export the workbook to TXT using the configured options
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

*Pourquoi c’est important* : Utiliser **save workbook as txt** avec les `TxtSaveOptions` préparées garantit que le fichier exporté correspond aux contraintes de précision définies à l’étape précédente.

### Contenu attendu de `SignificantDigits.txt`

```
0.00012346
```

La valeur montre cinq chiffres significatifs (`12346`) après arrondi, et les zéros initiaux sont préservés selon le format TXT.

## Variantes et cas particuliers

| Scénario | Ajustement |
|----------|------------|
| **Nombre différent de chiffres significatifs** | Appelez `txtOptions.setSignificantDigits(n)` où `n` est compris entre 1 et 15. |
| **Exporter une plage au lieu de la feuille entière** | Utilisez `txtOptions.setExportRange("A1:B10")` avant l’enregistrement. |
| **Conserver les séparateurs de colonnes** | Définissez `txtOptions.setSeparator('\t')` pour une sortie délimitée par des tabulations. |
| **Grandes feuilles de calcul** | Augmentez `txtOptions.setMemorySetting(MemorySetting.MEMORY_PREFERENCES)` pour éviter `OutOfMemoryError`. |

## Pièges courants et astuces professionnelles

- **Ne confondez pas les chiffres significatifs avec les décimales**. Les zéros initiaux ne sont pas comptés comme significatifs ; utilisez `setSignificantDigits` pour la précision réelle et `setDecimalPlaces` si vous avez besoin d’un nombre fixe de chiffres après la virgule.
- **Spécifiez toujours un chemin de sortie absolu** lors de l’exécution depuis un IDE afin d’éviter les erreurs de permission.
- **Validez le fichier généré** avec un simple appel `java.nio.file.Files.readAllLines(Paths.get(outputPath))` pour vous assurer que le contenu correspond aux attentes avant de le transmettre aux processus en aval.

## Code source complet à titre de référence

```java
import com.aspose.cells.*;

public class ExportExcelToTxtDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook and get the first worksheet
        Workbook workbook = new Workbook();
        Worksheet sheet = workbook.getWorksheets().get(0);

        // Step 2: Insert a high‑precision number (will be limited later)
        sheet.getCells().putValue("A1", 0.000123456789);

        // Step 3: Set TXT options – keep 5 significant digits
        TxtSaveOptions txtOptions = new TxtSaveOptions();
        txtOptions.setSignificantDigits(5);   // keep significant digits

        // Step 4: Save the workbook as TXT
        String outputPath = "output/SignificantDigits.txt";
        workbook.save(outputPath, txtOptions);

        System.out.println("Export completed: " + outputPath);
    }
}
```

L’exécution du programme produit `SignificantDigits.txt` contenant la ligne unique `0.00012346`, démontrant que le processus **export excel to txt** respecte à la fois les exigences **limit decimal places** et **keep significant digits**.

## Conclusion

Vous savez maintenant comment **exporter Excel vers TXT** avec Aspose.Cells pour Java tout en contrôlant la précision numérique. En configurant `TxtSaveOptions`, vous pouvez **limiter les décimales**, **conserver les chiffres significatifs**, et enregistrer le classeur au format txt de façon fiable, sans post‑traitement supplémentaire.

Ensuite, vous pourriez explorer :

- Exporter plusieurs feuilles vers des fichiers TXT séparés (`save workbook as txt` par feuille)
- Utiliser `setSeparator` pour créer une sortie compatible CSV
- Automatiser les conversions par lots pour de grands ensembles de données

N’hésitez pas à expérimenter avec différents nombres de chiffres et séparateurs afin d’adapter la solution aux besoins exacts de votre projet. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment créer et exporter Excel vers HTML avec Aspose.Cells Java | Guide des opérations sur les classeurs](/cells/english/java/workbook-operations/aspose-cells-java-excel-html-export/)
- [Enregistrer Excel en texte – Guide complet C# pour exporter Excel vers TXT](/cells/english/net/converting-excel-files-to-other-formats/save-excel-as-text-complete-c-guide-to-export-excel-to-txt/)
- [Exporter un classeur Excel en image avec Aspose.Cells pour Java : guide étape par étape](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}