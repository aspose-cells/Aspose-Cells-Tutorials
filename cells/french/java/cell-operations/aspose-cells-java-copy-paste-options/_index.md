---
date: '2026-02-22'
description: Apprenez à automatiser les rapports Excel avec Aspose.Cells en Java en
  utilisant CopyOptions et PasteOptions pour conserver la précision des formules et
  coller uniquement les valeurs visibles.
keywords:
- Aspose.Cells Java
- CopyOptions ReferToDestinationSheet
- PasteOptions Excel
title: Automatiser les rapports Excel – Maîtriser CopyOptions et PasteOptions en Java
  avec Aspose.Cells
url: /fr/java/cell-operations/aspose-cells-java-copy-paste-options/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Automatiser les rapports Excel avec Aspose.Cells : CopyOptions & PasteOptions en Java

Vous cherchez à **automatiser les rapports Excel** en utilisant Java ? Avec Aspose.Cells, vous pouvez copier, coller et ajuster les formules de manière programmatique afin que vos rapports restent précis et que seules les données dont vous avez besoin soient transférées. Dans ce tutoriel, nous passerons en revue deux fonctionnalités essentielles—**CopyOptions.ReferToDestinationSheet** et **PasteOptions**—qui vous permettent de préserver les références de formules et de coller les valeurs uniquement à partir des cellules visibles.

## Réponses rapides
- **Que fait `CopyOptions.ReferToDestinationSheet` ?** Ajuste les formules pour qu'elles pointent vers la feuille de destination lors de la copie des données.  
- **Comment coller uniquement les cellules visibles ?** Définissez `PasteOptions.setOnlyVisibleCells(true)` avec `PasteType.VALUES`.  
- **Quelle version de la bibliothèque est requise ?** Aspose.Cells 25.3 ou ultérieure.  
- **Ai-je besoin d'une licence pour la production ?** Oui, une licence permanente ou temporaire supprime les limites d'évaluation.  
- **Puis-je utiliser Maven ou Gradle ?** Les deux sont pris en charge ; voyez les extraits de dépendances ci‑dessous.

## Qu’est‑ce que « automatiser les rapports Excel » ?
Automatiser les rapports Excel signifie générer, consolider et mettre en forme des classeurs Excel de manière programmatique, éliminant les étapes manuelles de copier‑coller et réduisant les erreurs. Aspose.Cells offre une API riche qui permet aux développeurs Java de manipuler des feuilles de calcul à grande échelle.

## Pourquoi utiliser CopyOptions et PasteOptions pour les rapports ?
- **Conserver l'intégrité des formules** lors du déplacement de données entre les feuilles.  
- **Exclure les lignes/colonnes masquées** pour garder les rapports clairs et ciblés.  
- **Améliorer les performances** en copiant uniquement les données nécessaires plutôt que des plages entières.

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
- **Free Trial** – Ensemble complet de fonctionnalités pour l'évaluation.  
- **Temporary License** – Supprime les limitations de l'essai pendant vos tests.  
- **Permanent License** – Recommandée pour les charges de travail en production.

Initialisez Aspose.Cells dans votre code Java :

```java
import com.aspose.cells.Workbook;

Workbook workbook = new Workbook("path/to/your/excel/file.xlsx");
```

## Guide étape par étape

### 1. CopyOptions avec ReferToDestinationSheet

#### Vue d'ensemble
Définir `CopyOptions.ReferToDestinationSheet` sur `true` réécrit les références de formules afin qu'elles pointent vers la nouvelle feuille après l'opération de copie.

#### Étape 1 : Initialiser le classeur et les feuilles de calcul
```java
import com.aspose.cells.Workbook;
import com.aspose.cells.Worksheet;

String dataDir = "YOUR_DATA_DIRECTORY";
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Étape 2 : Configurer CopyOptions
```java
import com.aspose.cells.CopyOptions;

CopyOptions options = new CopyOptions();
options.setReferToDestinationSheet(true); // Adjust formulas to the destination sheet
```

#### Étape 3 : Exécuter l'opération de copie
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), options, null);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Pourquoi c’est important* : les formules qui faisaient initialement référence à `Sheet1` référenceront maintenant correctement `DestSheet`, garantissant la fiabilité de vos rapports automatisés.

**Conseil de dépannage** : Si les formules font encore référence à l'ancienne feuille, assurez‑vous que `setReferToDestinationSheet(true)` est appelé **avant** la copie.

### 2. PasteOptions pour les valeurs uniquement à partir des cellules visibles

#### Vue d'ensemble
`PasteOptions` vous permet de définir ce qui est collé. Utiliser `PasteType.VALUES` avec `onlyVisibleCells=true` copie uniquement les valeurs affichées, en ignorant les lignes/colonnes masquées et le formatage.

#### Étape 1 : Initialiser le classeur et les feuilles de calcul
```java
Workbook wb = new Workbook(dataDir + "/book1.xlsx");
Worksheet source = wb.getWorksheets().get(0);
Worksheet destination = wb.getWorksheets().add("DestSheet");
```

#### Étape 2 : Configurer PasteOptions
```java
import com.aspose.cells.PasteOptions;
import com.aspose.cells.PasteType;

PasteOptions pasteOptions = new PasteOptions();
pasteOptions.setPasteType(PasteType.VALUES); // Copy only values
pasteOptions.setOnlyVisibleCells(true); // Include only visible cells
```

#### Étape 3 : Exécuter l'opération de collage
```java
destination.getCells().copyRows(source.getCells(), 0, 0, source.getCells().getMaxDisplayRange().getRowCount(), null, pasteOptions);
wb.save("YOUR_OUTPUT_DIRECTORY/destination.xlsx");
```
*Pourquoi c’est important* : idéal pour extraire des données filtrées ou générer des rapports propres sans lignes masquées ni bruit de formatage.

**Conseil de dépannage** : Vérifiez que les lignes/colonnes sont réellement masquées dans Excel avant de copier ; sinon, elles seront incluses.

## Applications pratiques
1. **Financial Consolidation** – Fusionner les feuilles mensuelles dans un classeur maître tout en conservant la précision de toutes les formules.  
2. **Filtered Data Export** – Extraire uniquement les lignes visibles d'un tableau filtré vers une feuille de synthèse.  
3. **Scheduled Report Generation** – Automatiser la création nocturne de rapports Excel avec des valeurs de cellules précises et des références correctes.

## Considérations de performance
- **Libérez les classeurs** une fois terminé (`wb.dispose();`) pour libérer les ressources natives.  
- **Batch Operations** – Regroupez plusieurs appels de copie/collage pour réduire la surcharge.  
- **Monitor Memory** – Les grands classeurs peuvent nécessiter une augmentation du tas (`-Xmx2g`).

## Questions fréquemment posées

**Q1 : À quoi sert `CopyOptions.ReferToDestinationSheet` ?**  
R : Il réécrit les références de formules afin qu'elles pointent vers la feuille de destination après une copie, garantissant que les formules de reporting restent correctes.

**Q2 : How do I paste only visible cells?**  
R : Définissez `PasteOptions.setOnlyVisibleCells(true)` et choisissez `PasteType.VALUES`.

**Q3 : Can I use Aspose.Cells without purchasing a license?**  
R : Oui, un essai gratuit ou une licence temporaire est disponible pour l'évaluation, mais une licence permanente est requise pour la production.

**Q4 : Why are some references still wrong after copying?**  
R : Vérifiez que `ReferToDestinationSheet` est activé **avant** l'opération de copie et que les formules sources ne contiennent pas de liens vers des classeurs externes.

**Q5 : What memory‑management best practices should I follow?**  
R : Libérez les objets `Workbook` une fois terminés, traitez les gros fichiers par morceaux et surveillez l'utilisation du tas JVM.

**Q6 : Is it possible to combine CopyOptions and PasteOptions in one operation?**  
R : Oui, vous pouvez les chaîner en copiant d'abord avec `CopyOptions` puis en appliquant `PasteOptions` sur la plage cible.

## Ressources
- **Documentation** : [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)  
- **Download** : [Aspose.Cells Releases for Java](https://releases.aspose.com/cells/java/)  
- **Purchase** : [Buy Aspose.Cells](https://purchase.aspose.com/buy)  
- **Free Trial** : [Aspose.Cells Free Trial](https://releases.aspose.com/cells/java/)  
- **Temporary License** : [Apply for a Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Support Forum** : [Aspose Support](https://forum.aspose.com/c/cells)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}

---

**Dernière mise à jour** : 2026-02-22  
**Testé avec** : Aspose.Cells 25.3 for Java  
**Auteur** : Aspose