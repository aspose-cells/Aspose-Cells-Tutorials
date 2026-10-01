---
category: general
date: 2026-10-01
description: Apprenez comment exporter une forme avec ShapeExportOptions en Java,
  tout en conservant la forme éditable lors de la conversion en PPTX avec Aspose.Cells.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export shape with ShapeExportOptions
- Aspose Cells export shape
- Java export shape to PPTX
- editable shape export
- ShapeExportOptions setExportAsEditable
- export textbox shape
language: fr
lastmod: 2026-10-01
og_description: Exporter une forme avec ShapeExportOptions en Java pour créer des
  fichiers PPTX modifiables. Ce tutoriel vous guide à travers le processus complet
  en utilisant Aspose.Cells.
og_image_alt: Screenshot showing Java code exporting a textbox shape to PPTX using
  ShapeExportOptions
og_title: Exporter une forme avec ShapeExportOptions en Java – guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-10-01'
  description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  headline: How to export shape with ShapeExportOptions in Java
  type: TechArticle
- description: Learn how to export shape with ShapeExportOptions in Java, keeping
    the shape editable when converting to PPTX using Aspose.Cells.
  name: How to export shape with ShapeExportOptions in Java
  steps:
  - name: Expected result
    text: '- `textbox.pptx` appears in the specified directory. - Opening the file
      in PowerPoint shows a single slide with the original textbox. - The textbox
      is fully editable (you can change text, font, size, etc.).'
  - name: Verify programmatically
    text: '```java // Load the generated PPTX to confirm it contains one slide Presentation
      presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx"); int slideCount
      = presentation.getSlides().size(); System.out.println("Slides in exported PPTX:
      " + slideCount); ```'
  - name: 'Edge case: Multiple shapes'
    text: 'If the worksheet contains several shapes and you only want a specific one,
      locate it by name:'
  - name: 'Edge case: Shape not found'
    text: '```java if (worksheet.getShapes().size() == 0) { throw new IllegalStateException("No
      shapes found on the worksheet."); } ```'
  - name: 'Edge case: Export to other formats'
    text: '`ShapeExportOptions` also supports PNG, JPEG, SVG, and EMF. Change the
      file extension and optionally set `exportOptions.setImageFormat(ImageFormat.PNG)`.'
  - name: Conclusion
    text: You now know how to **export shape with ShapeExportOptions** in Java, preserving
      editability when converting a textbox (or any other shape) to a PPTX file. By
      following the steps above—setting up the library, loading the workbook, configuring
      `ShapeExportOptions`, and invoking `exportToImage`—you ca
  type: HowTo
tags:
- Aspose.Cells
- Java
- ShapeExportOptions
- PPTX
- Export
title: Comment exporter une forme avec ShapeExportOptions en Java
url: /fr/java/images-shapes/how-to-export-shape-with-shapeexportoptions-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment exporter une forme avec ShapeExportOptions en Java

Si vous devez **exporter une forme avec ShapeExportOptions** depuis un classeur Excel, ce guide vous montre les étapes exactes. Vous verrez comment garder la forme modifiable lors de sa conversion en fichier PPTX, ce qui est essentiel pour l'édition en aval dans PowerPoint.

L'exportation de formes est une tâche courante lorsque vous générez des présentations à partir de feuilles de calcul — que vous créiez des decks de vente, des tableaux de bord de reporting ou des présentations automatisées. Ce tutoriel couvre tout ce dont vous avez besoin, de la configuration du projet à la vérification du fichier exporté, et il utilise la bibliothèque **Aspose.Cells for Java**.

## Ce dont vous aurez besoin

- Java 17 ou supérieur (le code se compile avec n'importe quel JDK récent)
- Maven ou Gradle pour la gestion des dépendances
- Un fichier Excel (`Shapes.xlsx`) contenant au moins une zone de texte ou une autre forme
- Une connaissance de base des API Aspose.Cells

## Étape 1 : Ajouter Aspose.Cells à votre projet (Aspose Cells export shape)

Si vous utilisez Maven, ajoutez la dépendance suivante à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.10</version> <!-- use the latest stable version -->
</dependency>
```

Pour Gradle, placez ceci dans `build.gradle` :

```gradle
implementation 'com.aspose:aspose-cells:24.10'
```

> **Pro tip:** Enregistrez votre licence tôt pour éviter les filigranes d'évaluation.  
> ```java
> License license = new License();
> license.setLicense("Aspose.Total.Java.lic");
> ```

## Étape 2 : Charger le classeur qui contient la forme

```java
// Load the workbook that contains the shape
Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");
```

L'objet `Workbook` représente le fichier Excel complet. Le charger est la première condition préalable à toute manipulation de forme.

## Étape 3 : Accéder à la feuille de calcul et récupérer la forme souhaitée (Java export shape to PPTX)

```java
// Access the first worksheet (index 0)
Worksheet worksheet = workbook.getWorksheets().get(0);

// Retrieve the first shape on the sheet.
// You can also use get("ShapeName") if you know the shape's name.
Shape textBoxShape = worksheet.getShapes().get(0);
```

> **Pourquoi c'est important :** Les formes sont stockées par feuille, vous devez donc naviguer vers la feuille correcte avant de pouvoir exporter une forme spécifique.

## Étape 4 : Configurer **ShapeExportOptions** pour garder la forme modifiable (editable shape export)

```java
// Create export options and enable editable export
ShapeExportOptions exportOptions = new ShapeExportOptions();
exportOptions.setExportAsEditable(true); // <-- makes the shape editable in PPTX
```

Définir `ExportAsEditable` à `true` indique à Aspose.Cells de préserver les données vectorielles de la forme, permettant aux utilisateurs de PowerPoint de modifier la forme après l'importation.

## Étape 5 : Exporter la forme directement vers un fichier PPTX (export textbox shape)

```java
// Export the shape as a PPTX file
textBoxShape.exportToImage("YOUR_DIRECTORY/textbox.pptx", exportOptions);
```

La méthode `exportToImage` fonctionne pour plusieurs formats d'image ; lorsque le nom du fichier cible se termine par `.pptx`, Aspose.Cells écrit une diapositive PowerPoint contenant la forme.

### Résultat attendu

- `textbox.pptx` apparaît dans le répertoire spécifié.
- L'ouverture du fichier dans PowerPoint affiche une seule diapositive avec la zone de texte originale.
- La zone de texte est entièrement modifiable (vous pouvez changer le texte, la police, la taille, etc.).

## Étape 6 : Vérifier la sortie et gérer les cas limites courants

### Vérifier programmatique

```java
// Load the generated PPTX to confirm it contains one slide
Presentation presentation = new Presentation("YOUR_DIRECTORY/textbox.pptx");
int slideCount = presentation.getSlides().size();
System.out.println("Slides in exported PPTX: " + slideCount);
```

Si `slideCount` vaut `1`, l'exportation a réussi.

### Cas limite : Plusieurs formes

Si la feuille contient plusieurs formes et que vous ne voulez qu'une forme spécifique, localisez‑la par son nom :

```java
Shape targetShape = worksheet.getShapes().get("MyTextBox");
targetShape.exportToImage("output.pptx", exportOptions);
```

### Cas limite : Forme non trouvée

```java
if (worksheet.getShapes().size() == 0) {
    throw new IllegalStateException("No shapes found on the worksheet.");
}
```

### Cas limite : Exporter vers d'autres formats

`ShapeExportOptions` prend également en charge PNG, JPEG, SVG et EMF. Changez l'extension du fichier et, éventuellement, définissez `exportOptions.setImageFormat(ImageFormat.PNG)`.

## Exemple complet et exécutable

Assembler toutes les pièces vous donne un programme autonome que vous pouvez copier‑coller dans votre IDE :

```java
import com.aspose.cells.*;

public class ExportShapeExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/Shapes.xlsx");

        // 2️⃣ Get first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 3️⃣ Retrieve the first shape (or use get("ShapeName"))
        Shape shape = worksheet.getShapes().get(0);

        // 4️⃣ Prepare export options for editable PPTX
        ShapeExportOptions options = new ShapeExportOptions();
        options.setExportAsEditable(true); // keep shape editable

        // 5️⃣ Export to PPTX
        String outPath = "YOUR_DIRECTORY/textbox.pptx";
        shape.exportToImage(outPath, options);
        System.out.println("Shape exported to " + outPath);

        // 6️⃣ Optional verification
        Presentation pres = new Presentation(outPath);
        System.out.println("Slide count: " + pres.getSlides().size());
    }
}
```

L'exécution du programme crée `textbox.pptx`. Ouvrez-le dans PowerPoint, faites un clic droit sur la zone de texte, et vous verrez les poignées d'édition habituelles — confirmant que **export shape with ShapeExportOptions** a préservé la possibilité de modification.

## Questions fréquemment posées

| Question | Answer |
|----------|--------|
| *Puis-je exporter une forme de graphique ?* | Oui. Le même appel `exportToImage` fonctionne pour les graphiques, les images et SmartArt. |
| *Et si j’ai besoin d’un PNG à plus haute résolution ?* | Définissez `options.setImageFormat(ImageFormat.PNG)` et ajustez `options.setResolution(300)` avant l'exportation. |
| *Le PPTX exporté est‑il compatible avec les anciennes versions de PowerPoint ?* | La bibliothèque écrit du Office Open XML (PPTX) qui est pris en charge par PowerPoint 2007 et versions ultérieures. |
| *Ai‑je besoin d’une licence pour que cela fonctionne ?* | Une évaluation gratuite fonctionne mais ajoute un filigrane. Enregistrez une licence pour le supprimer. |

## Prochaines étapes

- Explorez **Aspose.Slides for Java** si vous devez combiner plusieurs formes exportées en un seul deck de diapositives.
- Utilisez **ShapeExportOptions.setExportAsEditable(false)** lorsque vous préférez une image raster (PNG/JPEG) pour un rendu plus rapide.
- Automatisez le traitement par lots : parcourez toutes les feuilles et exportez chaque forme vers des fichiers PPTX séparés.

---

### Conclusion

Vous savez maintenant comment **exporter une forme avec ShapeExportOptions** en Java, en préservant la possibilité de modification lors de la conversion d’une zone de texte (ou de toute autre forme) en fichier PPTX. En suivant les étapes ci‑dessus — configuration de la bibliothèque, chargement du classeur, configuration de `ShapeExportOptions` et appel de `exportToImage` — vous pouvez intégrer l'exportation de formes dans n'importe quel pipeline de reporting automatisé.

N'hésitez pas à expérimenter avec différentes formes, formats de sortie et réglages de résolution. Si vous avez trouvé ce guide utile, partagez‑le avec vos collègues ou ajoutez‑le à vos favoris pour une référence future. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités d'API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment ajuster les marges d'une forme dans Excel avec Aspose.Cells pour Java](/cells/english/java/images-shapes/excel-aspose-cells-java-shape-margins/)
- [Comment appliquer le formatage 3D d'une forme dans Excel avec Aspose.Cells pour Java](/cells/english/java/images-shapes/aspose-cells-java-3d-shape-formatting/)
- [Guide de copie de formes de classeur Aspose Cells Java](/cells/hindi/java/images-shapes/aspose-cells-java-workbook-shape-copying-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}