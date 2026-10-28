---
date: '2026-10-28'
description: Apprenez à coller des valeurs en utilisant les options de copier-coller
  d'Aspose.Cells en Java, avec du code étape par étape, la configuration de la dépendance
  Maven et des conseils de licence.
keywords:
- how to paste values
- aspose cells maven dependency
- java generate excel report
- aspose cells license java
- copyoptions refertodestinationsheet
lastmod: '2026-10-28'
og_description: Apprenez à coller des valeurs en utilisant les options de copier-coller
  d'Aspose.Cells en Java, avec du code étape par étape, la configuration de la dépendance
  Maven et des conseils de licence.
og_image_alt: Developer guide showing Java code for copying and pasting Excel data
  with Aspose.Cells
og_title: Comment coller des valeurs avec les options de copier-coller d'Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to paste values using Aspose.Cells copy and paste options
    in Java, with step‑by‑step code, Maven dependency setup, and licensing tips.
  headline: How to paste values with Aspose.Cells copy and paste options
  type: TechArticle
- questions:
  - answer: It rewrites formula references so they point to the destination sheet
      after a copy, ensuring reporting formulas stay correct.
    question: What is `CopyOptions.ReferToDestinationSheet` used for?
  - answer: Set `PasteOptions.setOnlyVisibleCells(true)` and choose `PasteType.VALUES`.
    question: How do I paste only visible cells?
  - answer: Yes, a free trial or temporary license is available for evaluation, but
      a permanent license is required for production.
    question: Can I use Aspose.Cells without purchasing a license?
  - answer: Double‑check that `ReferToDestinationSheet` is enabled **before** the
      copy operation and that the source formulas don’t contain external workbook
      links.
    question: Why are some references still wrong after copying?
  - answer: Dispose of `Workbook` objects when finished, process large files in chunks,
      and monitor JVM heap usage.
    question: What memory‑management best practices should I follow?
  type: FAQPage
tags:
- paste values
- Aspose.Cells
- Java Excel automation
- copy options
- paste options
title: Comment coller des valeurs avec les options de copier-coller d'Aspose.Cells
url: /fr/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment coller des valeurs avec les options de copie et de collage d'Aspose.Cells

Automatiser la génération de rapports Excel en Java signifie que vous pouvez créer, consolider et mettre en forme des classeurs sans jamais ouvrir Excel manuellement. Avec **Aspose.Cells**, vous avez un contrôle total sur les formules, les lignes masquées et les valeurs des cellules, de sorte que vos rapports restent précis et légers. Dans ce tutoriel, vous apprendrez à utiliser **CopyOptions.ReferToDestinationSheet** pour maintenir les formules correctes et **PasteOptions** pour coller uniquement les valeurs visibles dont vous avez besoin.

## Réponses rapides
- **Que fait `CopyOptions.ReferToDestinationSheet` ?** Il réécrit les formules afin qu'elles pointent vers la feuille de destination après une opération de copie.  
- **Comment coller uniquement les cellules visibles ?** Appelez `PasteOptions.setOnlyVisibleCells(true)` avec `PasteType.VALUES`.  
- **Quelle version de la bibliothèque est requise ?** Aspose.Cells 25.3 ou ultérieure.  
- **Ai-je besoin d'une licence pour la production ?** Oui – une licence permanente ou temporaire supprime les limites d'évaluation.  
- **Puis-je utiliser Maven ou Gradle ?** Les deux sont pris en charge ; voir les extraits de dépendances ci‑dessous.

## Qu'est-ce que « automatiser la génération de rapports Excel » ?
Automatiser la génération de rapports Excel signifie créer et mettre à jour des classeurs Excel de manière programmatique, vous permettant de créer, fusionner et mettre en forme des rapports sans copier‑coller manuel, ce qui réduit les erreurs et fait gagner des heures de travail répétitif. Cette approche est idéale pour les tâches batch planifiées, les tableaux de bord pilotés par les données et les pipelines de consolidation financière.

## Pourquoi utiliser CopyOptions et PasteOptions pour les rapports ?
Ces deux classes vous permettent de conserver les références de formules intactes lors de la copie de données **et** d'extraire uniquement les cellules visibles après filtrage ou masquage de lignes. Les utiliser ensemble réduit la quantité de données transférées jusqu'à 80 % dans les scénarios typiques de tableaux filtrés et garantit que les formules continuent de se calculer correctement dans la feuille de destination.

## Prérequis
- Java 8 ou supérieur.  
- Maven ou Gradle pour la gestion des dépendances.  
- Aspose.Cells 25.3+ (licence d'essai, temporaire ou permanente).  

## Configurer Aspose.Cells pour Java

Ajoutez la bibliothèque à votre projet avec l'une des options suivantes :

**Maven**  
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle**  
```gradle
implementation 'com.aspose:aspose-cells:25.3'
```

### Acquisition de licence
- **Essai gratuit** – ensemble complet de fonctionnalités pour l'évaluation.  
- **Licence temporaire** – supprime les limites d'essai pendant vos tests.  
- **Licence permanente** – recommandée pour les charges de travail en production.

Initialisez Aspose.Cells dans votre code Java :  
```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Guide étape par étape

### 1. copyOptions avec referToDestinationSheet

#### Vue d'ensemble
`CopyOptions` est l'objet de configuration d'Aspose.Cells qui contrôle la façon dont les formules et les références de cellules sont gérées lors d'une opération de copie. Définir `CopyOptions.ReferToDestinationSheet` à `true` réécrit les références de formules afin qu'elles pointent vers la nouvelle feuille après l'opération de copie.

#### Étape 1 : initialiser le classeur et les feuilles de calcul  
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Étape 2 : configurer copyOptions  
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Étape 3 : exécuter l'opération de copie  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Pourquoi c'est important* : Les formules qui faisaient initialement référence à `Sheet1` référenceront maintenant correctement `DestSheet`, ce qui maintient la fiabilité de vos rapports automatisés.

**Conseil de dépannage** : Si les formules font encore référence à l'ancienne feuille, assurez‑vous que `setReferToDestinationSheet(true)` est appelé **avant** la copie.

### 2. pasteOptions pour valeurs‑uniquement à partir des cellules visibles

#### Vue d'ensemble
`PasteOptions` est l'objet de paramètres d'Aspose.Cells qui définit ce qui est collé. Utiliser `PasteType.VALUES` avec `onlyVisibleCells=true` copie uniquement les valeurs affichées, en ignorant les lignes/colonnes masquées et le formatage.

#### Étape 1 : initialiser le classeur et les feuilles de calcul  
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Étape 2 : configurer pasteOptions  
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Étape 3 : exécuter l'opération de collage  
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```  
*Pourquoi c'est important* : Idéal pour extraire des données filtrées ou générer des rapports propres sans lignes masquées ni bruit de formatage.

**Conseil de dépannage** : Vérifiez que les lignes/colonnes sont réellement masquées dans Excel avant de copier ; sinon, elles seront incluses.

## Applications pratiques
1. **Consolidation financière** – fusionner les feuilles mensuelles dans un classeur maître tout en conservant toutes les formules précises.  
2. **Exportation de données filtrées** – extraire uniquement les lignes visibles d'un tableau filtré vers une feuille de synthèse.  
3. **Génération de rapports planifiée** – automatiser la création nocturne de rapports Excel avec des valeurs de cellules précises et des références correctes.

## Considérations de performance
- **Libérez les classeurs** une fois terminés (`wb.dispose();`) pour libérer les ressources natives.  
- **Opérations par lots** – regroupez plusieurs appels de copie/collage pour réduire la surcharge.  
- **Surveillez la mémoire** – les grands classeurs peuvent nécessiter une augmentation du tas (`-Xmx2g`).  
- Aspose.Cells prend en charge **plus de 50 formats d'entrée et de sortie** et peut traiter des classeurs contenant **jusqu'à 2 millions de lignes** sans charger le fichier complet en mémoire, offrant des performances à haut débit pour les charges de travail d'entreprise.

## Questions fréquentes

**Q : À quoi sert `CopyOptions.ReferToDestinationSheet` ?**  
R : Il réécrit les références de formules afin qu'elles pointent vers la feuille de destination après une copie, garantissant que les formules de rapport restent correctes.

**Q : Comment coller uniquement les cellules visibles ?**  
R : Définissez `PasteOptions.setOnlyVisibleCells(true)` et choisissez `PasteType.VALUES`.

**Q : Puis-je utiliser Aspose.Cells sans acheter de licence ?**  
R : Oui, un essai gratuit ou une licence temporaire est disponible pour l'évaluation, mais une licence permanente est requise pour la production.

**Q : Pourquoi certaines références sont‑elles encore incorrectes après la copie ?**  
R : Vérifiez que `ReferToDestinationSheet` est activé **avant** l'opération de copie et que les formules source ne contiennent pas de liens vers des classeurs externes.

**Q : Quelles bonnes pratiques de gestion de la mémoire devrais‑je suivre ?**  
R : Libérez les objets `Workbook` une fois terminés, traitez les gros fichiers par morceaux et surveillez l'utilisation du tas JVM.

**Q : Est‑il possible de combiner CopyOptions et PasteOptions en une seule opération ?**  
R : Oui, vous pouvez les enchaîner en copiant d'abord avec `CopyOptions` puis en appliquant `PasteOptions` sur la plage cible.

## Ressources
- **Documentation** : [Référence Aspose.Cells Java](https://reference.aspose.com/cells/java/)  
- **Téléchargement** : [Versions Aspose.Cells pour Java](https://releases.aspose.com/cells/java/)  
- **Achat** : [Acheter Aspose.Cells](https://purchase.aspose.com/buy)  
- **Essai gratuit** : [Essai gratuit Aspose.Cells](https://releases.aspose.com/cells/java/)  
- **Licence temporaire** : [Demander une licence temporaire](https://purchase.aspose.com/temporary-license/)  
- **Forum de support** : [Support Aspose](https://forum.aspose.com/c/cells)

**Dernière mise à jour** : 2026-10-28  
**Testé avec** : Aspose.Cells 25.3 pour Java  
**Auteur** : Aspose

## Tutoriels associés

- [Lire un fichier Excel Java – Maîtriser la manipulation des cellules du classeur avec Aspose.Cells](/cells/java/cell-operations/aspose-cells-java-workbook-cell-manipulation/)
- [Ajouter des données à une cellule dans Excel avec Aspose.Cells pour Java](/cells/java/cell-operations/aspose-cells-java-set-active-cell-excel/)
- [Convertir les indices de ligne et de colonne des cellules Excel avec Aspose.Cells Java](/cells/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}