---
category: general
date: 2026-06-30
description: Trier les valeurs uniques dans Excel avec Java. Apprenez à définir une
  formule, recalculer les formules et générer une liste unique dans Excel avec Aspose.Cells.
draft: false
keywords:
- sort unique values excel
- how to set formula
- how to recalculate formulas
- generate unique list excel
- set array formula
language: fr
og_description: Trier les valeurs uniques dans Excel avec Java. Ce guide montre comment
  définir une formule, recalculer les formules et générer une liste unique dans Excel
  en quelques minutes.
og_title: Trier les valeurs uniques Excel – Tutoriel Java pour les formules matricielles
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  headline: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  type: TechArticle
- description: Sort unique values Excel using Java. Learn how to set formula, recalculate
    formulas, and generate unique list Excel with Aspose.Cells.
  name: Sort Unique Values Excel – Complete Java Guide to Set Array Formulas
  steps:
  - name: How It Works
    text: '- `UNIQUE(B1:B10)` scans the range and returns a vertical array of distinct
      strings. - `SORT(...)` takes that array and orders it in ascending order. -
      Wrapping the whole thing in `=` and calling `setFormulaArray` tells Aspose.Cells
      to treat the result as a **spilled array**, just like Excel would.'
  - name: Empty Cells in the Source Range
    text: 'If `B1:B10` contains blanks, `UNIQUE` will treat them as a distinct entry.
      To ignore blanks, wrap the range with `FILTER`:'
  - name: Non‑Contiguous Data
    text: 'When your data lives in multiple columns, you can join them with `CHOOSE`
      or `TEXTJOIN` before applying `UNIQUE`. For example:'
  - name: ' ## What Should You Learn Next?


      The following tutorials cover closely related topics that build on the techniques
      demonstrated in this guide. Each resource includes complete working code examples
      with step-by-step explanations to help you master additional API features and
      explore alternative implementation approaches in your own projects.

      - [How to Sort Excel Files by Cell Color Using Aspose.Cells Java&#58; A Comprehensive
      Guide](/cells/english/java/data-analysis/excel-file-sorting-aspose-cells-java/)
      - [Mastering Aspose.Cells Java&#58; How to Interrupt Formula Calculation in
      Excel Workbooks](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
      - [How to Create an Excel Data Validation List with Aspose.Cells for Java&#58;
      A Step-by-Step Guide](/cells/english/java/data-validation/excel-data-validation-aspose-cells-java/)

      {{< /blocks/products/pf/tutorial-page-section >}}'
    text: '{{< /blocks/products/pf/main-container >}} {{< /blocks/products/pf/main-wrap-class
      >}} {{< blocks/products/products-backtop-button >}}'
  type: HowTo
- questions:
  - answer: The `SORT` and `UNIQUE` functions are part of the Dynamic Array engine
      introduced in Excel 365. For legacy files you’d need to use classic array formulas
      like `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells
      can still evaluate them, but the syntax is more verbose.
    question: Does this work with older Excel versions (pre‑Office 365)?
  - answer: Absolutely. Just change the address in `cells.get("A1")`. The spilled
      array will always start at the cell you specify and expand right‑and‑down as
      needed.
    question: Can I set the array formula on a range other than `A1`?
  - answer: 'Replace the static range with a dynamic one, e.g., `B:B` or a named range.
      The formula becomes `=SORT(UNIQUE(B:B))`. Be cautious with whole‑column references
      on very large sheets; they can impact performance. --- ## Conclusion We’ve just
      covered **how to set formula** in Java to **sort unique values'
    question: What if my source data is larger than `B1:B10`?
  type: FAQPage
tags:
- Excel automation
- Java
- Aspose.Cells
title: Trier les valeurs uniques dans Excel – Guide complet Java pour définir les
  formules matricielles
url: /fr/java/formulas-functions/sort-unique-values-excel-complete-java-guide-to-set-array-fo/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Trier les valeurs uniques Excel – Guide complet Java pour définir des formules de tableau

Vous vous êtes déjà demandé comment **trier les valeurs uniques Excel** sans faire glisser les formules partout ? Vous n'êtes pas le seul. Dans de nombreux scénarios de reporting, vous avez besoin d'une liste propre, triée alphabétiquement, des entrées distinctes, et le faire manuellement est pénible.  

La bonne nouvelle ? Avec quelques lignes de code Java, vous pouvez **set array formula** sur une feuille de calcul, puis **recalculate formulas** afin que la plage débordante se remplisse automatiquement. Dans ce tutoriel, nous passerons en revue tout le processus — de la création d’un classeur à la génération d’une liste unique à la façon d’Excel — afin que vous puissiez intégrer la solution directement dans votre application.

## Ce que couvre ce tutoriel

- Configuration d’un projet Java avec Aspose.Cells (la bibliothèque qui alimente le snippet de code).  
- Utilisation conjointe des fonctions `SORT` et `UNIQUE` pour **generate unique list Excel**.  
- Application d’une **array formula** à une cellule de façon programmatique.  
- Déclenchement d’un passage de calcul afin que l’étape **how to recalculate formulas** s’exécute instantanément.  
- Vérification du résultat et ajustement de la solution pour les cas limites comme les cellules vides ou les plages non contiguës.

À la fin de ce guide, vous pourrez insérer une méthode prête à l’emploi dans n’importe quel service Java qui doit exporter des feuilles Excel propres.

> **Pro tip :** Si vous utilisez déjà Maven, ajouter Aspose.Cells comme dépendance vous évite de gérer manuellement les fichiers JAR.

---

## Prérequis

| Exigence | Pourquoi c'est important |
|----------|---------------------------|
| Java 8 ou plus récent | Aspose.Cells cible Java 8+. |
| Maven (ou Gradle) | Simplifie la gestion des dépendances. |
| Aspose.Cells for Java | Fournit les API `Workbook`, `Worksheet` et les formules que nous utiliserons. |
| Familiarité de base avec les fonctions Excel | Comprendre `SORT` et `UNIQUE` vous aide à adapter le code. |

> *Si vous n’avez pas encore Aspose.Cells, ajoutez ceci à votre `pom.xml`* :

```xml
<!-- Aspose.Cells for Java -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.12</version> <!-- latest as of June 2026 -->
</dependency>
```

---

## Étape 1 : Créer un nouveau classeur (How to Set Formula Begins Here)

Tout d’abord, nous avons besoin d’un classeur vierge. Considérez-le comme la toile vide sur laquelle nous allons plus tard **set array formula** sur la cellule `A1`.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // The rest of the steps follow...
```

> *Pourquoi créer un nouveau classeur ?*  
> Il garantit un environnement propre, évitant les formules cachées qui pourraient interférer avec nos données de test.

---

## Étape 2 : Remplir des données d’exemple (Optionnel mais utile)

Pour voir le résultat clairement, remplissons la colonne **B** avec quelques entrées dupliquées.

```java
        // Step 2: Get the first worksheet
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        // Sample data in B1:B10
        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }
```

> *Pourquoi utiliser la colonne B ?*  
> La formule que nous allons écrire fait référence à `B1:B10`, donc placer les données là reflète l’exemple classique d’Excel.

---

## Étape 3 : Définir une formule de tableau qui **Sort Unique Values Excel**

Maintenant, la magie opère. Nous combinons `UNIQUE` (pour éliminer les doublons) avec `SORT` (pour les trier alphabétiquement). L’expression résultante est une **array formula**, ce qui signifie qu’elle se déversera automatiquement dans les cellules adjacentes.

```java
        // Step 3: Set an array formula that sorts the unique values from B1:B10
        // This is the core of “how to set formula” for our scenario.
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");
```

### Comment ça fonctionne

- `UNIQUE(B1:B10)` parcourt la plage et renvoie un tableau vertical de chaînes distinctes.  
- `SORT(...)` prend ce tableau et le classe par ordre croissant.  
- En entourant le tout de `=` et en appelant `setFormulaArray`, on indique à Aspose.Cells de traiter le résultat comme un **spilled array**, exactement comme le ferait Excel.

> **Note :** Si vous utilisez une version plus ancienne d’Excel qui ne possède pas `SORT` ou `UNIQUE`, vous pouvez revenir à `SORT(UNIQUE(...))` avec la fonction **LET** ou utiliser des formules de tableau classiques (`=INDEX(...)`). Ce tutoriel se concentre sur l’approche moderne des tableaux dynamiques car c’est la façon la plus propre de **generate unique list Excel** aujourd’hui.

---

## Étape 4 : Recalculer les formules afin que la plage débordante soit remplie

Après avoir placé la formule, le classeur ne l’évalue pas automatiquement. C’est ici qu’intervient l’étape **how to recalculate formulas**.

```java
        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();
```

Appeler `calculateFormula()` force Aspose.Cells à exécuter le moteur Excel, remplissant les cellules `A1`, `A2`, … avec les valeurs uniques triées.

> *Pourquoi ne pas se fier à l’évaluation paresseuse ?*  
> Dans un contexte serveur, vous avez souvent besoin des données prêtes à être exportées (CSV, PDF, etc.) immédiatement après le calcul, donc un appel explicite garantit la cohérence.

---

## Étape 5 : Vérifier le résultat (Débogage optionnel)

Il est toujours judicieux d’imprimer les valeurs débordantes dans la console — surtout lorsque vous apprenez une nouvelle API.

```java
        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break; // stop at first empty cell
            System.out.println("- " + value);
            row++;
        }

        // Optionally, save the workbook to inspect in Excel
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

L’exécution du programme affiche :

```
Sorted unique list:
- Apple
- Banana
- Cherry
- Date
- Elderberry
- Fig
- Grape
```

Ouvrez `SortedUniqueValues.xlsx` et vous verrez les mêmes données se déverser à partir de `A1` vers le bas.

---

## Gestion des cas limites

### Cellules vides dans la plage source

Si `B1:B10` contient des cellules vides, `UNIQUE` les considérera comme une entrée distincte. Pour ignorer les vides, encapsulez la plage avec `FILTER` :

```java
cells.get("A1").setFormulaArray("=SORT(UNIQUE(FILTER(B1:B10, B1:B10<>\"\")))");
```

### Données non contiguës

Lorsque vos données se trouvent dans plusieurs colonnes, vous pouvez les joindre avec `CHOOSE` ou `TEXTJOIN` avant d’appliquer `UNIQUE`. Par exemple :

```java
cells.get("A1").setFormulaArray(
    "=SORT(UNIQUE(CHOOSE({1,2}, B1:B10, C1:C10)))"
);
```

Ces ajustements démontrent la flexibilité de **how to set formula** pour des scénarios plus complexes.

---

## Exemple complet fonctionnel (Toutes les étapes combinées)

Voici le programme Java complet et exécutable. Copiez‑collez‑le dans votre IDE, ajoutez la dépendance Aspose.Cells, puis lancez *Run*.

```java
import com.aspose.cells.*;

public class UniqueSortExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create a new workbook
        Workbook workbook = new Workbook();

        // Step 2: Get the first worksheet and fill sample data
        Worksheet worksheet = workbook.getWorksheets().get(0);
        Cells cells = worksheet.getCells();

        String[] rawData = { "Apple", "Banana", "Apple", "Cherry", "Banana",
                             "Date", "Elderberry", "Fig", "Date", "Grape" };
        for (int i = 0; i < rawData.length; i++) {
            cells.get("B" + (i + 1)).putValue(rawData[i]);
        }

        // Step 3: Set an array formula that sorts the unique values from B1:B10
        cells.get("A1").setFormulaArray("=SORT(UNIQUE(B1:B10))");

        // Step 4: Recalculate formulas so the spilled range is populated automatically
        workbook.calculateFormula();

        // Step 5: Output the spilled range to the console
        System.out.println("Sorted unique list:");
        int row = 0;
        while (true) {
            String value = cells.get(row, 0).getStringValue(); // column A = index 0
            if (value == null || value.isEmpty()) break;
            System.out.println("- " + value);
            row++;
        }

        // Save the workbook for visual verification
        workbook.save("SortedUniqueValues.xlsx");
    }
}
```

**Résultat attendu** (affiché dans la console) correspond à la liste triée et dédupliquée dont nous avons parlé. L’ouverture du fichier Excel généré révèle les mêmes valeurs débordant à partir de `A1` vers le bas.

---

## Questions fréquentes

**Q : Cette méthode fonctionne‑t‑elle avec les versions plus anciennes d’Excel (pré‑Office 365) ?**  
R : Les fonctions `SORT` et `UNIQUE` font partie du moteur de Tableaux Dynamiques introduit dans Excel 365. Pour les fichiers hérités, vous devrez recourir à des formules de tableau classiques comme `{=INDEX(..., MATCH(0, COUNTIF($A$1:A1, $B$1:$B$10), 0))}`. Aspose.Cells peut toujours les évaluer, mais la syntaxe est plus verbeuse.

**Q : Puis‑je définir la formule de tableau sur une plage autre que `A1` ?**  
R : Absolument. Il suffit de modifier l’adresse dans `cells.get("A1")`. Le tableau débordant commencera toujours à la cellule que vous spécifiez et s’étendra vers la droite et le bas selon les besoins.

**Q : Que faire si mes données sources dépassent `B1:B10` ?**  
R : Remplacez la plage statique par une plage dynamique, par exemple `B:B` ou une plage nommée. La formule devient `=SORT(UNIQUE(B:B))`. Soyez prudent avec les références de colonne entière sur des feuilles très volumineuses ; elles peuvent impacter les performances.

---

## Conclusion

Nous venons de couvrir **how to set formula** en Java pour **sort unique values Excel**, comment **recalculate formulas**, et comment **generate unique list Excel** à l’aide de l’API puissante d’Aspose.Cells. Les étapes sont simples : créer un classeur, remplir les données, appliquer une formule de tableau, déclencher le calcul et vérifier le résultat.  

À partir d’ici, vous pouvez étendre le scénario — ajouter une mise en forme conditionnelle, exporter en PDF, ou intégrer la méthode dans un service web qui délivre des rapports prêts à l’emploi. L’idée centrale reste la même : laissez les fonctions natives d’Excel faire le gros du travail, et laissez Java orchestrer le processus.

Prêt à faire passer votre automatisation Excel au niveau supérieur ? Essayez de remplacer `SORT` par `SORTBY` pour trier selon une colonne secondaire, ou expérimentez avec `FILTER` pour exclure les lignes qui ne répondent pas aux règles métier. Les possibilités sont pratiquement infinies.

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}