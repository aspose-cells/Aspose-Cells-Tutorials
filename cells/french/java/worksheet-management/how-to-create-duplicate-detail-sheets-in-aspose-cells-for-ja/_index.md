---
category: general
date: 2026-08-17
description: Apprenez à créer des feuilles de détail dupliquées avec Aspose.Cells
  pour Java et à autoriser les noms de feuilles en double à l'aide de SmartMarkerProcessor.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- create duplicate detail sheets
- allow duplicate sheet names
language: fr
lastmod: 2026-08-17
og_description: Créez des feuilles de détail dupliquées dans Aspose.Cells pour Java
  et autorisez les noms de feuilles dupliqués. Suivez ce tutoriel complet pour des
  résultats instantanés.
og_image_alt: Generated Excel workbook showing multiple detail sheets with the same
  name
og_title: Créer des feuilles de détail dupliquées dans Aspose.Cells pour Java – guide
  étape par étape
schemas:
- author: Aspose
  dateModified: '2026-08-17'
  description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  headline: How to create duplicate detail sheets in Aspose.Cells for Java
  type: TechArticle
- description: Learn how to create duplicate detail sheets with Aspose.Cells for Java
    and allow duplicate sheet names using SmartMarkerProcessor.
  name: How to create duplicate detail sheets in Aspose.Cells for Java
  steps:
  - name: Load the master template workbook.
    text: Load the master template workbook.
  - name: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
    text: Configure `SmartMarkerProcessor` to **allow duplicate sheet names**.
  - name: Process the workbook so that a new detail sheet is created for each data
      group.
    text: Process the workbook so that a new detail sheet is created for each data
      group.
  - name: Save the resulting workbook that now contains duplicated detail sheets.
    text: Save the resulting workbook that now contains duplicated detail sheets.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Comment créer des feuilles de détail dupliquées dans Aspose.Cells pour Java
url: /fr/java/worksheet-management/how-to-create-duplicate-detail-sheets-in-aspose-cells-for-ja/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment créer des feuilles de détail dupliquées dans Aspose.Cells pour Java

Si vous devez **créer des feuilles de détail dupliquées** dans un classeur Excel, Aspose.Cells pour Java le rend simple. Ce tutoriel montre exactement comment autoriser des noms de feuilles en double lors de la génération de feuilles de détail avec SmartMarkerProcessor, afin de produire un classeur contenant plusieurs feuilles partageant le même nom.

Vous verrez un exemple complet et exécutable, une répartition de chaque option de configuration, ainsi que des astuces pour gérer les cas limites courants tels que les collisions de noms et les grands ensembles de données. Aucune référence externe n’est requise — tout ce dont vous avez besoin est inclus dans le code ci‑dessous.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* Kit de développement Java (JDK) 8 ou plus récent.  
* Maven ou Gradle pour gérer les dépendances.  
* Bibliothèque Aspose.Cells pour Java (version 23.9 ou ultérieure). Ajoutez la dépendance Maven suivante à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
</dependency>
```

* Un classeur modèle maître (`master_template.xlsx`) contenant une région Smart Marker pour les données détaillées.

## Vue d'ensemble de la solution

La solution suit quatre étapes logiques :

1. Charger le classeur modèle maître.  
2. Configurer `SmartMarkerProcessor` pour **autoriser les noms de feuilles en double**.  
3. Traiter le classeur afin qu'une nouvelle feuille de détail soit créée pour chaque groupe de données.  
4. Enregistrer le classeur résultant qui contient désormais des feuilles de détail dupliquées.

Chaque étape est expliquée en détail ci‑dessous, et le fichier source complet est fourni à la fin du guide.

## Étape 1 : Charger le classeur modèle maître

La première opération crée une instance `Workbook` qui représente le fichier modèle. Le modèle doit contenir un espace réservé Smart Marker (par ex., `&=DetailData`) qui indique au processeur où insérer les données.

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Load the master template workbook from the file system
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");
```

**Pourquoi c’est important :** Charger le modèle isole la mise en page et le formatage de la logique de génération des données, ce qui garde votre code propre et facilite la réutilisation du même modèle pour différents ensembles de données.

## Étape 2 : Configurer SmartMarkerProcessor pour autoriser les noms de feuilles en double

Par défaut, Aspose.Cells génère des noms de feuilles uniques lors de la création de feuilles de détail. Pour **autoriser les noms de feuilles en double**, définissez l’option `DetailSheetNewName` sur une valeur constante. Le processeur réutilisera ce nom pour chaque feuille générée.

```java
        // Create a SmartMarkerProcessor instance
        SmartMarkerProcessor processor = new SmartMarkerProcessor();

        // Enable duplicate detail sheet names by assigning a fixed name
        processor.getOptions().setDetailSheetNewName("DetailSheet");

        // Optional: if you want to keep the original sheet after processing, set this flag
        // processor.getOptions().setKeepOriginalDetailSheet(true);
```

**Pourquoi c’est important :** Le réglage de `DetailSheetNewName` indique au moteur de réutiliser le même nom pour chaque feuille de détail, ce qui satisfait directement la exigence d’**autoriser les noms de feuilles en double**. Cette approche est utile lorsque les outils en aval identifient les feuilles par leur position plutôt que par leur nom.

## Étape 3 : Traiter le classeur pour générer les feuilles de détail

Après la configuration, invoquez `process` sur le classeur. Le processeur lit la région Smart Marker, crée une nouvelle feuille pour chaque groupe de données et la remplit avec les lignes correspondantes.

```java
        // Process the workbook; this creates the duplicate detail sheets
        processor.process(workbook);
```

**Pourquoi c’est important :** L’appel `process` effectue le travail lourd — analyse des Smart Markers, clonage de la feuille modèle et insertion des données. Comme l’option `DetailSheetNewName` est déjà définie, chaque nouvelle feuille reçoit le même nom, produisant ainsi des noms de feuilles en double dans le fichier final.

## Étape 4 : Enregistrer le classeur résultant

Enfin, écrivez le classeur modifié dans un nouveau fichier. Le fichier de sortie contiendra autant d’onglets « DetailSheet » qu’il y a de groupes de données.

```java
        // Save the workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

**Pourquoi c’est important :** L’enregistrement du fichier finalise les modifications apportées par le processeur. Le classeur résultant peut être ouvert dans Microsoft Excel, LibreOffice ou toute autre application de tableur prenant en charge le format XLSX.

## Code source complet

En assemblant toutes les pièces, voici le programme complet que vous pouvez copier, coller et exécuter :

```java
import com.aspose.cells.*;

public class DuplicateDetailSheet {
    public static void main(String[] args) throws Exception {
        // Step 1: Load the master template workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/master_template.xlsx");

        // Step 2: Create a SmartMarkerProcessor and allow duplicate detail sheet names
        SmartMarkerProcessor processor = new SmartMarkerProcessor();
        processor.getOptions().setDetailSheetNewName("DetailSheet"); // same name allowed for each detail sheet

        // Step 3: Process the workbook to generate the detail sheets
        processor.process(workbook);

        // Step 4: Save the resulting workbook with duplicated detail sheets
        workbook.save("YOUR_DIRECTORY/duplicate_detail.xlsx");
    }
}
```

### Résultat attendu

Lorsque vous ouvrez `duplicate_detail.xlsx`, vous verrez plusieurs onglets nommés **DetailSheet**. Chaque onglet contient l’ensemble de données correspondant à un groupe Smart Marker spécifique dans le modèle. La mise en page, le formatage et les formules du modèle maître sont conservés sur chaque feuille dupliquée.

## Gestion des problèmes courants

| Problème | Explication | Solution |
|----------|-------------|----------|
| Excel affiche un avertissement concernant les noms de feuilles en double | Excel autorise les noms en double mais peut afficher un avertissement à l'ouverture du fichier. | L'avertissement est sans danger ; le classeur fonctionne correctement. Si vous préférez supprimer l'avertissement, renommez les feuilles après le traitement en utilisant `Workbook.getWorksheets().get(i).setName("DetailSheet" + i);`. |
| Les grands ensembles de données entraînent une forte utilisation de la mémoire | Chaque feuille dupliquée crée une copie complète du modèle, ce qui peut consommer de la RAM. | Activez le mode streaming avec `Workbook.setMemorySetting(MemorySetting.MEMORY_PREFERENCE);` avant de charger le modèle. |
| Région Smart Marker introuvable | Le processeur ne peut pas localiser `&=DetailData` dans le modèle. | Vérifiez que la syntaxe du placeholder correspond à la source de données et que la feuille du modèle n'est pas masquée. |

## Astuce pro : personnaliser le schéma de nommage des duplicatas

Si vous avez besoin d’un schéma de nommage prévisible tout en autorisant les duplicatas, combinez un nom de base avec un indice :

```java
processor.getOptions().setDetailSheetNewName("DetailSheet_{0}");
```

Le placeholder `{0}` est remplacé par l’indice de la feuille, produisant des noms comme `DetailSheet_1`, `DetailSheet_2`, etc. Cela satisfait toujours l’exigence d’**autoriser les noms de feuilles en double** car le nom de base reste constant.

## Étapes suivantes

Maintenant que vous pouvez **créer des feuilles de détail dupliquées**, vous pourriez explorer les sujets suivants :

* **Remplir les feuilles de détail avec des images** – utilisez des objets `Picture` pour intégrer des logos ou des graphiques.  
* **Appliquer un formatage conditionnel** – ajoutez des règles `FormatCondition` pour mettre en évidence les lignes en fonction des valeurs.  
* **Exporter en PDF** – appelez `workbook.save("output.pdf", SaveFormat.PDF);` pour générer une version PDF des feuilles dupliquées.  

Chacune de ces extensions s’appuie sur le même flux de travail Smart Marker démontré ici, vous permettant d’automatiser en toute confiance des tâches de reporting Excel complexes.

---

*Vous avez appris comment créer des feuilles de détail dupliquées dans Aspose.Cells pour Java et comment autoriser les noms de feuilles en double à l’aide de SmartMarkerProcessor. Appliquez le code, adaptez le modèle et intégrez la technique dans vos pipelines de reporting.*

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer et accéder aux feuilles Excel, ajouter des signets PDF avec Aspose.Cells pour Java](/cells/english/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Créer, accéder aux feuilles Excel, ajouter des signets PDF Aspose Cells Java](/cells/german/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)
- [Créer, accéder aux feuilles Excel, ajouter des signets PDF Aspose Cells Java](/cells/french/java/workbook-operations/create-access-excel-sheets-add-pdf-bookmarks-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}