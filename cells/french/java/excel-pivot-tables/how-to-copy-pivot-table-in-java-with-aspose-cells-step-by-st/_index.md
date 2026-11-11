---
category: general
date: 2026-10-20
description: Apprenez à copier un tableau croisé dynamique avec Aspose.Cells en Java.
  Ce tutoriel montre comment copier une plage vers une nouvelle feuille et dupliquer
  en toute sécurité la feuille du tableau croisé dynamique.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to copy pivot table
- copy range to new sheet
- duplicate pivot table sheet
language: fr
lastmod: 2026-10-20
og_description: Comment copier un tableau croisé dynamique avec Aspose.Cells en Java.
  Suivez ce guide pour copier une plage vers une nouvelle feuille et dupliquer la
  feuille du tableau croisé dynamique sans perdre de données.
og_image_alt: Screenshot showing how to copy pivot table from one worksheet to another
  in a Java program
og_title: Comment copier un tableau croisé dynamique en Java – tutoriel complet Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-20'
  description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  headline: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
- description: Learn how to copy pivot table using Aspose.Cells in Java. This tutorial
    shows how to copy range to new sheet and duplicate pivot table sheet safely.
  name: How to copy pivot table in Java with Aspose.Cells – step‑by‑step guide
  steps:
  - name: Load the workbook that holds the original pivot table.
    text: Load the workbook that holds the original pivot table.
  - name: Identify the exact range that includes the pivot table.
    text: Identify the exact range that includes the pivot table.
  - name: Create a new worksheet that will receive the copied data.
    text: Create a new worksheet that will receive the copied data.
  - name: Use the `Range.copy` method to transfer the range to the new sheet.
    text: Use the `Range.copy` method to transfer the range to the new sheet.
  - name: Save the workbook to a new file.
    text: Save the workbook to a new file.
  type: HowTo
tags:
- Aspose.Cells
- Java
- Excel automation
title: Comment copier un tableau croisé dynamique en Java avec Aspose.Cells – guide
  étape par étape
url: /fr/java/excel-pivot-tables/how-to-copy-pivot-table-in-java-with-aspose-cells-step-by-st/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment copier un tableau croisé dynamique en Java avec Aspose.Cells – guide étape par étape

Si vous avez besoin de **comment copier un tableau croisé dynamique** dans une application Java, ce guide vous accompagne pas à pas. Que vous construisiez un moteur de reporting ou automatisiez une migration de données, vous verrez comment copier une plage vers une nouvelle feuille tout en préservant la définition et les données du tableau croisé dynamique.

Copier un tableau croisé dynamique peut sembler risqué car le cache sous‑jacent et les paramètres de champ sont souvent perdus. Ce tutoriel montre une approche fiable avec Aspose.Cells, présente le code complet exécutable et explique pourquoi chaque ligne est importante. À la fin, vous pourrez dupliquer la feuille du tableau croisé dynamique en quelques secondes.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* Java 8 ou une version plus récente installée.
* Aspose.Cells for Java (version 23.10 ou ultérieure) ajouté au classpath de votre projet.
* Un classeur source (`source.xlsx`) contenant un tableau croisé dynamique dans la plage `A1:G20`.
* Une connaissance de base de Java et des concepts Excel.

Aucune bibliothèque supplémentaire n’est requise ; Aspose.Cells gère toutes les opérations Excel en interne.

## Comment copier un tableau croisé dynamique – stratégie globale

L’idée principale est simple :

1. Charger le classeur qui contient le tableau croisé dynamique original.
2. Identifier la plage exacte qui inclut le tableau croisé dynamique.
3. Créer une nouvelle feuille de calcul qui recevra les données copiées.
4. Utiliser la méthode `Range.copy` pour transférer la plage vers la nouvelle feuille.  
   Cette méthode copie automatiquement le cache du tableau croisé dynamique, de sorte que le tableau reste fonctionnel.
5. Enregistrer le classeur dans un nouveau fichier.

Comme l’opération de copie agit au niveau de la plage, la **feuille du tableau croisé dynamique dupliquée** conserve toutes les configurations de champs, filtres et éléments calculés.

## Étape 1 : Charger le classeur source

```java
// Import Aspose.Cells classes
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // Load the source workbook that contains the pivot table
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");
```

*Pourquoi c’est important* : Charger le classeur vous donne accès à ses feuilles, cellules et au cache du tableau croisé dynamique. Aspose.Cells lit le fichier complet en mémoire, ce qui rend les opérations suivantes rapides et thread‑safe.

## Étape 2 : Définir la plage source contenant le tableau croisé dynamique

```java
        // Locate the first worksheet (index 0) and create a range covering the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)               // first sheet
                                    .getCells()
                                    .createRange("A1:G20"); // adjust if your pivot table is larger
```

*Pourquoi c’est important* : L’appel `createRange` indique à Aspose.Cells exactement quelles cellules copier. Inclure l’ensemble de la zone du tableau croisé dynamique garantit que les lignes de cache cachées sont également transférées. Si vous omettez une partie du cache, le tableau croisé dynamique copié apparaîtrait vide.

## Étape 3 : Ajouter une feuille de destination pour les données copiées

```java
        // Add a new worksheet that will hold the duplicated pivot table
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");
```

*Pourquoi c’est important* : Ajouter une feuille dédiée isole le tableau croisé dynamique copié de l’original, facilitant la comparaison des résultats ou l’utilisation de la feuille comme modèle pour un traitement ultérieur.

## Étape 4 : Copier la plage vers la feuille de destination (le tableau croisé dynamique est préservé)

```java
        // Copy the defined range to cell A1 of the new worksheet
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));
```

*Pourquoi c’est important* : La méthode `copy` ne copie pas seulement les valeurs et le format des cellules, elle réplique également le cache du tableau croisé dynamique. C’est l’étape clé qui vous permet de **dupliquer la feuille du tableau croisé dynamique** sans perdre aucune fonctionnalité.

## Étape 5 : Enregistrer le classeur avec la plage copiée

```java
        // Persist the workbook to a new file
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

*Pourquoi c’est important* : L’enregistrement crée un nouveau fichier Excel (`result.xlsx`) contenant à la fois l’original et la feuille du tableau croisé dynamique dupliquée. Vous pouvez maintenant ouvrir le fichier dans Excel pour vérifier que le tableau croisé dynamique fonctionne exactement comme avant.

## Exemple complet, exécutable

En assemblant tous les éléments, voici le programme complet que vous pouvez copier‑coller dans votre IDE :

```java
import com.aspose.cells.*;

public class PivotCopyDemo {
    public static void main(String[] args) throws Exception {
        // 1. Load the source workbook
        Workbook workbook = new Workbook("YOUR_DIRECTORY/source.xlsx");

        // 2. Define the source range that contains the pivot table
        Range sourceRange = workbook.getWorksheets()
                                    .get(0)
                                    .getCells()
                                    .createRange("A1:G20");

        // 3. Add a destination worksheet for the copied data
        Worksheet destinationSheet = workbook.getWorksheets().add("CopyResult");

        // 4. Copy the range to the destination worksheet (pivot table is preserved)
        sourceRange.copy(destinationSheet.getCells().createRange("A1"));

        // 5. Save the workbook with the copied range
        workbook.save("YOUR_DIRECTORY/result.xlsx");
    }
}
```

### Résultat attendu

* L’ouverture de `result.xlsx` montre deux feuilles de calcul :
  * **Sheet1** – les données et le tableau croisé dynamique d’origine.
  * **CopyResult** – une duplication exacte du tableau croisé dynamique, pleinement fonctionnelle.
* Tous les champs du tableau croisé dynamique, filtres et éléments calculés se comportent exactement comme dans la source.

Si vous modifiez le tableau croisé dynamique source après la copie, la feuille dupliquée **ne** reflétera pas ces changements car le cache a été dupliqué au moment de la copie. Cette isolation est souvent souhaitable lorsque vous avez besoin d’un instantané du rapport.

## Pièges courants et comment les éviter

| Problème | Pourquoi cela se produit | Solution |
|----------|--------------------------|----------|
| **Le tableau croisé dynamique apparaît vide** | La plage copiée a omis les lignes de cache cachées. | Assurez‑vous que la plage inclut l’ensemble du cache (généralement quelques lignes sous le tableau visible). |
| **Le nom de la feuille de destination existe déjà** | `add("CopyResult")` lève une exception si le nom est déjà utilisé. | Utilisez `workbook.getWorksheets().addUniqueName("CopyResult")` ou vérifiez `contains` avant d’ajouter. |
| **Erreurs de chemin de fichier** | `YOUR_DIRECTORY` incorrect entraîne une `FileNotFoundException`. | Utilisez des chemins absolus ou `Paths.get(...).toAbsolutePath()` de Java pour résoudre les emplacements. |
| **Ralentissement des performances sur de gros classeurs** | Copier d’énormes plages duplique des cellules inutiles. | Limitez la plage à la zone exacte du tableau croisé dynamique, ou utilisez `Range.copy` avec `CopyOptions` pour ignorer le formatage si ce n’est pas nécessaire. |

## Astuce pro : Utiliser `CopyOptions` pour un contrôle plus fin

Si vous avez uniquement besoin des données du tableau croisé dynamique et souhaitez ignorer le formatage des cellules, vous pouvez passer un objet `CopyOptions` :

```java
CopyOptions options = new CopyOptions();
options.setCopyStyle(false);        // skip styles
options.setCopyMerged(true);        // keep merged cells
sourceRange.copy(destinationSheet.getCells().createRange("A1"), options);
```

Cela réduit la taille du fichier de la feuille dupliquée et accélère l’opération de copie, surtout pour les gros classeurs.

## Comment copier une plage vers une nouvelle feuille sans perdre les formules

L’exemple ci‑dessus copie déjà les formules car `Range.copy` les préserve par défaut. Si vous ne voulez que les valeurs (par ex., pour figer l’état actuel), définissez `options.setPasteType(PasteType.VALUES)`.

```java
CopyOptions opt = new CopyOptions();
opt.setPasteType(PasteType.VALUES);
sourceRange.copy(destinationSheet.getCells().createRange("A1"), opt);
```

La feuille de destination contient maintenant des valeurs statiques, mais le tableau croisé dynamique fonctionnera toujours car son cache fait partie de la plage.

## Récapitulatif de la solution

* **Comment copier un tableau croisé dynamique** – charger le classeur, définir la plage exacte, ajouter une nouvelle feuille, copier la plage et enregistrer.
* Le processus montre également **copier une plage vers une nouvelle feuille** et comment **dupliquer la feuille du tableau croisé dynamique** en toute sécurité.
* Vous pouvez affiner la copie avec `CopyOptions` pour des scénarios de performance ou de valeurs uniquement.

## Prochaines étapes et sujets associés

* **Actualiser le cache du tableau croisé dynamique par programme** – utilisez `PivotTable.refreshData()` après avoir mis à jour les données sources.
* **Exporter le tableau croisé dynamique en PDF** – combinez cette technique de copie avec `PdfSaveOptions` pour créer des rapports instantanés.
* **Automatiser la duplication de plusieurs feuilles** – parcourez toutes les feuilles et appliquez la même logique de copie.

Expérimentez ces variantes pour adapter le modèle à votre pipeline de reporting spécifique. Si vous rencontrez des cas particuliers, comme des sources de données externes ou des tableaux croisés dynamiques pilotés par VBA, la même approche de copie de plage fonctionne, mais vous devrez peut‑être copier également les objets de connexion sous‑jacents.

---

*Bon codage ! Si ce tutoriel vous a aidé à apprendre **comment copier un tableau croisé dynamique**, n’hésitez pas à le partager avec vos collègues ou à contribuer aux améliorations.*

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment copier une plage et préserver un tableau croisé dynamique en Java](/cells/english/java/excel-pivot-tables/how-to-copy-range-and-preserve-a-pivot-table-in-java/)
- [Créer un nouveau classeur en Java – Guide complet pour copier un tableau croisé dynamique](/cells/english/java/excel-pivot-tables/create-new-workbook-in-java-full-guide-to-copy-pivot-table/)
- [Copier un tableau croisé dynamique entre classeurs – Guide Java étape par étape](/cells/english/java/excel-pivot-tables/copy-pivot-table-between-workbooks-step-by-step-java-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}