---
category: general
date: 2026-06-08
description: Obtenez la date et l'heure d’une cellule en utilisant Aspose.Cells Java
  et apprenez comment écrire une valeur dans une cellule Excel en quelques étapes
  seulement.
draft: false
keywords:
- get datetime from cell
- write value to excel cell
- Aspose.Cells Java date parsing
- Japanese era calendar Excel
- Excel formula recalculation Java
language: fr
og_description: Obtenez la date et l'heure à partir d'une cellule en utilisant Aspose.Cells
  Java. Ce tutoriel montre également comment écrire une valeur dans une cellule Excel
  de manière efficace.
og_title: Obtenir la date et l'heure d’une cellule dans Excel avec Java – Guide complet
schemas:
- author: Aspose
  dateModified: '2026-06-08'
  description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  headline: Get datetime from cell in Java Excel – Complete Guide
  type: TechArticle
- description: Get datetime from cell using Aspose.Cells Java and learn how to write
    value to excel cell in just a few steps.
  name: Get datetime from cell in Java Excel – Complete Guide
  steps:
  - name: What if the cell already contains a true Excel date?
    text: 'If `cell.getType()` returns `CellValueType.IS_DATE_TIME`, you can skip
      the recalculation step and read the value directly:'
  - name: How to process a whole column of era strings?
    text: 'Loop through the used range and apply the same settings once:'
  - name: Can I disable the Japanese era handling later?
    text: 'Yes—just flip the flag back:'
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
title: Obtenir la date et l'heure d’une cellule dans Java Excel – Guide complet
url: /fr/java/cell-operations/get-datetime-from-cell-in-java-excel-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Obtenir la date et l'heure d'une cellule dans Java Excel – Guide complet

Vous avez déjà eu besoin de **obtenir la date et l'heure d'une cellule** mais la valeur ressemble à une chaîne d'ère japonaise ? Vous n'êtes pas le seul. Dans de nombreuses feuilles de calcul héritées, les dates sont stockées sous la forme « Reiwa 3/04/01 », et extraire un `java.time.LocalDateTime` correct à partir de cela peut ressembler à décoder un message secret.  

Heureusement, Aspose.Cells for Java peut gérer la conversion pour vous, et pendant que nous y sommes, nous vous montrerons également comment **écrire une valeur dans une cellule Excel** afin que vous puissiez faire un aller‑retour des données sans compromettre la logique de la feuille.

Dans ce tutoriel, vous apprendrez :

* Comment créer un classeur et cibler une feuille de calcul spécifique.  
* Les étapes exactes pour activer le calendrier d'ère japonaise pour l'analyse.  
* Pourquoi vous devez recalculer les formules avant de lire la date.  
* Comment écrire une nouvelle valeur dans une cellule sans perdre le formatage.  

Pas d'outils externes, pas de magie—juste du code Java simple que vous pouvez intégrer dans n'importe quel projet Maven dès aujourd'hui.

---

## Prérequis

* **Java 8+** (l'exemple utilise l'API moderne `java.time`).  
* **Aspose.Cells for Java** ≥ 23.9.0 – ajoutez la dépendance via Maven ou Gradle.  
* Familiarité de base avec les concepts Excel (feuilles, cellules, formules).  

Si vous n'avez pas la bibliothèque, récupérez‑la depuis le référentiel officiel d'Aspose :

```xml
<!-- Maven -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9.0</version>
    <classifier>jdk17</classifier>
</dependency>
```

---

## Étape 1 : Créer un nouveau classeur et accéder à la première feuille de calcul

Pour commencer, nous avons besoin d'un nouvel objet `Workbook`. Considérez‑le comme l'ouverture d'un nouveau fichier Excel en mémoire.

```java
// Step 1: Initialize workbook and grab the first sheet
Workbook workbook = new Workbook();                     // creates an empty .xlsx
Worksheet worksheet = workbook.getWorksheets().get(0); // first (and only) sheet
```

*Pourquoi c'est important :*  
Créer le classeur de façon programmatique vous donne un contrôle total sur les paramètres avant que des données n'atteignent le système de fichiers. La première feuille (`index 0`) est celle où nous démontrerons à la fois la lecture et l'écriture.

---

## Étape 2 : Écrire une chaîne de date d'ère japonaise dans la cellule A1

Nous allons maintenant **écrire une valeur dans une cellule Excel** A1. Cela reflète un scénario réel où un utilisateur a saisi manuellement « Reiwa 3/04/01 ».

```java
// Step 2: Write the era date string into A1
Cell cell = worksheet.getCells().get("A1");
cell.putValue("Reiwa 3/04/01"); // raw string, not yet a date
```

*Astuce rapide :* `putValue` est polyvalent — il accepte les chaînes, les nombres, les dates et même les formules. Lorsque vous transmettez une simple chaîne, Aspose la stocke exactement telle quelle, ce qui est parfait pour notre démonstration.

---

## Étape 3 : Activer le calendrier d'ère japonaise pour l'analyse des dates

Par défaut, Aspose.Cells utilise le calendrier grégorien. Pour donner du sens à « Reiwa », nous basculons un paramètre.

```java
// Step 3: Turn on Japanese era calendar support
WorkbookSettings settings = workbook.getSettings();
settings.setUseJapaneseEraCalendar(true);
```

*Pourquoi activer cela ?*  
Le calendrier d'ère japonaise associe les noms d'ères (Reiwa, Heisei, Showa) à leurs équivalents grégoriens. Sans ce drapeau, la bibliothèque traiterait la chaîne comme du texte brut, et vous n'obtiendriez jamais un objet `DateTime` correct.

---

## Étape 4 : Recalculer les formules afin que la chaîne d'ère se convertisse en date grégorienne

Aspose ne parse pas automatiquement la chaîne en date. Au lieu de cela, il traite la cellule comme un résultat de formule après un passage de calcul.

```java
// Step 4: Force a recalculation to convert the era string
workbook.calculateFormula(); // processes all cells, including A1
System.out.println(cell.getDateTime()); // → 2021‑04‑01
```

Lorsque `calculateFormula()` s'exécute, le moteur reconnaît le motif d'ère, applique le calendrier japonais et stocke la date grégorienne résultante en interne. L'appel `getDateTime()` renvoie alors un `java.util.Date` (ou vous pouvez le convertir en `java.time`).

**Sortie attendue**

```
2021-04-01T00:00:00.000+00:00
```

---

## Étape 5 : Écrire une nouvelle valeur dans la même cellule (ou une autre cellule)

Supposons que vous deviez écraser la chaîne originale par une date ISO‑8601 propre. Voici comment **écrire une valeur dans une cellule Excel** en toute sécurité, en préservant le style de la cellule.

```java
// Step 5: Overwrite A1 with a formatted date string
java.time.LocalDateTime now = java.time.LocalDateTime.now();
cell.putValue(now); // Aspose will store it as a proper Excel date
// Optional: apply a date format style
Style style = cell.getStyle();
style.setNumber(14); // built‑in "m/d/yyyy" format
cell.setStyle(style);
```

*Ce qui se passe ?*  
`putValue` détecte le type `LocalDateTime` et le convertit en représentation du numéro de série d'Excel. Définir le format numérique garantit que la cellule affiche la date exactement comme vous l'attendez lorsqu'elle est ouverte dans Excel.

---

## Exemple complet fonctionnel

En rassemblant le tout, voici une classe Java unique que vous pouvez compiler et exécuter. Elle crée un classeur, écrit une chaîne d'ère, la convertit, puis enregistre le fichier.

```java
import com.aspose.cells.*;

public class JapaneseEraDateDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create workbook & get first sheet
        Workbook workbook = new Workbook();
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // 2️⃣ Write Japanese era date string to A1
        Cell cell = worksheet.getCells().get("A1");
        cell.putValue("Reiwa 3/04/01");

        // 3️⃣ Enable Japanese era calendar
        WorkbookSettings settings = workbook.getSettings();
        settings.setUseJapaneseEraCalendar(true);

        // 4️⃣ Recalculate so the string becomes a Gregorian date
        workbook.calculateFormula();
        System.out.println("Converted date: " + cell.getDateTime());

        // 5️⃣ Overwrite with a clean LocalDateTime (optional)
        java.time.LocalDateTime now = java.time.LocalDateTime.now();
        cell.putValue(now);
        Style style = cell.getStyle();
        style.setNumber(14); // m/d/yyyy
        cell.setStyle(style);

        // 6️⃣ Save the workbook
        workbook.save("output.xlsx");
        System.out.println("Workbook saved as output.xlsx");
    }
}
```

Exécutez cela avec `java -cp aspose-cells-23.9.jar;. JapaneseEraDateDemo` et ouvrez **output.xlsx**. Vous verrez la cellule A1 afficher la date actuelle, tandis que la console enregistre la valeur convertie « 2021‑04‑01 ».

---

## Gestion des cas limites et questions fréquentes

### Et si la cellule contient déjà une vraie date Excel ?

Si `cell.getType()` renvoie `CellValueType.IS_DATE_TIME`, vous pouvez ignorer l'étape de recalcul et lire directement la valeur :

```java
if (cell.getType() == CellValueType.IS_DATE_TIME) {
    System.out.println("Already a date: " + cell.getDateTime());
}
```

### Comment traiter une colonne entière de chaînes d'ère ?

Parcourez la plage utilisée et appliquez les mêmes paramètres une fois :

```java
Range used = worksheet.getCells().getMaxDisplayRange();
for (int row = 0; row < used.getRowCount(); row++) {
    Cell c = used.getCell(row, 0); // column A
    c.putValue(c.getStringValue()); // re‑assign to trigger parsing
}
workbook.calculateFormula();
```

### Puis‑je désactiver la gestion de l'ère japonaise plus tard ?

Oui—il suffit de réinitialiser le drapeau :

```java
settings.setUseJapaneseEraCalendar(false);
```

N'oubliez pas de recalculer à nouveau si vous modifiez le paramètre après avoir écrit des données.

---

## Astuces professionnelles et pièges

* **Performance :** Activer le calendrier d'ère japonaise ajoute un léger surcoût. Si vous n'en avez besoin que pour quelques cellules, envisagez d'activer le paramètre, de traiter, puis de le désactiver.  
* **Conscience de la locale :** La chaîne d'ère doit correspondre exactement au modèle « EraName yy/MM/dd ». Une faute d'orthographe de « Reiwa » (par ex., « Rewa ») laissera la cellule en texte brut.  
* **Format d'enregistrement :** `Workbook.save("output.xlsx")` écrit un fichier XLSX. Utilisez `"output.xls"` si vous avez besoin du format binaire plus ancien, mais notez que certaines fonctionnalités (comme le parsing d'ère) peuvent être limitées.

---

## Conclusion

Vous savez maintenant comment **obtenir la date et l'heure d'une cellule** lorsque la source utilise une notation d'ère japonaise, et vous avez également vu une méthode propre pour **écrire une valeur dans une cellule Excel** avec le formatage approprié. En basculant `setUseJapaneseEraCalendar(true)` et en forçant un recalcul de formule, Aspose.Cells comble le fossé entre les chaînes d'ère héritées et les dates grégoriennes modernes—tout cela avec quelques lignes de Java.

Et ensuite ? Essayez d'étendre ce modèle à d'autres calendriers culturels (thaï, hijri) ou de traiter par lots de grands classeurs en utilisant la même approche. Les mêmes principes—activer le bon calendrier, recalculer, puis lire/écrire—s'appliquent partout.

Vous avez un format de date difficile à décoder ? Laissez un commentaire ci‑dessous, et résolvons le problème ensemble. Bon codage !  

![Exemple d'obtention de la date et l'heure d'une cellule](https://example.com/images/get-datetime-from-cell.png "Exemple d'obtention de la date et l'heure d'une cellule")

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Maîtriser le système de date 1904 dans Excel avec Aspose.Cells Java pour des opérations de cellules efficaces](/cells/english/java/cell-operations/aspose-cells-java-configure-1904-date-system-excel/)
- [Comment implémenter le calcul récursif des cellules dans Aspose.Cells Java pour une automatisation Excel améliorée](/cells/english/java/calculation-engine/aspose-cells-java-recursive-cell-calculations/)
- [Comment convertir les noms de cellules Excel en indices avec Aspose.Cells pour Java : guide étape par étape](/cells/english/java/cell-operations/convert-excel-cell-names-to-indices-aspose-cells-java/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}