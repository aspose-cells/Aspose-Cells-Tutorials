---
date: '2026-05-18'
description: Apprenez à ajouter un segment à un tableau croisé dynamique dans Excel
  avec Aspose.Cells for Java — chargez des classeurs, personnalisez les segments et
  enregistrez les fichiers Excel efficacement.
keywords:
- add slicer to pivot
- save excel file java
- load excel workbook java
- Aspose.Cells Java
- Excel slicer automation
schemas:
- author: Aspose
  dateModified: '2026-05-18'
  description: Learn how to add slicer to pivot in Excel using Aspose.Cells for Java—load
    workbooks, customize slicers, and save Excel files efficiently.
  headline: How to Add Slicer to Pivot in Excel Using Aspose.Cells for Java
  type: TechArticle
- questions:
  - answer: Yes, it handles formulas, charts, pivot tables, conditional formatting,
      and more across 50+ formats.
    question: Does Aspose.Cells support other Excel features besides slicers?
  - answer: Absolutely. Aspose.Cells works with Java 8, 11, 17, and 21.
    question: Is the library compatible with Java 11 and newer?
  - answer: Yes. Because Aspose.Cells is pure Java, it runs on any OS with a compatible
      JVM.
    question: Can I run this code on a Linux server?
  - answer: Call `slicer.setStyleType(SlicerStyleType.YOUR_CHOSEN_STYLE);` where the
      enum provides dozens of predefined styles.
    question: How do I apply a custom style to a slicer?
  - answer: The Aspose.Cells documentation and the official GitHub repository contain
      extensive examples for slicers, pivot tables, and chart automation.
    question: Where can I find more code samples?
  type: FAQPage
title: Comment ajouter un segment à un tableau croisé dynamique dans Excel avec Aspose.Cells
  for Java
url: /fr/java/advanced-features/excel-slicer-modifications-java-aspose-cells/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Ajouter un segment à un tableau croisé dynamique dans Excel à l'aide d'Aspose.Cells pour Java

## Introduction

Si vous cherchez à **ajouter un segment à un tableau croisé dynamique** de manière programmatique, Aspose.Cells pour Java vous propose une API pure‑Java qui gère les segments sans nécessiter Microsoft Office. Dans de nombreux projets de reporting, les développeurs passent des heures à ajuster manuellement les segments ; avec cette bibliothèque, vous pouvez automatiser ces modifications en quelques secondes, améliorer la cohérence et garder vos tableaux de bord à jour sur tous les environnements. Ce guide vous montre comment afficher les informations de version, **charger un classeur Excel Java**, accéder aux feuilles de calcul, personnaliser les propriétés du segment, puis **enregistrer le fichier Excel Java** avec les mises à jour.

## Réponses rapides
- **Quel bibliothèque permet l'automatisation des segments ?** Aspose.Cells pour Java  
- **Puis-je ajouter un segment à un tableau croisé dynamique par programme ?** Oui – utilisez la classe `Slicer`  
- **Une licence est‑elle requise pour la production ?** Un essai gratuit suffit pour l'évaluation ; une licence est nécessaire pour un usage commercial  
- **Quelles versions de Java sont prises en charge ?** JDK 8 et supérieures (y compris 11, 17, 21)  
- **Où trouver la dépendance Maven ?** Sur Maven Central sous `com.aspose:aspose-cells`

## Qu'est‑ce que « add slicer to pivot » dans ce contexte ?

**Add slicer to pivot** signifie créer ou modifier programmatique un segment qui contrôle les critères de filtrage d'un tableau croisé dynamique, permettant aux utilisateurs finaux de découper les données de façon interactive. En utilisant l'API Aspose.Cells, vous pouvez définir la position, le style et les champs liés du segment, puis l'associer à un ou plusieurs tableaux croisés dynamiques afin que les modifications effectuées via le segment filtrent instantanément les données sous‑jacentes sans intervention manuelle.

## Pourquoi utiliser Aspose.Cells pour l'automatisation des segments Excel ?

Aspose.Cells prend en charge **plus de 50 formats d'entrée et de sortie** et peut traiter des classeurs contenant **jusqu'à 10 000 lignes** sans charger le fichier complet en mémoire, offrant ainsi une automatisation haute performance sous Windows, Linux et macOS. La bibliothèque vous donne un contrôle total sur l'apparence, le style et les tableaux croisés dynamiques liés aux segments, éliminant les dépendances COM et réduisant la surcharge d'exécution.

## Prérequis

- Kit de développement Java (JDK) 8 ou supérieur  
- IDE tel qu'IntelliJ IDEA ou Eclipse  
- Maven ou Gradle pour la gestion des dépendances  

### Bibliothèques et dépendances requises

Nous utiliserons Aspose.Cells pour Java, une bibliothèque puissante qui permet la manipulation de fichiers Excel dans les applications Java. Voici les détails d'installation :

**Maven :**

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

**Gradle :**

```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Acquisition de licence

Aspose.Cells pour Java propose un essai gratuit pour démarrer. Pour une utilisation intensive, vous pouvez obtenir une licence temporaire ou acheter une licence complète. Visitez [purchase Aspose](https://purchase.aspose.com/buy) pour explorer vos options.

## Configuration d'Aspose.Cells pour Java

Ajoutez les déclarations d'importation nécessaires en haut de vos fichiers Java :

```java
import com.aspose.cells.*;
```

Assurez‑vous que vos répertoires de données sont correctement définis :

```java
String dataDir = "YOUR_DATA_DIRECTORY";
String outDir = "YOUR_OUTPUT_DIRECTORY";
```

## Comment ajouter un segment à un tableau croisé dynamique dans Excel à l'aide d'Aspose.Cells ?

Pour ajouter un segment, chargez d'abord le classeur, localisez la feuille contenant le tableau croisé dynamique cible, puis créez un objet `Slicer` lié à ce tableau. Configurez son style, sa position et le champ qu'il filtre, puis enregistrez le classeur. Cette séquence garantit que le segment est pleinement fonctionnel et correctement associé au tableau croisé dynamique, offrant une expérience de filtrage interactive aux utilisateurs finaux.

### Afficher la version d'Aspose.Cells pour Java

La classe `VersionInfo` fournit la version actuelle de la bibliothèque Aspose.Cells.  
```java
public class VersionDisplay {
    public static void displayVersion() throws Exception {
        System.out.println("Aspose.Cells for Java Version: " + CellsHelper.getVersion());
    }
}
```

### Charger un classeur Excel Java

La classe `Workbook` représente un fichier Excel complet chargé en mémoire.  
```java
public class LoadExcelFile {
    public static Workbook loadWorkbook() throws Exception {
        return new Workbook(dataDir + "/sampleFormattingSlicer.xlsx");
    }
}
```

### Accéder à la feuille de calcul

Un objet `Worksheet` correspond à une feuille unique du classeur.  
```java
public class AccessWorksheet {
    public static Worksheet getFirstWorksheet(Workbook wb) throws Exception {
        return wb.getWorksheets().get(0);
    }
}
```

### Personnaliser le segment du tableau de bord Excel

La classe `Slicer` encapsule un segment lié à un tableau croisé dynamique, permettant la personnalisation du filtre.  
```java
public class ModifySlicerProperties {
    public static void configureSlicer(Worksheet ws) throws Exception {
        Slicer slicer = ws.getSlicers().get(0);
        
        // Set number of columns displayed by the slicer
        slicer.setNumberOfColumns(2);
        
        // Change the style type for better visual appeal
        slicer.setStyleType(SlicerStyleType.SLICER_STYLE_LIGHT_6);
    }
}
```

### Enregistrer le fichier Excel Java

La méthode `save` de `Workbook` écrit le classeur modifié dans un fichier.  
```java
public class SaveWorkbook {
    public static void saveModifiedWorkbook(Workbook wb) throws Exception {
        wb.save(outDir + "/outputFormattingSlicer.xlsx", SaveFormat.XLSX);
    }
}
```

## Problèmes courants et solutions

- **Le segment n'apparaît pas après l'enregistrement :** assurez‑vous que le segment est lié à un tableau croisé dynamique existant et que `setShowHeader` est défini sur `true`.  
- **Ralentissement de performance sur de gros fichiers :** traitez uniquement les feuilles nécessaires et désactivez le recalcul automatique avec `WorkbookSettings.setRecalcMode(RecalcMode.Manual)`.  
- **Style non appliqué :** vérifiez que le `SlicerStyleType` choisi est pris en charge dans la version cible d'Excel.

## FAQ

**Q : Aspose.Cells prend‑il en charge d'autres fonctionnalités Excel en plus des segments ?**  
R : Oui, il gère les formules, graphiques, tableaux croisés dynamiques, mise en forme conditionnelle et bien plus encore sur plus de 50 formats.

**Q : La bibliothèque est‑elle compatible avec Java 11 et les versions ultérieures ?**  
R : Absolument. Aspose.Cells fonctionne avec Java 8, 11, 17 et 21.

**Q : Puis‑je exécuter ce code sur un serveur Linux ?**  
R : Oui. Étant donné qu'Aspose.Cells est purement Java, il s'exécute sur tout système d'exploitation disposant d'une JVM compatible.

**Q : Comment appliquer un style personnalisé à un segment ?**  
R : Appelez `slicer.setStyleType(SlicerStyleType.VOTRE_STYLE_CHOISI);` où l'énumération fournit des dizaines de styles prédéfinis.

**Q : Où puis‑je trouver davantage d'exemples de code ?**  
R : La documentation d'Aspose.Cells et le dépôt officiel GitHub contiennent de nombreux exemples pour les segments, les tableaux croisés dynamiques et l'automatisation des graphiques.

## Conclusion

Dans ce tutoriel, vous avez appris à **ajouter un segment à un tableau croisé dynamique** dans Excel à l'aide d'Aspose.Cells pour Java — vérifier la version de la bibliothèque, **charger un classeur Excel Java**, accéder à la feuille appropriée, **personnaliser le segment du tableau de bord Excel**, puis **enregistrer le fichier Excel Java**. En automatisant ces étapes, vous pouvez créer des tableaux de bord dynamiques et interactifs sans effort manuel.

**Étapes suivantes :**  
- Expérimentez avec différentes valeurs de `SlicerStyleType` pour correspondre à l'identité visuelle de votre entreprise.  
- Combinez l'automatisation des segments avec le rafraîchissement des données du tableau croisé dynamique pour des pipelines de reporting entièrement dynamiques.  

Prêt à mettre en œuvre ces techniques dans votre propre projet ? Essayez‑les dès aujourd'hui !

---

**Last Updated:** 2026-05-18  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Tutoriels associés

- [Maîtriser Aspose.Cells pour Java : charger et accéder efficacement aux tableaux croisés dynamiques dans Excel](/cells/java/data-analysis/aspose-cells-java-load-pivot-tables/)
- [Enregistrer le fichier Excel Java & mettre à jour les segments avec Aspose.Cells](/cells/java/advanced-features/update-slicers-java-excel-aspose-cells/)
- [Actualiser le segment Excel et le personnaliser avec Aspose.Cells pour Java](/cells/java/advanced-features/customize-slicers-excel-aspose-cells-java/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}