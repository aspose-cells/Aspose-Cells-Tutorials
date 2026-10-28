---
category: general
date: 2026-09-05
description: Apprenez à copier une plage dans Excel, à exporter Excel vers PowerPoint
  et à convertir Excel en pptx avec un exemple Java complet.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy range
- export excel to powerpoint
- convert excel to pptx
- copy pivot table sheet
- how to export excel
language: fr
lastmod: 2026-09-05
og_description: Comment copier une plage et exporter Excel vers PowerPoint avec Java.
  Suivez ce guide étape par étape pour convertir Excel en PPTX efficacement.
og_image_alt: Screenshot showing how to copy range from Excel to PowerPoint in a Java
  IDE
og_title: Comment copier une plage depuis Excel et l’exporter vers PowerPoint en Java
schemas:
- author: Aspose
  dateModified: '2026-09-05'
  description: Learn how to copy range in Excel, export excel to PowerPoint and convert
    excel to pptx with a complete Java example.
  headline: How to copy range from Excel and export it to PowerPoint using Java
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
- PowerPoint export
title: Comment copier une plage depuis Excel et l’exporter vers PowerPoint avec Java
url: /fr/java/integration-interoperability/how-to-copy-range-from-excel-and-export-it-to-powerpoint-usi/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment copier une plage depuis Excel et l'exporter vers PowerPoint avec Java

Si vous devez **comment copier une plage** depuis un classeur Excel et ensuite **exporter Excel vers PowerPoint**, ce guide vous fournit une solution complète, prête à l'emploi. Vous verrez exactement comment copier une plage contenant un tableau croisé dynamique, créer une nouvelle feuille de calcul pour la copie, et enfin **convert Excel to PPTX** avec un seul appel de méthode.

Copier des plages et exporter des classeurs est une exigence courante lorsque vous générez des rapports, des présentations ou des tableaux de bord de façon programmatique. À la fin de ce tutoriel, vous disposerez d’un programme Java qui :

* Charge un fichier `.xlsx` existant.
* Copie la plage `A1:H20` (incluant un tableau croisé dynamique) vers une nouvelle feuille.
* Enregistre le classeur sous forme d’une présentation `.pptx` éditable.

Vous n’avez besoin que de la bibliothèque Aspose.Cells for Java ; aucune dépendance supplémentaire n’est requise.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* Java 17 (ou version supérieure) installé.
* Maven ou Gradle pour gérer les dépendances.
* Aspose.Cells for Java 23.9 (ou la dernière version) – ajoutez‑la à votre projet comme indiqué dans l’extrait Maven ci‑dessous.
* Un fichier Excel (`input.xlsx`) contenant les données et le tableau croisé dynamique que vous souhaitez copier.

```xml
<!-- Maven dependency -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier>
</dependency>
```

## Étape 1 : Charger le classeur depuis un fichier

La première opération pour **comment copier une plage** consiste à ouvrir le classeur source. Cela vous donne accès aux feuilles, aux cellules et aux tableaux croisés dynamiques.

```java
// Load the workbook from a file
Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");
```

*Pourquoi cette étape ?*  
Le chargement du fichier crée une représentation en mémoire du document Excel, vous permettant de manipuler son contenu sans toucher au fichier original.

## Étape 2 : Obtenir la feuille source contenant les données

Typiquement, la première feuille contient les données que vous voulez copier. Vous pouvez la récupérer par son indice.

```java
// Get the source worksheet (first sheet) that contains the data/pivot table
Worksheet sourceSheet = workbook.getWorksheets().get(0);
```

Si votre classeur stocke le tableau croisé dynamique sur une autre feuille, remplacez `0` par l’indice approprié ou utilisez `get("SheetName")`.

## Étape 3 : Ajouter une nouvelle feuille pour la plage copiée

Créer une feuille de destination isole les données copiées et rend l’exportation ultérieure plus propre.

```java
// Add a new worksheet that will receive the copied range
Worksheet destinationSheet = workbook.getWorksheets().add("Copy");
```

Vous pouvez nommer la feuille comme vous le souhaitez ; le nom « Copy » indique clairement qu’elle contient la plage dupliquée.

## Étape 4 : Copier la plage (comment copier une plage) incluant le tableau croisé dynamique

Nous effectuons maintenant l’opération principale **comment copier une plage**. La méthode `copyRange` copie à la fois les valeurs et le formatage, et elle préserve la définition du tableau croisé dynamique.

```java
// Copy the range A1:H20 (including the pivot table) to the new sheet starting at A1
sourceSheet.getCells().copyRange(
        "A1:H20",
        destinationSheet.getCells().get("A1"),
        new CopyOptions()   // default options copy values, formats, and objects
);
```

*Pourquoi utiliser `CopyOptions` ?*  
Fournir une instance de `CopyOptions` vous permet d’ajuster finement ce qui est copié (par ex., les formules, les largeurs de colonnes). Le constructeur par défaut copie tout, ce qui est idéal lorsque vous voulez une réplique exacte d’une **copy pivot table sheet**.

## Étape 5 : Préparer les options pour exporter le classeur en tant que présentation PowerPoint éditable

L’exportation vers PowerPoint se fait via `ImageOrPrintOptions`. Définir le format d’enregistrement sur `SaveFormat.PPTX` indique à Aspose.Cells de générer un fichier PowerPoint au lieu d’une image.

```java
// Prepare options to export the workbook as an editable PowerPoint presentation
ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
pptOptions.setSaveFormat(SaveFormat.PPTX);   // this enables export excel to powerpoint
```

Vous pouvez également ajuster les dimensions des diapositives, le DPI et d’autres paramètres de présentation via `pptOptions` si vous avez besoin d’une mise en page personnalisée.

## Étape 6 : Enregistrer le classeur en fichier PPTX (convertir Excel en PPTX)

Enfin, appelez `workbook.save` avec les options PPTX. Cette étape **comment exporter Excel** dans un diaporama.

```java
// Save the workbook to a PPTX file using the configured options
workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);
```

Après l’exécution du programme, `output.pptx` contiendra une seule diapositive où la plage copiée apparaît exactement comme dans Excel, y compris les contrôles du tableau croisé dynamique.

### Résultat attendu

Ouvrez `output.pptx` avec Microsoft PowerPoint ou tout visualiseur compatible. Vous devriez voir une diapositive affichant la plage `A1:H20`, en conservant les couleurs des cellules, les bordures et la mise en page du tableau croisé dynamique. La diapositive est entièrement éditable — vous pouvez déplacer, redimensionner ou formater le tableau comme tout contenu natif de PowerPoint.

## Exemple complet exécutable

Assembler toutes les étapes vous donne une classe Java autonome :

```java
import com.aspose.cells.*;

public class ExcelToPowerPoint {
    public static void main(String[] args) throws Exception {
        // 1. Load the workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/input.xlsx");

        // 2. Get the source worksheet (first sheet)
        Worksheet sourceSheet = workbook.getWorksheets().get(0);

        // 3. Add a destination worksheet
        Worksheet destinationSheet = workbook.getWorksheets().add("Copy");

        // 4. Copy the range A1:H20 (including pivot table)
        sourceSheet.getCells().copyRange(
                "A1:H20",
                destinationSheet.getCells().get("A1"),
                new CopyOptions()
        );

        // 5. Configure export options for PowerPoint
        ImageOrPrintOptions pptOptions = new ImageOrPrintOptions();
        pptOptions.setSaveFormat(SaveFormat.PPTX);

        // 6. Save as PPTX
        workbook.save("YOUR_DIRECTORY/output.pptx", pptOptions);

        System.out.println("Export completed: output.pptx created successfully.");
    }
}
```

Exécutez la classe depuis votre IDE ou via la ligne de commande :

```bash
mvn compile exec:java -Dexec.mainClass=ExcelToPowerPoint
```

Vous verrez le message de confirmation une fois le fichier écrit.

## Questions fréquentes et cas particuliers

| Question | Réponse |
|----------|--------|
| **Puis‑je copier une plage non contiguë ?** | Utilisez `copyRange` avec une plage nommée qui comprend plusieurs zones, ou appelez `copyRange` plusieurs fois pour chaque bloc. |
| **Que faire si la feuille source contient plusieurs tableaux croisés dynamiques ?** | Chaque tableau croisé dynamique à l’intérieur du rectangle copié est transféré. Pour les tableaux situés en dehors du rectangle, copiez‑les séparément. |
| **Comment exporter plusieurs feuilles en diapositives séparées ?** | Parcourez les feuilles de calcul, copiez chacune dans une feuille temporaire, puis appelez `workbook.save` avec `pptOptions` à chaque itération, en ajoutant au même PPTX via l’API `Presentation`. |
| **Le PPTX généré est‑il éditable ?** | Oui. L’exportation crée des objets PowerPoint natifs, vous pouvez donc modifier le texte, remodeler les tableaux ou ajouter des animations après coup. |
| **Et les classeurs volumineux ?** | Augmentez `pptOptions.setDpi(300)` pour une meilleure fidélité, mais surveillez l’utilisation mémoire ; traitez les feuilles par lots si nécessaire. |

## Astuces pro

* **Conserver les largeurs de colonnes** – appelez `CopyOptions.setColumnWidth(true)` avant la copie si vous avez besoin d’une correspondance exacte des largeurs.  
* **Utiliser une taille de diapositive personnalisée** – `pptOptions.setImageHeight(720); pptOptions.setImageWidth(1280);` pour correspondre à une présentation 16 : 9.  
* **Ajouter une diapositive de titre** – après l’exportation, ouvrez le PPTX avec Aspose.Slides et préfixez une diapositive contenant un titre et une date.

## Conclusion

Vous savez maintenant **comment copier une plage** depuis un classeur Excel, **exporter Excel vers PowerPoint**, et **convertir Excel en PPTX** avec Java. En suivant les six étapes ci‑dessus, vous pouvez automatiser la génération de rapports, créer des présentations à partir de données en temps réel et conserver la fonctionnalité du tableau croisé dynamique.

### Et après ?

* Explorez les variantes de **copy pivot table sheet**, comme la copie uniquement du cache du tableau croisé dynamique.  
* Combinez ce flux de travail avec **Aspose.Slides** pour ajouter des animations personnalisées ou du branding.  
* Automatisez le traitement par lots pour des dizaines de classeurs dans un job planifié.

N’hésitez pas à expérimenter avec les options et à adapter le code à votre propre chaîne de reporting. Si vous rencontrez des problèmes, la documentation Aspose.Cells for Java offre des informations plus détaillées sur `CopyOptions` et `ImageOrPrintOptions`. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment exporter Excel vers PowerPoint – Guide pas à pas](/cells/english/net/converting-excel-files-to-other-formats/how-to-export-excel-to-powerpoint-step-by-step-guide/)
- [Comment copier plusieurs colonnes dans Excel en utilisant Aspose.Cells Java : Guide complet](/cells/english/java/range-management/copy-multiple-columns-excel-aspose-cells-java/)
- [Comment convertir Excel en PowerPoint en utilisant Aspose.Cells pour .NET : Guide complet](/cells/english/net/workbook-operations/convert-excel-to-powerpoint-aspose-cells-dotnet/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}