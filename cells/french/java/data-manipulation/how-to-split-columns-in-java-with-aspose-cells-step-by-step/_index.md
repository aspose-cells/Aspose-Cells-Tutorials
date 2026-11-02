---
category: general
date: 2026-10-07
description: Comment diviser les colonnes avec Aspose.Cells pour Java. Apprenez à
  séparer une chaîne en colonnes, automatiser une formule Excel et écrire une formule
  dans une cellule en quelques lignes de code.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to split columns
- split string into columns
- automate excel formula
- write formula to cell
language: fr
lastmod: 2026-10-07
og_description: Comment diviser des colonnes en Java avec Aspose.Cells. Ce tutoriel
  vous montre comment diviser une chaîne en colonnes, automatiser l'évaluation des
  formules Excel et écrire une formule dans une cellule.
og_image_alt: Screenshot of Java code that splits columns in an Excel worksheet using
  Aspose.Cells
og_title: Comment diviser des colonnes en Java avec Aspose.Cells – tutoriel rapide
schemas:
- author: Aspose
  dateModified: '2026-10-07'
  description: How to split columns using Aspose.Cells for Java. Learn to split string
    into columns, automate Excel formula, and write formula to cell in a few lines
    of code.
  headline: How to split columns in Java with Aspose.Cells – step‑by‑step guide
  type: TechArticle
tags:
- Aspose.Cells
- Java
- Excel automation
title: Comment diviser des colonnes en Java avec Aspose.Cells – guide étape par étape
url: /fr/java/data-manipulation/how-to-split-columns-in-java-with-aspose-cells-step-by-step/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment diviser des colonnes en Java avec Aspose.Cells – guide étape par étape

Si vous devez **diviser des colonnes** dans une feuille de calcul Excel de façon programmatique, ce guide vous montre le processus complet avec Aspose.Cells pour Java. Vous apprendrez également comment **diviser une chaîne en colonnes**, **automatiser l’évaluation d’une formule Excel**, et **écrire une formule dans une cellule** à l’aide d’un code concis, prêt pour la production.

La division de colonnes programmatique élimine le copier‑coller manuel, réduit les erreurs et permet des transformations de données à grande échelle. À la fin de ce tutoriel, vous pourrez générer, modifier et évaluer des formules à la volée, faisant d’Excel une véritable partie de votre backend Java.

## Prérequis

Avant de commencer, assurez‑vous d’avoir :

* Java 17 ou version ultérieure installé.
* Maven 3.8+ (ou Gradle) pour la gestion des dépendances.
* Une licence Aspose.Cells pour Java (la version d’évaluation gratuite suffit pour l’apprentissage).
* Une connaissance de base de la syntaxe Java et des concepts Excel.

Si l’un de ces éléments manque, installez‑le d’abord ; les extraits de code supposent un projet Maven standard.

## Étape 1 : Ajouter Aspose.Cells à votre projet

Ajoutez la dépendance suivante à votre `pom.xml`. Cela récupère la dernière version stable de la bibliothèque Aspose.Cells.

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>24.9</version> <!-- Use the latest version available -->
</dependency>
```

**Pourquoi cette étape est importante :** La bibliothèque fournit les classes `Workbook`, `Worksheet` et `Cell` nécessaires pour manipuler les fichiers Excel sans Microsoft Office. Sans cette dépendance, le code ne compilera pas.

## Étape 2 : Créer un classeur et sélectionner la première feuille

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Initialize a new workbook and access the first worksheet
        Workbook workbook = new Workbook();                     // creates an empty .xlsx file in memory
        Worksheet worksheet = workbook.getWorksheets().get(0); // first sheet is index 0
```

L’objet `Workbook` représente le fichier Excel complet. Accéder à la première feuille garantit un point de départ prévisible pour la formule que nous allons écrire.

## Étape 3 : Écrire la formule WRAPCOLS dans une cellule cible

```java
        // Step 3: Identify the target cell (A1) where the formula will be placed
        Cell targetCell = worksheet.getCells().get("A1");

        // Step 3: Write the WRAPCOLS formula to split a long string into three columns
        // WRAPCOLS(string, columns) distributes the string across the specified number of columns.
        targetCell.setFormula("=WRAPCOLS(\"This is a very long string that needs to be split\",3)");
```

**Pourquoi nous utilisons `WRAPCOLS` :** La fonction intégrée d’Excel `WRAPCOLS` découpe automatiquement une valeur texte unique en un nombre défini de colonnes, en gérant intelligemment les limites de mots. C’est la méthode la plus fiable pour **diviser une chaîne en colonnes** sans logique de parsing personnalisée.

## Étape 4 : Forcer le classeur à évaluer la formule

```java
        // Step 4: Calculate all formulas in the workbook so the result becomes visible
        workbook.calculateFormula();
```

L’appel à `calculateFormula()` **automatise l’évaluation de la formule Excel** côté serveur. Sans cet appel, la cellule contiendrait encore le texte de la formule, et non les valeurs calculées.

## Étape 5 : Récupérer et afficher le résultat découpé

```java
        // Step 5: Retrieve the computed value from the target cell
        String result = targetCell.getStringValue(); // returns the first column of the split result
        System.out.println("First column output: " + result);

        // Optionally, read the other columns created by WRAPCOLS
        String second = worksheet.getCells().get("B1").getStringValue();
        String third  = worksheet.getCells().get("C1").getStringValue();

        System.out.println("Second column output: " + second);
        System.out.println("Third column output: " + third);

        // Save the workbook to verify the split visually (optional)
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

Lorsque vous exécutez le programme, la console affiche :

```
First column output: This is a very long
Second column output: string that needs
Third column output: to be split
```

Le fichier généré `SplitColumnsResult.xlsx` montre les trois colonnes remplies avec le texte découpé.

## Comprendre la fonction WRAPCOLS

* **Syntaxe :** `WRAPCOLS(text, columns, [delimiter])`
* **Paramètres :**
  * `text` – la chaîne que vous souhaitez diviser.
  * `columns` – le nombre de colonnes sur lesquelles répartir le texte.
  * `delimiter` (facultatif) – caractère utilisé pour couper la chaîne ; la valeur par défaut est un espace.
* **Valeur de retour :** Un tableau qui se déverse dans les cellules adjacentes, chaque élément contenant une portion du texte original.

Comme la fonction se déverse horizontalement, vous n’avez besoin d’écrire la formule que dans la cellule la plus à gauche (A1 dans l’exemple). Excel remplit automatiquement B1, C1, … selon les besoins.

## Variantes courantes et cas limites

| Situation | Ajustement recommandé |
|-----------|-----------------------|
| **Nombre de colonnes variable** | Remplacez le `3` codé en dur par une variable : `targetCell.setFormula(String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount));` |
| **Délimiteur personnalisé** | Utilisez le troisième argument, par ex. `=WRAPCOLS(A2,4,",")` pour découper sur les virgules. |
| **Chaîne source vide** | La fonction renvoie des cellules vides ; protégez‑vous contre les `null` ou les chaînes vides avant de définir la formule. |
| **Jeux de données volumineux** | Appliquez la formule dans une boucle pour chaque ligne, puis appelez `calculateFormula()` une seule fois après la boucle pour améliorer les performances. |
| **Caractères non ASCII** | WRAPCOLS fonctionne avec Unicode ; assurez‑vous que votre fichier source Java est enregistré en UTF‑8. |

**Astuce :** Lors du traitement de nombreuses lignes, stockez la formule dans une variable chaîne et réutilisez‑la afin d’éviter le surcoût de concaténation répétée.

## Exemple complet, exécutable

Voici le programme complet prêt à être copié‑collé. Il inclut les déclarations d’import, la gestion des exceptions et une opération de sauvegarde optionnelle.

```java
import com.aspose.cells.*;

public class SplitColumnsExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook and access the first worksheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // Define the long string and desired column count
        String longString = "This is a very long string that needs to be split";
        int columnCount = 3;

        // Write the WRAPCOLS formula to cell A1
        Cell targetCell = worksheet.getCells().get("A1");
        String formula = String.format("=WRAPCOLS(\"%s\",%d)", longString, columnCount);
        targetCell.setFormula(formula);

        // Evaluate all formulas in the workbook
        workbook.calculateFormula();

        // Read and display each column's result
        System.out.println("First column output: " + worksheet.getCells().get("A1").getStringValue());
        System.out.println("Second column output: " + worksheet.getCells().get("B1").getStringValue());
        System.out.println("Third column output: " + worksheet.getCells().get("C1").getStringValue());

        // Save the workbook for visual verification
        workbook.save("SplitColumnsResult.xlsx");
    }
}
```

L’exécution de ce programme produit la même sortie console présentée précédemment et écrit un fichier Excel qui montre clairement **comment diviser des colonnes**.

## Checklist de dépannage

* **Formule non évaluée** – Vérifiez que `workbook.calculateFormula()` est appelé après la définition de la formule.
* **Cellules vides après la division** – Assurez‑vous que la chaîne source n’est pas `null` ou vide, et que le nombre de colonnes est supérieur à zéro.
* **Exception de licence** – Fournissez un fichier de licence Aspose.Cells valide (`License license = new License(); license.setLicense("Aspose.Total.lic");`) avant de créer le classeur pour supprimer les filigranes d’évaluation.
* **Lenteur sur de grandes feuilles** – Appelez `calculateFormula()` une seule fois après que toutes les formules aient été écrites, pas après chaque cellule individuelle.

## Conclusion

Vous savez maintenant **comment diviser des colonnes** en Java avec Aspose.Cells, comment **diviser une chaîne en colonnes** avec la fonction `WRAPCOLS`, comment **automatiser l’évaluation d’une formule Excel**, et comment **écrire une formule dans une cellule** de façon programmatique. Cette technique élimine les étapes manuelles de préparation des données et intègre les puissantes capacités de traitement de texte d’Excel directement dans vos applications Java.

### Prochaines étapes

* Explorez d’autres fonctions texte telles que `TEXTSPLIT` et `FILTERXML` pour des scénarios de parsing plus complexes.
* Combinez `WRAPCOLS` avec `IFERROR` pour gérer les entrées inattendues de façon élégante.
* Intégrez la solution dans un service Spring Boot qui reçoit des données CSV via REST et renvoie un fichier Excel rempli.

En maîtrisant ces modèles, vous pourrez créer des flux de travail Excel automatisés, robustes et évolutifs, adaptés aux besoins de votre entreprise. Bon codage !

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et à explorer des approches d’implémentation alternatives dans vos propres projets.

- [aspose cells java – Split Names into Columns](/cells/english/java/cell-operations/aspose-cells-java-split-names-columns/)
- [Auto-Fit Excel Columns in Java Using Aspose.Cells](/cells/english/java/formatting/aspose-cells-java-auto-fit-excel-columns-guide/)
- [How to Delete Blank Columns in Excel Using Aspose.Cells Java&#58; A Comprehensive Guide](/cells/english/java/worksheet-management/delete-blank-columns-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}