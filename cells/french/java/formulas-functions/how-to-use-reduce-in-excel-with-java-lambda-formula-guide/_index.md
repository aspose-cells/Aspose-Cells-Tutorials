---
category: general
date: 2026-06-08
description: Comment utiliser reduce dans Excel avec Java en utilisant Aspose.Cells.
  Apprenez la formule lambda Excel, les tableaux dynamiques en Java, comment écrire
  une lambda et la somme avec reduce dans un tutoriel clair, étape par étape.
draft: false
keywords:
- how to use reduce
- lambda formula excel
- dynamic arrays java
- how to write lambda
- sum with reduce
language: fr
og_description: Comment utiliser reduce dans Excel avec Java. Maîtrisez la formule
  lambda Excel, les tableaux dynamiques Java et la somme avec reduce grâce à un exemple
  complet et exécutable.
og_title: Comment utiliser Reduce dans Excel avec Java – Guide de la formule Lambda
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  headline: How to Use Reduce in Excel with Java – Lambda Formula Guide
  type: TechArticle
- description: How to use reduce in Excel with Java using Aspose.Cells. Learn lambda
    formula Excel, dynamic arrays java, how to write lambda, and sum with reduce in
    a clear step‑by‑step tutorial.
  name: How to Use Reduce in Excel with Java – Lambda Formula Guide
  steps:
  - name: What if I need a horizontal array instead of vertical?
    text: 'Swap the column/row arguments in `EXPAND`. For a horizontal spill across
      B1:F1:'
  - name: Can I use REDUCE to multiply instead of sum?
    text: 'Absolutely. Just change the lambda body:'
  - name: Does Aspose.Cells support custom LAMBDA functions?
    text: Yes, you can define named LAMBDA functions via the workbook’s `Names` collection,
      then call them like any built‑in formula. That’s a deeper dive for a later tutorial
      on **how to write lambda** functions that live beyond a single cell.
  - name: What about older Excel versions that don’t recognize REDUCE?
    text: If you target Excel 2019 or earlier, the engine will return `#NAME?`. In
      such cases
  type: HowTo
tags:
- Excel
- Java
- Aspose.Cells
title: Comment utiliser Reduce dans Excel avec Java – Guide de formule Lambda
url: /fr/java/formulas-functions/how-to-use-reduce-in-excel-with-java-lambda-formula-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment utiliser Reduce dans Excel avec Java – Guide des formules Lambda

Vous vous êtes déjà demandé **comment utiliser reduce** dans Excel lorsque vous écrivez du code Java ? Vous n'êtes pas seul. De nombreux développeurs se heurtent à un mur en essayant de combiner les nouvelles fonctions de tableau dynamique d'Excel avec l'automatisation basée sur Java, et la réponse n'est pas aussi cryptique qu'elle le paraît au premier abord.

Dans ce tutoriel, nous parcourrons un exemple concret qui montre **comment utiliser reduce** avec une expression **lambda formula Excel**, le tout propulsé par la bibliothèque Aspose.Cells for Java. À la fin, vous serez capable de générer des tableaux dynamiques en Java, d'écrire des fonctions lambda et de calculer une **somme avec reduce** — sans aucune manipulation manuelle de feuille de calcul.

---

## Ce que vous allez créer

- Un nouveau classeur créé entièrement depuis Java.  
- Un tableau dynamique **EXPAND** qui remplit les cellules A1:A5 avec les nombres 1‑5.  
- Une formule **REDUCE** qui additionne ces nombres à l'aide d'une **lambda formula Excel**.  
- Un fichier `.xlsx` enregistré que vous pouvez ouvrir dans n'importe quel programme de tableur pour vérifier le résultat.

Pas de macros externes, pas de VBA — juste du code Java pur et les fonctions modernes d'Excel.

---

## Prérequis

- Java 17 (ou tout JDK récent) – les versions plus anciennes fonctionnent mais vous manquerez le sucre `var`.  
- Aspose.Cells for Java (l'essai gratuit fonctionne bien pour cette démonstration).  
- Une connaissance de base de la syntaxe Java et des formules Excel.

Si vous êtes nouveau avec les **dynamic arrays java**, ne vous inquiétez pas — ce guide explique chaque élément.

---

## Étape 1 : Configurer votre projet et importer Aspose.Cells

Tout d'abord, ajoutez la dépendance Maven Aspose.Cells à votre `pom.xml` (ou récupérez le JAR manuellement).

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- latest as of June 2026 -->
</dependency>
```

> **Astuce :** Gardez vos dépendances à jour ; les versions plus récentes améliorent la vitesse d'évaluation des formules, ce qui compte lorsque vous **comment utilisez reduce** dans de grandes feuilles.

---

## Étape 2 : Créer un classeur et accéder à la première feuille de calcul

Nous allons maintenant créer un tout nouveau classeur. C'est la base pour apprendre **comment utiliser reduce** car l'objet workbook nous fournit un bac à sable où déposer des formules.

```java
// Step 2: Initialize a new workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx in memory
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet by default
```

*Pourquoi c'est important :* La classe `Workbook` représente l'ensemble du fichier Excel, tandis que `Worksheet` représente un seul onglet. Vous verrez plus tard comment les **dynamic arrays java** peuvent remplir de nombreuses cellules à partir d'une seule formule placée en A1.

---

## Étape 3 : Générer un tableau vertical avec EXPAND

La fonction `EXPAND` d'Excel peut déverser des valeurs dans une plage. Nous l'utiliserons pour créer les nombres 1 à 5 dans la colonne A.

```java
// Step 3: Write an EXPAND formula to produce 1‑5 vertically
Cell expandCell = worksheet.getCells().get("A1");
expandCell.setFormula("=EXPAND({1},5,1)"); // {1} is the seed, 5 rows, 1 column
expandCell.calculate(); // forces the engine to evaluate the formula now
```

Si vous ouvrez le classeur résultant, les cellules A1:A5 afficheront 1, 2, 3, 4, 5. C'est la partie **dynamic arrays java** — une formule remplit toute une plage.

---

## Étape 4 : Écrire une lambda REDUCE pour additionner le tableau

C'est ici que nous répondons à la question principale : **comment utiliser reduce** dans Excel depuis Java. La fonction `REDUCE` parcourt un tableau, en appliquant une lambda que vous fournissez. Dans notre cas, nous additionnerons les nombres.

```java
// Step 4: Use REDUCE with a LAMBDA to compute the sum of A1:A5
Cell reduceCell = worksheet.getCells().get("B1");
reduceCell.setFormula(
    "=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))"
);
reduceCell.calculate(); // forces evaluation immediately
```

Décomposons cela :

- `0` – la valeur initiale de l'accumulateur (`acc`).  
- `A1:A5` – le tableau que nous avons généré avec **EXPAND**.  
- `LAMBDA(acc, x, acc + x)` – la **lambda formula Excel** qui ajoute chaque élément (`x`) à l'accumulateur (`acc`).  

Lorsque la formule s'exécute, `B1` finit par contenir **15**, la **somme avec reduce** des nombres 1‑5.

> **Comment écrire une lambda** dans Excel ? Considérez‑la comme une fonction anonyme où les premiers arguments sont les paramètres, et l'expression finale est la valeur de retour. En Java, nous incorporons simplement le texte ; le moteur Excel effectue le travail lourd.

---

## Étape 5 : Enregistrer le classeur

Enfin, nous persistons le classeur sur le disque afin que vous puissiez l'ouvrir dans Excel, Google Sheets ou tout visualiseur supportant le format `.xlsx`.

```java
// Step 5: Persist the workbook
String outputPath = "YOUR_DIRECTORY/new-functions.xlsx";
workbook.save(outputPath);
System.out.println("Workbook saved to " + outputPath);
```

Ouvrez le fichier et vous verrez :

| A | B |
|---|---|
| 1 | 15 |
| 2 |   |
| 3 |   |
| 4 |   |
| 5 |   |

La **somme avec reduce** apparaît en B1, confirmant que nous avons démontré avec succès **comment utiliser reduce** avec une **lambda formula Excel** depuis Java.

---

## Exemple complet fonctionnel

Ci-dessous se trouve le programme Java complet, prêt à être exécuté. Copiez‑collez‑le dans votre IDE, ajustez le répertoire de sortie, et cliquez sur **Run**.

```java
import com.aspose.cells.*;

public class ReduceLambdaDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ EXPAND – generate vertical array 1‑5 in A1:A5
        Cell expandCell = worksheet.getCells().get("A1");
        expandCell.setFormula("=EXPAND({1},5,1)");
        expandCell.calculate(); // evaluate now

        // 3️⃣ REDUCE – sum the values using a lambda
        Cell reduceCell = worksheet.getCells().get("B1");
        reduceCell.setFormula("=REDUCE(0, A1:A5, LAMBDA(acc, x, acc + x))");
        reduceCell.calculate(); // evaluate now

        // 4️⃣ Save the workbook
        String outPath = "new-functions.xlsx";
        workbook.save(outPath);
        System.out.println("Workbook created at: " + outPath);
    }
}
```

**Sortie attendue** lorsque vous ouvrez `new-functions.xlsx` :

- Les cellules **A1:A5** contiennent `1, 2, 3, 4, 5`.  
- La cellule **B1** affiche `15`, confirmant la **somme avec reduce**.

---

## Questions fréquentes & cas limites

### Et si j'ai besoin d'un tableau horizontal au lieu d'un vertical ?

Inversez les arguments colonne/ligne dans `EXPAND`. Pour un débordement horizontal de B1 à F1 :

```java
expandCell.setFormula("=EXPAND({1},1,5)");
```

### Puis‑je utiliser REDUCE pour multiplier au lieu d'additionner ?

Absolument. Il suffit de modifier le corps de la lambda :

```java
reduceCell.setFormula("=REDUCE(1, A1:A5, LAMBDA(acc, x, acc * x))");
```

Maintenant B1 affichera `120` (5 ! = 120).

### Aspose.Cells prend‑il en charge les fonctions LAMBDA personnalisées ?

Oui, vous pouvez définir des fonctions LAMBDA nommées via la collection `Names` du classeur, puis les appeler comme n'importe quelle formule intégrée. C’est un sujet plus approfondi pour un futur tutoriel sur **comment écrire lambda** des fonctions qui vivent au‑delà d'une seule cellule.

### Qu'en est‑il des versions plus anciennes d'Excel qui ne reconnaissent pas REDUCE ?

Si vous ciblez Excel 2019 ou antérieur, le moteur renverra `#NAME?`. Dans de tels cas

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Maîtriser Aspose.Cells Java : comment interrompre le calcul des formules dans les classeurs Excel](/cells/english/java/calculation-engine/master-aspose-cells-java-interrupt-formula-calculation-workbook/)
- [Comment convertir les noms de cellules Excel en indices avec Aspose.Cells for Java : guide étape par étape](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)
- [Comment créer et formater des cellules Excel avec Aspose.Cells for Java : guide étape par étape](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}