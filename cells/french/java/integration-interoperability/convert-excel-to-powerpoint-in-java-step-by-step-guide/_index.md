---
category: general
date: 2026-11-22
description: Convertir Excel en PowerPoint en Java avec Aspose.Cells. Apprenez comment
  créer un PowerPoint à partir d’un fichier Excel, exporter les feuilles de calcul
  en diapositives PPTX et automatiser les présentations.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- convert excel to powerpoint
- create powerpoint from excel file
- convert excel workbook to pptx slides
- java convert .xlsx to .pptx
language: fr
lastmod: 2026-11-22
og_description: Convertir Excel en PowerPoint en Java avec Aspose.Cells. Ce tutoriel
  vous montre comment créer un PowerPoint à partir d’un fichier Excel et exporter
  des fichiers .xlsx en diapositives .pptx.
og_image_alt: Diagram illustrating convert excel to powerpoint workflow
og_title: Convertir Excel en PowerPoint avec Java – guide complet de programmation
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Convert Excel to PowerPoint in Java using Aspose.Cells. Learn how to
    create PowerPoint from Excel file, export worksheets as PPTX slides, and automate
    presentations.
  headline: Convert Excel to PowerPoint in Java – step‑by‑step guide
  type: TechArticle
- description: Convert Excel to PowerPoint in Java using Aspose.Cells. Learn how to
    create PowerPoint from Excel file, export worksheets as PPTX slides, and automate
    presentations.
  name: Convert Excel to PowerPoint in Java – step‑by‑step guide
  steps:
  - name: Expected output
    text: 'Running the program prints:'
  - name: Converting only selected sheets
    text: 'If you want to **convert Excel workbook to PPTX slides** but exclude certain
      worksheets, filter them before saving:'
  - name: Handling large workbooks
    text: 'For workbooks with many sheets, memory consumption can become significant.
      Use `WorkbookSettings` to enable streaming:'
  - name: Preserving formulas
    text: Aspose.Cells evaluates formulas before rendering. If you need the raw formula
      text on the slide, set `opts.setExportFormulas(true)`.
  type: HowTo
tags:
- java
- excel
- powerpoint
- aspose
title: Convertir Excel en PowerPoint en Java – guide étape par étape
url: /fr/java/integration-interoperability/convert-excel-to-powerpoint-in-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Convertir Excel en PowerPoint en Java – guide étape par étape

Si vous devez **convertir Excel en PowerPoint en Java**, ce guide vous montre comment le faire avec Aspose.Cells. Que vous construisiez un moteur de reporting ou que vous automatisiez des présentations, vous apprendrez à **créer PowerPoint à partir d’un fichier Excel** de façon programmatique et à exporter chaque feuille de calcul en diapositives PPTX modifiables.

Le tutoriel couvre tout, de la configuration du projet à l’enregistrement de la présentation finale. À la fin, vous disposerez d’un programme Java exécutable qui convertit un classeur `.xlsx` en fichier `.pptx` que vous pouvez modifier dans Microsoft PowerPoint. Aucun copier‑coller manuel n’est nécessaire.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* Java 17 ou version ultérieure installé (le code utilise le système de modules moderne).  
* Une licence Aspose.Cells for Java ou une clé d’évaluation temporaire.  
* Maven ou Gradle pour la gestion des dépendances (l’exemple utilise Maven).  
* Un classeur Excel d’exemple (`input.xlsx`) placé dans un répertoire connu.

> **Astuce :** Aspose.Cells prend en charge les fichiers `.xls` et `.xlsx`. Le même code fonctionne pour les deux formats ; il suffit de changer l’extension du fichier.

## Étape 1 : Configurer le projet Java pour **convertir Excel en PowerPoint**

Créez un nouveau projet Maven (ou ajoutez‑le à un projet existant) et incluez la dépendance Aspose.Cells :

```xml
<!-- pom.xml -->
<project xmlns="http://maven.apache.org/POM/4.0.0" ...>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>excel-to-pptx</artifactId>
    <version>1.0.0</version>
    <properties>
        <java.version>17</java.version>
    </properties>

    <dependencies>
        <!-- Aspose.Cells for Java -->
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-cells</artifactId>
            <version>24.10</version> <!-- latest version as of 2026 -->
        </dependency>
    </dependencies>
</project>
```

Exécutez `mvn clean install` pour télécharger la bibliothèque. Si vous disposez d’un fichier de licence (`Aspose.Total.lic`), placez‑le dans le dossier `src/main/resources` ; le code le chargera automatiquement.

## Étape 2 : Charger le classeur Excel

La première étape fonctionnelle du processus de **conversion du classeur Excel en diapositives PPTX** consiste à charger le fichier source. Aspose.Cells peut ouvrir des fichiers depuis le système de fichiers, un flux ou même un tableau d’octets.

```java
package com.example;

import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // Load the license (optional for evaluation)
        License license = new License();
        try {
            license.setLicense(ExcelToPowerPoint.class.getResourceAsStream("/Aspose.Total.lic"));
        } catch (Exception e) {
            System.out.println("License not found – running in evaluation mode.");
        }

        // Path to the source .xlsx file
        String inputPath = "YOUR_DIRECTORY/input.xlsx";

        // Load the workbook
        Workbook wb = new Workbook(inputPath);
        System.out.println("Workbook loaded successfully.");
```

**Pourquoi c’est important :** Le chargement du classeur valide le format du fichier et prépare les structures internes qu’Aspose.Cells traduira ensuite en objets PowerPoint.

## Étape 3 : Configurer les options d’enregistrement pour **créer PowerPoint à partir d’un fichier Excel**

Aspose.Cells utilise `ImageOrPrintOptions` pour définir le format de sortie lors de la conversion en fichiers de présentation. Définissez le `SaveFormat` sur `SaveFormat.PPTX` pour générer des diapositives modifiables.

```java
        // Step 3: Set up conversion options
        ImageOrPrintOptions opts = new ImageOrPrintOptions();
        opts.setSaveFormat(SaveFormat.PPTX);          // Export as PPTX
        opts.setOnePagePerSheet(false);               // Each sheet becomes a separate slide
        opts.setRenderToSize(1024, 768);               // Optional: control slide resolution
        System.out.println("Conversion options configured.");
```

**Pourquoi c’est important :** Le drapeau `setOnePagePerSheet(false)` indique à Aspose.Cells de traiter chaque feuille de calcul comme une diapositive individuelle, ce qui est le scénario le plus courant lorsque vous **convertissez Excel en PowerPoint** pour des présentations.

## Étape 4 : Enregistrer le classeur en diapositives PPTX

Vous pouvez maintenant écrire la présentation sur le disque. La méthode `Workbook.save` accepte le chemin de sortie ainsi que les options que vous avez configurées.

```java
        // Step 4: Export the workbook to a PowerPoint file
        String outputPath = "YOUR_DIRECTORY/editable.pptx";
        wb.save(outputPath, opts);
        System.out.println("Conversion complete. PowerPoint saved to: " + outputPath);
    }
}
```

Lorsque vous ouvrez `editable.pptx` dans Microsoft PowerPoint, vous verrez une diapositive par feuille de calcul, avec toutes les cellules rendues sous forme de zones de texte et de formes modifiables. Vous pouvez ensuite modifier les polices, les couleurs ou ajouter des animations directement dans PowerPoint.

### Résultat attendu

L’exécution du programme affiche :

```
Workbook loaded successfully.
Conversion options configured.
Conversion complete. PowerPoint saved to: YOUR_DIRECTORY/editable.pptx
```

Et le fichier `editable.pptx` apparaît dans le répertoire spécifié, prêt à être ajusté manuellement ou à être utilisé dans une automatisation supplémentaire.

## Étape 5 : Variantes courantes et cas limites

### Conversion de feuilles sélectionnées uniquement

Si vous souhaitez **convertir le classeur Excel en diapositives PPTX** mais exclure certaines feuilles, filtrez‑les avant l’enregistrement :

```java
        // Example: Export only the first two worksheets
        int[] sheetIndices = {0, 1};
        wb.save(outputPath, opts, sheetIndices);
```

### Gestion de classeurs volumineux

Pour les classeurs contenant de nombreuses feuilles, la consommation de mémoire peut devenir importante. Utilisez `WorkbookSettings` pour activer le streaming :

```java
        wb.getSettings().setMemorySetting(MemorySetting.MEMORY_PREFERENCE);
```

### Conservation des formules

Aspose.Cells évalue les formules avant le rendu. Si vous avez besoin du texte brut de la formule sur la diapositive, définissez `opts.setExportFormulas(true)`.

## Étape 6 : Vérifier le résultat programmatique (optionnel)

Vous pouvez charger le PPTX généré avec Aspose.Slides pour confirmer que le nombre de diapositives correspond au nombre de feuilles :

```java
import com.aspose.slides.*;

        Presentation pres = new Presentation(outputPath);
        int slideCount = pres.getSlides().size();
        System.out.println("Generated PPTX contains " + slideCount + " slides.");
```

Cette vérification supplémentaire est utile dans les pipelines CI où vous voulez vous assurer que la conversion a réussi.

## Conclusion

Vous disposez maintenant d’une solution complète, prête pour la production, pour **convertir Excel en PowerPoint en Java**. Le programme charge un classeur `.xlsx`, configure `ImageOrPrintOptions` pour **créer PowerPoint à partir d’un fichier Excel**, et enregistre le résultat sous forme de diapositives PPTX modifiables. En ajustant les options, vous pouvez affiner la résolution, sélectionner des feuilles spécifiques ou streamer de gros fichiers, rendant l’approche flexible pour de nombreux scénarios d’automatisation.

**Prochaines étapes**

* Explorez davantage **java convert .xlsx to .pptx** en ajoutant des mises en page de diapositives personnalisées avec Aspose.Slides.  
* Automatisez le traitement par lots de plusieurs classeurs à l’aide d’un simple observateur de répertoires.  
* Combinez cette conversion avec la génération de graphiques pilotés par les données pour produire des présentations dynamiques.

N’hésitez pas à expérimenter avec les paramètres et à partager vos résultats. Bon codage !

## Que devriez‑vous apprendre ensuite ?


Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets avec des explications étape par étape pour vous aider à maîtriser d’autres fonctionnalités de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Convert Excel to PowerPoint with Aspose.Cells in Java](/cells/english/java/integration-interoperability/convert-excel-to-powerpoint-with-aspose-cells-in-java/)
- [How to Convert Excel to PowerPoint Using Aspose.Cells for .NET: A Complete Guide](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)
- [Convert Excel To Powerpoint Aspose Cells Dotnet](/cells/german/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}