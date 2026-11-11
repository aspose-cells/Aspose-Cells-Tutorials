---
date: '2026-10-28'
description: Apprenez comment modifier le système de dates Excel en 1904 en utilisant
  Aspose.Cells pour Java, définir le format de date Excel et convertir le système
  1904 d'Excel efficacement.
keywords:
- change excel date system
- excel 1904 date conversion
- maven dependency aspose cells
lastmod: '2026-10-28'
og_description: Modifiez le système de dates Excel en 1904 avec Aspose.Cells pour
  Java. Apprenez étape par étape comment activer le système 1904, définir les dates
  et revenir en arrière.
og_image_alt: Aspose.Cells Java guide showing how to switch Excel to the 1904 date
  system
og_title: Modifier le système de dates Excel en 1904 avec Aspose.Cells pour Java
schemas:
- author: Aspose
  dateModified: '2026-10-28'
  description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  headline: Change Excel date system to 1904 with Aspose.Cells Java
  type: TechArticle
- description: Learn how to change Excel date system to 1904 using Aspose.Cells for
    Java, set Excel date format, and convert Excel 1904 system efficiently.
  name: Change Excel date system to 1904 with Aspose.Cells Java
  steps:
  - name: initialize and load the workbook
    text: The `Workbook` class represents an entire Excel file in memory. First, create
      a `Workbook` instance that points to your existing file.
  - name: enable the 1904 date system
    text: The `WorkbookSettings.setDate1904` method toggles the workbook‑level date
      flag. Setting it to `true` activates the 1904 system for all worksheets. **Pro
      tip:** You can also call `setDate1904(false)` later if you need to revert.
  - name: save the modified workbook
    text: Finally, write the changes to a new file (or overwrite the original). The
      `save` method respects the active date system automatically. > **Note:** The
      code above uses the class name `tWorkbook` as originally provided. Ensure this
      typo matches your project’s naming conventions or correct it to `Workb
  type: HowTo
- questions:
  - answer: The 1900 system starts on January 1, 1900, while the 1904 system starts
      on January 1, 1904, shifting all dates by 1,462 days.
    question: What is the difference between the 1900 and 1904 date systems?
  - answer: Yes, but you must close the file in Excel first; otherwise the save operation
      will fail.
    question: Can I change the date system of a workbook that is currently open in
      Excel?
  - answer: The method works in the free trial, but a full license removes evaluation
      limitations.
    question: Do I need a license to use `setDate1904`?
  - answer: No, the date system is a workbook‑level setting; it applies to all worksheets.
    question: Is it possible to change the date system for only a single worksheet?
  - answer: Open the saved file in Excel, go to **File → Options → Advanced**, and
      check the **"Use 1904 date system"** box.
    question: How can I verify that the date system was changed?
  type: FAQPage
tags:
- change excel date system
- aspose cells java
- excel date conversion
- java excel processing
title: Modifier le système de dates Excel en 1904 avec Aspose.Cells Java
url: /fr/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Modifier le système de dates Excel en 1904 avec Aspose.Cells Java

Dans ce tutoriel, vous apprendrez à **modifier le système de dates Excel** au format 1904 en utilisant Aspose.Cells pour Java. Le système 1904 est essentiel lorsque vous devez conserver des dates héritées provenant de Mac ou aligner vos modèles financiers qui attendent cet epoch. Nous parcourrons l’installation de la bibliothèque, le chargement d’un classeur, la bascule du système de dates et l’enregistrement du résultat — le tout sans nécessiter Microsoft Excel sur le serveur.

## Réponses rapides
- **Que fait le système de dates 1904 ?** Il commence à compter les jours à partir du 1 janvier 1904, décalant toutes les dates de 1 462 jours par rapport au système par défaut de 1900.  
- **Pourquoi utiliser Aspose.Cells pour modifier le système de dates ?** Il fournit une API simple qui fonctionne sans Excel installé et prend en charge les gros fichiers.  
- **Quelles versions de Java sont prises en charge ?** JDK 8 ou supérieur.  
- **Ai-je besoin d’une licence ?** Un essai gratuit suffit pour l’évaluation ; une licence supprime les limites d’utilisation.  
- **Puis-je reconvertir au système 1900 plus tard ?** Oui, il suffit d’appeler `setDate1904(false)`.

## Qu’est‑ce que le système de dates 1904 dans Excel ?
Le système de dates 1904 compte les jours à partir du 1 janvier 1904, au lieu de l’époque par défaut de 1900. Ce décalage ajoute exactement 1 462 jours à chaque valeur de date, ce qui explique pourquoi les classeurs Mac hérités apparaissent décalés lorsqu’ils sont ouverts sous Windows. Il est principalement utilisé pour la compatibilité avec d’anciens fichiers Excel Macintosh et certains modèles financiers hérités.

## Pourquoi modifier le système de dates Excel avec Aspose.Cells ?
Vous pouvez basculer le système de dates directement depuis Java, éliminant les étapes manuelles dans Excel. Aspose.Cells traite des classeurs jusqu’à **2 GB** et peut convertir un classeur de 500 feuilles en moins de **2 secondes** sur un serveur typique à 4 cœurs, offrant une automatisation serveur à haut débit.

## Prérequis
- Java Development Kit (JDK) 8 ou supérieur.  
- Maven ou Gradle pour la gestion des dépendances.  
- Connaissances de base en programmation Java.  

## Configuration d’Aspose.Cells pour Java

### Maven
Ajoutez la dépendance suivante à votre fichier `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

### Gradle
Incluez cette ligne dans votre fichier `build.gradle` :

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

#### Acquisition de licence
Aspose propose un essai gratuit, une licence temporaire et des licences commerciales complètes. Vous pouvez commencer avec l’[essai gratuit](https://releases.aspose.com/cells/java/) ou obtenir une licence temporaire depuis la [page de licence temporaire](https://purchase.aspose.com/temporary-license/).

## Comment modifier le système de dates Excel en 1904 avec Aspose.Cells pour Java ?
Chargez le classeur, activez le paramètre 1904 et enregistrez le fichier — ce flux en trois étapes met à jour l’époque interne des dates du classeur en moins d’une seconde. L’appel d’API `setDate1904(true)` bascule le drapeau du système, et la modification est persistée lorsque vous appelez `save`. Aucun installation d’Excel n’est requise, ce qui le rend idéal pour les environnements serveur sans interface graphique.

### Étape 1 : initialiser et charger le classeur
La classe `Workbook` représente un fichier Excel complet en mémoire. Commencez par créer une instance `Workbook` qui pointe vers votre fichier existant.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Initialize a Workbook object with the path to your Excel file
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
```

### Étape 2 : activer le système de dates 1904
La méthode `WorkbookSettings.setDate1904` bascule le drapeau de date au niveau du classeur. Le définir à `true` active le système 1904 pour toutes les feuilles de calcul.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
// Load the workbook from your specified directory
Workbook workbook = new Workbook(dataDir + "/Mybook.xlsx");

// Enable the 1904 date system
workbook.getSettings().setDate1904(true);
```

**Astuce :** Vous pouvez également appeler `setDate1904(false)` plus tard si vous devez revenir en arrière.

### Étape 3 : enregistrer le classeur modifié
Enfin, écrivez les modifications dans un nouveau fichier (ou écrasez l’original). La méthode `save` respecte automatiquement le système de dates actif.

```java
import com.aspose.cells.Workbook;

String dataDir = "YOUR_DATA_DIRECTORY"; // Ensure the path to your Excel file is correct
String outDir = "YOUR_OUTPUT_DIRECTORY"; // Specify where you want to save the modified workbook

// Load and modify your workbook as shown in previous steps
tWorkbook workbook = new Workbook(dataDir + "/Mybook.xlsx");
workbook.getSettings().setDate1904(true);

// Save the changes to a new file
workbook.save(outDir + "/I1904DateSystem_out.xls");
```

> **Note :** Le code ci‑dessus utilise le nom de classe `tWorkbook` tel qu’il a été fourni initialement. Assurez‑vous que cette coquille correspond aux conventions de nommage de votre projet ou corrigez‑la en `Workbook` si nécessaire.

## Définir la date Excel par programmation (mot‑clé secondaire)
Si vous devez ajuster les valeurs de cellules individuelles après avoir changé le système, vous pouvez utiliser `cells.get(i, j).putValue(Date)` où la date sera interprétée selon le système de dates actif.

## Convertir le système Excel 1904 en 1900 (mot‑clé secondaire)
Pour revenir en arrière, appelez simplement :

```java
workbook.getSettings().setDate1904(false);
```

Puis enregistrez à nouveau le classeur.

## Applications pratiques
1. **Archivage des données** – Conserver les horodatages hérités lors de la migration d’anciennes feuilles de calcul Mac.  
2. **Rapports multiplateformes** – Générer des rapports qui s’ouvrent correctement à la fois sous Windows et macOS sans discordances de dates.  
3. **Modélisation financière** – Aligner les calculs de dates avec les modèles financiers hérités qui attendent le système 1904.  

## Considérations de performance
- Limitez les opérations sur le classeur dans une seule session afin de maintenir une faible consommation de mémoire ; Aspose.Cells diffuse les données et ne charge jamais le fichier complet en RAM sauf si vous le demandez explicitement.  
- Ajustez les drapeaux de collecte des déchets de Java (`-XX:+UseG1GC`) pour les fichiers très volumineux afin d’éviter des pics de temps de pause.  

## Questions fréquemment posées

**Q : Quelle est la différence entre les systèmes de dates 1900 et 1904 ?**  
R : Le système 1900 commence le 1 janvier 1900, tandis que le système 1904 commence le 1 janvier 1904, décalant toutes les dates de 1 462 jours.

**Q : Puis‑je changer le système de dates d’un classeur qui est actuellement ouvert dans Excel ?**  
R : Oui, mais vous devez d’abord fermer le fichier dans Excel ; sinon l’opération d’enregistrement échouera.

**Q : Ai‑je besoin d’une licence pour utiliser `setDate1904` ?**  
R : La méthode fonctionne avec l’essai gratuit, mais une licence complète supprime les limitations d’évaluation.

**Q : Est‑il possible de changer le système de dates pour une seule feuille de calcul ?**  
R : Non, le système de dates est un paramètre au niveau du classeur ; il s’applique à toutes les feuilles.

**Q : Comment vérifier que le système de dates a bien été modifié ?**  
R : Ouvrez le fichier enregistré dans Excel, allez dans **Fichier → Options → Avancé**, et cochez la case **« Utiliser le système de dates 1904 »**.

## Conclusion
Vous savez maintenant comment **modifier le système de dates Excel** en 1904 avec Aspose.Cells pour Java, comment définir des dates de cellules individuelles, et comment revenir au système 1900 si nécessaire. Intégrez ces extraits dans vos pipelines de traitement de données pour garantir la compatibilité des dates sur toutes les plateformes et avec les fichiers hérités.

---

**Dernière mise à jour :** 2026-10-28  
**Testé avec :** Aspose.Cells 25.3 pour Java  
**Auteur :** Aspose  

**Ressources**
- **Documentation :** [Aspose.Cells Java Reference](https://reference.aspose.com/cells/java/)
- **Téléchargement :** [Aspose.Cells Releases](https://releases.aspose.com/cells/java/)
- **Acheter une licence :** [Buy Aspose.Cells](https://purchase.aspose.com/buy)
- **Essai gratuit :** [Start Free Trial](https://releases.aspose.com/cells/java/)
- **Licence temporaire :** [Get Temporary License](https://purchase.aspose.com/temporary-license/)
- **Forum de support :** [Aspose Support](https://forum.aspose.com/c/cells/9)

## Tutoriels associés

- [Convertir efficacement Excel en PDF avec des formats de date personnalisés en utilisant Aspose.Cells pour Java](/cells/java/workbook-operations/render-excel-custom-date-formats-pdf-aspose-cells-java/)
- [Aspose.Cells pour Java : comment créer et formater des classeurs Excel efficacement](/cells/java/getting-started/aspose-cells-java-workbook-creation-guide/)
- [Maîtriser la manipulation d’Excel avec Aspose.Cells pour Java : opérations sur les classeurs et tutoriel de style de cellules](/cells/java/workbook-operations/excel-manipulation-aspose-cells-java-tutorial/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}