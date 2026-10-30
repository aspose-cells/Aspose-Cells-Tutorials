---
category: general
date: 2026-07-20
description: Appliquer le format numérique Excel avec Java et Aspose.Cells. Apprenez
  comment appliquer le style monétaire dans Excel, créer un classeur Excel en Java
  et importer efficacement un DataTable vers Excel.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- apply number format excel
- apply currency style excel
- create excel workbook java
- import datatable to excel
language: fr
lastmod: 2026-07-20
og_description: Appliquer le format de nombre Excel avec Java. Ce guide vous montre
  comment appliquer le style monétaire dans Excel, créer un classeur Excel en Java
  et importer un DataTable dans Excel étape par étape.
og_image_alt: Screenshot of an Excel workbook where apply number format excel has
  been applied to a currency column
og_title: Appliquer le format de nombre Excel en Java – Tutoriel complet Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-07-20'
  description: Apply number format excel using Java and Aspose.Cells. Learn how to
    apply currency style excel, create excel workbook java, and import datatable to
    excel efficiently.
  headline: Apply Number Format Excel in Java – Complete Aspose.Cells Guide
  type: TechArticle
- questions:
  - answer: Absolutely. Open the workbook with `new Workbook("Existing.xlsx")`, fetch
      the target worksheet, and follow steps 3‑5 to apply the style array to new data.
    question: Can I apply the number format to an existing workbook?
  - answer: Use a different built‑in number index (`14` for short date, `22` for long
      date) or a custom format like `yyyy‑mm‑dd`. The workflow stays the same.
    question: What if I need to format dates instead of currency?
  - answer: 'Yes. Just change the file extension in `workbook.save("MyFile.xls")`.
      Aspose will automatically switch to the binary format. ## Wrap‑Up – What We
      Achieved We have **applied number format excel** to a column of monetary values,
      demonstrated how to **apply currency style excel**, shown the simplest wa'
    question: Does this work with older Excel versions (.xls)?
  type: FAQPage
tags:
- Aspose.Cells
- Java
- Excel Automation
title: Appliquer le format de nombre Excel en Java – Guide complet d’Aspose.Cells
url: /fr/java/formatting/apply-number-format-excel-in-java-complete-aspose-cells-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Appliquer le format de nombre Excel en Java – Guide complet Aspose.Cells

Vous vous êtes déjà demandé comment **apply number format excel** directement depuis du code Java ? Peut-être que vous générez des rapports financiers ou que vous avez besoin d’une façon rapide de mettre en forme une colonne de montants sans ouvrir Excel manuellement. Bonne nouvelle ? Avec Aspose.Cells, vous pouvez le faire en quelques lignes, et vous apprendrez également comment **apply currency style excel**, **create excel workbook java**, et **import datatable to excel** en une seule routine propre.

Dans ce tutoriel, nous allons parcourir un exemple réel : une liste de montants stockée dans un `List<Map<String,Object>>` Java est importée dans un nouveau classeur, la première colonne reçoit un format de devise intégré, et le fichier est enregistré prêt à être distribué. Prêt à voir à quel point c’est simple ? Plongeons‑y.

## Prérequis – Ce dont vous avez besoin

- **Java Development Kit (JDK) 8+** – le code s'exécute sur n'importe quel JDK récent.  
- **Aspose.Cells for Java** library (the Maven artifact `com.aspose:aspose-cells`) – c’est le moteur qui nous permet de manipuler des fichiers Excel sans Office installé.  
- Un **IDE préféré** (IntelliJ IDEA, Eclipse, VS Code…) – n'importe quel éditeur convient, mais un IDE accélère le débogage.  
- Familiarité de base avec les **collections Java** – nous utiliserons une `List` de `Map` pour imiter une DataTable.  

C’est tout. Aucun service externe, aucune installation d’Excel, juste du Java pur.

## Étape 1 : Créer un classeur Excel Java – Instanciation du classeur

La première chose dont nous avons besoin est un objet workbook. Considérez‑le comme la toile vierge où tout vivra.

```java
// Step 1: Create a new workbook instance
Workbook workbook = new Workbook(); // creates an in‑memory Excel file
```

Pourquoi créer le classeur en premier ? Aspose.Cells fonctionne entièrement en mémoire, vous pouvez donc ajouter des feuilles, des styles et des données avant même de toucher le disque. Cette approche est rapide et rend votre code testable.

## Étape 2 : Préparer les données – Importer DataTable vers Excel à l’aide d’une liste de maps

Dans de nombreuses applications d’entreprise, les données proviennent des bases de données sous forme de tables. Ici, nous simulons cela avec un `List<Map<String,Object>>`. Chaque map représente une ligne, et la clé `"Amount"` correspond à une valeur numérique.

```java
// Step 2: Build a DataTable‑like structure (list of maps)
List<Map<String, Object>> dataRows = new ArrayList<>();

// Row 1
dataRows.add(new HashMap<>() {{
    put("Amount", 1234.56);
}});
// Row 2
dataRows.add(new HashMap<>() {{
    put("Amount", 7890.12);
}});
```

Vous pourriez vous demander : « Pourquoi ne pas utiliser un `ResultSet` ou des POJOs ? » La méthode `importDataTable` accepte toute collection qui se comporte comme une DataTable, et une liste de maps est la façon la plus simple de démontrer le concept sans ajouter de dépendances supplémentaires.

## Étape 3 : Définir le format de nombre – Appliquer le style de devise Excel

Voici le cœur du tutoriel : **apply number format excel**. Aspose.Cells propose des formats de nombre intégrés ; le format de devise est l’index 5. Nous récupérons le style par défaut de la première feuille, modifions son format de nombre, et le conservons pour une utilisation ultérieure.

```java
// Step 3: Get the default style and set a currency number format
Style currencyStyle = workbook.getWorksheets().get(0).getCells().getDefaultStyle();
currencyStyle.setNumber(5); // 5 = built‑in currency format ($#,##0.00)
```

Pourquoi utiliser le style par défaut comme base ? Il contient déjà la police, l’alignement et d’autres paramètres par défaut du classeur, vous n’avez donc besoin de changer que ce qui importe — dans ce cas, le format de nombre. Si vous avez besoin d’un format personnalisé (par ex. « €#,##0.00 »), vous pouvez appeler `currencyStyle.setCustom("#,##0.00 €")` à la place.

## Étape 4 : Configurer les options d’importation – Lier le tableau de styles

Aspose.Cells vous permet de transmettre un tableau d’objets `Style` qui correspondent aux colonnes importées. Comme nos données n’ont qu’une seule colonne, nous fournissons un tableau à un seul élément contenant le style de devise.

```java
// Step 4: Configure import options with the style array
ImportTableOptions importOptions = new ImportTableOptions();
importOptions.setStyleArray(new Style[] { currencyStyle });
```

Si vous devez un jour styliser plusieurs colonnes différemment, il suffit d’étendre le tableau : `new Style[] { styleForCol1, styleForCol2, … }`. L’ordre des styles correspond à l’ordre des colonnes dans les données source.

## Étape 5 : Importer les données – Faire entrer le DataTable dans la feuille

Avec le classeur prêt, les données préparées et les styles définis, nous pouvons enfin **import datatable to excel**. Nous commençons à la cellule `A1`, incluons les en‑têtes de colonnes (`true`), et transmettons les `ImportTableOptions`.

```java
// Step 5: Perform the import
Worksheet worksheet = workbook.getWorksheets().get(0);
worksheet.getCells().importDataTable(dataRows, true, "A1", importOptions);
```

Remarquez le drapeau `true` — Aspose.Cells générera automatiquement une ligne d’en‑tête basée sur les clés des maps (`"Amount"`). Si vous le passez à `false`, l’en‑tête sera omise, vous donnant plus de contrôle sur la mise en page finale.

## Étape 6 : Enregistrer le fichier – Créer un classeur Excel Java sur le disque

La dernière pièce du puzzle consiste à persister le classeur en mémoire dans un fichier physique. Vous pouvez choisir n’importe quel format supporté par Aspose (`.xlsx`, `.xls`, `.csv`, …). Ici, nous enregistrons au format XLSX.

```java
// Step 6: Save the workbook to disk
String outputPath = "DataTableWithCurrencyStyle.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Après avoir exécuté le programme, ouvrez le fichier généré. Vous verrez la colonne `"Amount"` formatée avec le symbole dollar, deux décimales et les séparateurs de milliers appropriés — exactement ce que vous attendez lorsque vous **apply number format excel** pour des valeurs monétaires.

## Résultat attendu

| Montant |
|--------|
| $1,234.56 |
| $7,890.12 |

L’en‑tête « Montant » apparaît en gras (style par défaut), et chaque cellule en dessous montre le format de devise que nous avons défini. Aucun formatage manuel dans Excel n’est requis.

## Astuces professionnelles et pièges courants

- **Réutiliser les styles judicieusement** – Les styles sont légers, mais créer un nouveau `Style` pour chaque cellule peut nuire aux performances. Réutilisez toujours un objet style lorsque vous appliquez le même format à de nombreuses cellules, comme nous l’avons fait avec `currencyStyle`.  
- **Formats personnalisés** – Si votre locale utilise un symbole monétaire différent, remplacez `currencyStyle.setNumber(5)` par `currencyStyle.setCustom("€#,##0.00")`. Testez le format dans Excel pour vérifier son comportement.  
- **Jeux de données volumineux** – Pour des milliers de lignes, envisagez d’utiliser `importDataTable` avec le drapeau `ImportTableOptions.setImportDataOnly(true)` afin de sauter la génération d’en‑tête et d’accélérer l’importation.  
- **Sécurité des threads** – Les objets Aspose.Cells ne sont **pas** thread‑safe. Créez un `Workbook` distinct par thread si vous générez des rapports en parallèle.

## Questions fréquentes

**Q : Puis‑je appliquer le format de nombre à un classeur existant ?**  
R : Absolument. Ouvrez le classeur avec `new Workbook("Existing.xlsx")`, récupérez la feuille cible, et suivez les étapes 3‑5 pour appliquer le tableau de styles aux nouvelles données.

**Q : Et si je dois formater des dates au lieu de devises ?**  
R : Utilisez un autre index de nombre intégré (`14` pour la date courte, `22` pour la date longue) ou un format personnalisé comme `yyyy‑mm‑dd`. Le flux de travail reste le même.

**Q : Cela fonctionne‑t‑il avec les anciennes versions d’Excel (.xls) ?**  
R : Oui. Il suffit de changer l’extension du fichier dans `workbook.save("MyFile.xls")`. Aspose basculera automatiquement vers le format binaire.

## Conclusion – Ce que nous avons accompli

Nous avons **applied number format excel** à une colonne de valeurs monétaires, démontré comment **apply currency style excel**, montré la façon la plus simple de **create excel workbook java**, et utilisé Aspose.Cells pour **import datatable to excel** sans toucher à l’interface utilisateur. Tout cela a été réalisé dans un programme concis et autonome que vous pouvez copier, coller et exécuter.

Et après ? Essayez d’étendre l’exemple :

- Ajoutez d’autres colonnes (par ex. « Date », « Description ») et attribuez des styles différents à chaque colonne.  
- Exportez les mêmes données en CSV et comparez la perte des formats numériques.  
- Intégrez le code dans un service Spring Boot qui renvoie le classeur en tant que réponse HTTP téléchargeable.

N’hésitez pas à expérimenter, et si vous rencontrez des difficultés, laissez un commentaire ci‑dessous. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités supplémentaires de l’API et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Comment appliquer des styles aux cellules Excel avec Aspose.Cells pour Java – Guide complet](/cells/english/java/formatting/apply-styles-excel-aspose-cells-java/)
- [Fusionner des cellules et appliquer des styles dans Excel avec Aspose.Cells pour Java – Guide complet](/cells/english/java/formatting/merge-cells-apply-styles-aspose-cells-java/)
- [Aspose.Cells pour Java : comment créer et formater efficacement des classeurs Excel](/cells/english/java/getting-started/aspose-cells-java-workbook-creation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}