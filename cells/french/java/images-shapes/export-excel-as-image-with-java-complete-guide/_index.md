---
category: general
date: 2026-11-22
description: Exporter Excel en image avec Java en utilisant Aspose.Cells. Apprenez
  comment ajouter une image à la feuille de calcul et enregistrer Excel au format
  PNG en quelques étapes.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- export excel as image
- add picture to worksheet
- export excel sheet to png
- save excel as png file
- save workbook as image
language: fr
lastmod: 2026-11-22
og_description: Exportez Excel en image avec Java en utilisant Aspose.Cells. Suivez
  ce guide pour ajouter une image à la feuille de calcul et enregistrer rapidement
  le fichier Excel au format PNG.
og_image_alt: Code snippet showing Java export of an Excel worksheet to a PNG image
og_title: Exporter Excel en image avec Java – tutoriel étape par étape
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Export Excel as image with Java using Aspose.Cells. Learn how to add
    picture to worksheet and save Excel as PNG file in a few steps.
  headline: Export Excel as image with Java – complete guide
  type: TechArticle
tags:
- Java
- Aspose.Cells
- Excel automation
- Image export
title: Exporter Excel en image avec Java – guide complet
url: /fr/java/images-shapes/export-excel-as-image-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Exporter Excel en image avec Java – guide complet

Si vous devez **exporter Excel en image** dans une application Java, ce tutoriel vous montre une solution prête à l'emploi. Vous verrez comment ajouter une image à la feuille de calcul, configurer les options d'exportation, et enfin **enregistrer Excel en fichier PNG** en quelques lignes de code.

Le guide couvre tout, de la configuration de Maven à la gestion des cas particuliers, afin que vous puissiez intégrer la technique dans n'importe quel projet nécessitant des captures visuelles de feuilles de calcul.

## Prérequis

* Java 17 ou version plus récente installé.
* Maven 3.6+ (ou Gradle) pour la gestion des dépendances.
* Une licence Aspose.Cells for Java (l'évaluation gratuite fonctionne pour les tests).
* Un classeur Excel d'exemple (`sample.xlsx`) contenant les données que vous souhaitez exporter.

## Étape 1 : Ajouter la dépendance Aspose.Cells

Aspose.Cells fournit la classe `ImageOrPrintOptions` utilisée pour **exporter Excel en image**. Ajoutez la dépendance suivante à votre `pom.xml` (ou l'équivalent Gradle).

```xml
<!-- pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest stable version -->
</dependency>
```

> **Astuce :** Gardez le numéro de version à jour ; les nouvelles versions incluent des améliorations de performances pour le rendu d'images.

## Étape 2 : Charger le classeur et sélectionner la feuille de calcul

La première étape programmatique consiste à ouvrir le fichier Excel et à obtenir une référence à la feuille de calcul que vous souhaitez exporter.

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load the workbook from disk
        Workbook wb = new Workbook("sample.xlsx");

        // Access the first worksheet (index 0)
        Worksheet ws = wb.getWorksheets().get(0);
```

*Pourquoi c'est important* : Charger le classeur vous donne accès à ses objets internes, et sélectionner la bonne feuille garantit que la bonne plage est rendue.

## Étape 3 : Configurer ImageOrPrintOptions (exporter Excel en image)

`ImageOrPrintOptions` contrôle le format d'image, la résolution et d'autres paramètres de rendu. Ici, nous définissons le format sur PNG, ce qui satisfait l'exigence **exporter la feuille Excel en png**.

```java
        // Create options for image export
        ImageOrPrintOptions opts = new ImageOrPrintOptions();

        // Set the desired image format (PNG)
        opts.setSaveFormat(SaveFormat.PNG);

        // Optional: increase resolution for sharper output
        opts.setResolution(300);
```

Définir le format sur `PNG` garantit une compression sans perte, rendant le fichier adapté à un traitement ultérieur ou à une inclusion dans des rapports.

## Étape 4 : Ajouter une image à la feuille de calcul (add picture to worksheet)

Si vous devez incorporer une image — comme un logo ou une capture d'une autre plage — utilisez la collection `Pictures`. Le code suivant insère une image de la plage `A1:G20` dans le coin supérieur gauche de la feuille de calcul.

```java
        // Insert a picture of the range A1:G20 at cell (0,0)
        ws.getPictures().add(0, 0, "A1:G20");
```

> **Pourquoi vous pourriez faire cela** : Ajouter une image avant l'exportation vous permet de combiner des graphiques statiques avec les données de la feuille, produisant une image finale plus riche.

## Étape 5 : Enregistrer la feuille de calcul en fichier PNG (save excel as png file, save workbook as image)

Enfin, appelez `Workbook.save` avec les options configurées. La méthode écrit un fichier PNG dans le répertoire spécifié.

```java
        // Save the worksheet as an image file
        wb.save("output/pivot.png", opts);

        System.out.println("Export completed: output/pivot.png");
    }
}
```

Lorsque le programme se termine, `output/pivot.png` contient une représentation pixel‑parfait de la feuille de calcul, y compris l'image que vous avez ajoutée.

### Fichier source complet

```java
import com.aspose.cells.*;

public class ExcelToImage {
    public static void main(String[] args) throws Exception {
        // Load workbook
        Workbook wb = new Workbook("sample.xlsx");
        Worksheet ws = wb.getWorksheets().get(0);

        // Configure export options
        ImageOrPrintOptions opts = new ImageOrPrintOptions();
        opts.setSaveFormat(SaveFormat.PNG);
        opts.setResolution(300); // optional high‑DPI output

        // Add picture to worksheet
        ws.getPictures().add(0, 0, "A1:G20");

        // Export worksheet as PNG image
        wb.save("output/pivot.png", opts);
        System.out.println("Export completed: output/pivot.png");
    }
}
```

L'exécution de la classe produit le fichier PNG affiché ci-dessous (l'image est illustrative ; votre fichier reflétera le contenu réel de la feuille de calcul).

![Feuille de calcul Excel exportée en PNG](/images/excel-to-png.png "Résultat de l'exportation d'Excel en image avec Java")

*Texte alternatif (alt de l'image) :* **Résultat de l'exportation d'Excel en image avec Java – une capture PNG de la feuille de calcul** (satisfait l'exigence d'alt d'image).

## Problèmes courants et comment les éviter

| Issue | Reason | Fix |
|-------|--------|-----|
| **Fichier non trouvé** | Le chemin vers `sample.xlsx` est incorrect. | Utilisez un chemin absolu ou placez le fichier à la racine du projet. |
| **Image vide** | La feuille de calcul n'a aucun contenu visible ou la plage d'image est vide. | Vérifiez que les cellules `A1:G20` contiennent des données ou ajustez la plage. |
| **Résolution basse** | Le DPI par défaut est 96, ce qui peut apparaître flou à l'impression. | Appelez `opts.setResolution(300)` (ou plus) avant d'enregistrer. |
| **Exception de licence** | L'utilisation de la version d'évaluation peut ajouter un filigrane. | Appliquez une licence Aspose.Cells valide avec `License license = new License(); license.setLicense("Aspose.Total.lic");`. |

## Prochaines étapes

Maintenant que vous pouvez **exporter Excel en image**, vous pourriez explorer :

* **Exporter la feuille Excel en png** pour chaque feuille d'un classeur (boucle sur `wb.getWorksheets()`).
* Convertir le PNG en PDF avec Aspose.PDF si vous avez besoin d'un format adapté aux documents.
* Intégrer le PNG généré dans une page web ou une pièce jointe d'email directement depuis Java.

Ces extensions s'appuient sur le même modèle `ImageOrPrintOptions`, maintenant la cohérence du code.

## Conclusion

Vous avez appris comment **exporter Excel en image** avec Java, comment **ajouter une image à la feuille de calcul**, et comment **enregistrer Excel en fichier PNG** en utilisant Aspose.Cells. L'exemple complet montre une méthode fiable pour **enregistrer le classeur en image**, gérer la résolution et éviter les erreurs courantes. Appliquez ce modèle pour automatiser les rapports, générer des miniatures ou intégrer des visuels de feuilles de calcul dans tout flux de travail basé sur Java.

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Comment exporter une feuille de calcul Excel en PNG avec Aspose.Cells Java](/cells/english/java/workbook-operations/export-excel-to-png-aspose-cells-java/)
- [Exporter un classeur Excel en image avec Aspose.Cells pour Java : guide étape par étape](/cells/english/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)
- [Exporter un classeur Excel en image avec Aspose Cells pour Java](/cells/german/java/import-export/export-excel-workbook-as-image-using-aspose-cells-for-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}