---
title: Regroupement de données dans des tableaux croisés dynamiques
linktitle: Regroupement de données dans des tableaux croisés dynamiques
second_title: API de traitement Java Excel Aspose.Cells
description: Découvrez comment créer des tableaux croisés dynamiques dans Excel à l'aide d'Aspose.Cells pour Java. Automatisez le regroupement et l'analyse des données avec des exemples de code source.
weight: 14
url: /fr/java/excel-pivot-tables/grouping-data-in-pivot-tables/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Regroupement de données dans des tableaux croisés dynamiques


Les tableaux croisés dynamiques sont un outil puissant pour analyser et résumer les données dans des feuilles de calcul. Ils vous permettent de regrouper et de classer les données pour obtenir des informations précieuses. Dans cet article, nous découvrirons comment regrouper efficacement les données dans des tableaux croisés dynamiques à l'aide d'Aspose.Cells pour Java, ainsi que des exemples de code source.

## Introduction

Les tableaux croisés dynamiques offrent un moyen flexible d'organiser et de résumer les données de grands ensembles de données. Ils vous permettent de créer des vues personnalisées de vos données en les regroupant en catégories ou en hiérarchies. Cela peut vous aider à identifier plus facilement les tendances, les modèles et les valeurs aberrantes dans vos données.

## Étape 1 : Créer un tableau croisé dynamique

Commençons par créer un tableau croisé dynamique à l'aide d'Aspose.Cells pour Java. Vous trouverez ci-dessous un exemple de création d'un tableau croisé dynamique à partir d'un fichier Excel.

```java
// Charger le fichier Excel
Workbook workbook = new Workbook("sample.xlsx");

// Accéder à la feuille de calcul contenant les données
Worksheet worksheet = workbook.getWorksheets().get(0);

// Spécifier la plage de données
CellArea sourceData = new CellArea();
sourceData.startRow = 0;
sourceData.endRow = 19; // En supposant 20 lignes de données
sourceData.startColumn = 0;
sourceData.endColumn = 3; // En supposant 4 colonnes de données

// Créer un tableau croisé dynamique basé sur la plage de données
int index = worksheet.getPivotTables().add(sourceData, "A1", "PivotTable1");

// Obtenir le tableau croisé dynamique par index
PivotTable pivotTable = worksheet.getPivotTables().get(index);

// Ajouter des champs aux lignes et aux colonnes
pivotTable.addFieldToArea("Product", PivotFieldType.ROW);
pivotTable.addFieldToArea("Region", PivotFieldType.COLUMN);

// Ajouter des valeurs et appliquer l'agrégation
pivotTable.addFieldToArea("Sales", PivotFieldType.DATA);
pivotTable.getDataFields().get(0).setFunction(PivotFieldFunction.SUM);

// Enregistrer le fichier Excel modifié
workbook.save("output.xlsx");
```

## Étape 2 : regrouper les données

 Dans Aspose.Cells pour Java, vous pouvez regrouper des données dans le tableau croisé dynamique à l'aide de`PivotField` classe. Voici un exemple de la manière de regrouper un champ dans le tableau croisé dynamique :

```java
// Accéder au champ « Produit » dans le tableau croisé dynamique
PivotField productField = pivotTable.getPivotFields().get("Product");

//Regroupez le champ « Produit » selon un critère spécifique, par exemple par lettre de départ
productField.setIsAutoSubtotals(false);
productField.setBaseField("Product");
productField.setAutoSort(true);
productField.setAutoShow(true);

// Enregistrer le fichier Excel modifié avec les données groupées
workbook.save("output_grouped.xlsx");
```

## Étape 3 : Personnaliser le regroupement

Vous pouvez personnaliser davantage les paramètres de regroupement, par exemple en spécifiant des intervalles de regroupement basés sur des dates ou des règles de regroupement personnalisées. Voici un exemple de personnalisation du regroupement basé sur des dates :

```java
// Accéder au champ « Date » dans le tableau croisé dynamique (en supposant qu'il s'agisse d'un champ de date)
PivotField dateField = pivotTable.getPivotFields().get("Date");

// Regrouper les dates par mois
dateField.setIsAutoSubtotals(false);
dateField.setIsDateGroup(true);
dateField.setDateGroupingType(PivotFieldDateGroupingType.MONTHS);

// Enregistrez le fichier Excel modifié avec le regroupement de dates personnalisé
workbook.save("output_custom_grouping.xlsx");
```

## Conclusion

Le regroupement de données dans des tableaux croisés dynamiques est une technique précieuse pour analyser et résumer des données dans Excel, et Aspose.Cells pour Java facilite l'automatisation de ce processus. Avec les exemples de code source fournis, vous pouvez créer des tableaux croisés dynamiques, personnaliser le regroupement et obtenir des informations sur vos données de manière efficace.

## FAQ

### 1. Quel est le but des tableaux croisés dynamiques dans Excel ?

Les tableaux croisés dynamiques dans Excel permettent de résumer et d'analyser de grands ensembles de données. Ils vous permettent de créer des vues personnalisées de vos données, facilitant ainsi l'identification des modèles et des tendances.

### 2. Comment puis-je personnaliser le regroupement des données dans un tableau croisé dynamique ?

 Vous pouvez personnaliser le regroupement des données dans un tableau croisé dynamique à l'aide de l'`PivotField` classe dans Aspose.Cells pour Java. Cela vous permet de spécifier des critères de regroupement, tels que des intervalles basés sur des dates ou des règles personnalisées.

### 3. Puis-je automatiser la création de tableaux croisés dynamiques à l'aide d'Aspose.Cells pour Java ?

Oui, vous pouvez automatiser la création de tableaux croisés dynamiques dans Excel à l’aide d’Aspose.Cells pour Java, comme démontré dans les exemples de code source fournis.
{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
