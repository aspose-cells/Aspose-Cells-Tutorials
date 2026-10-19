---
category: general
date: 2026-06-30
description: Définir un format de nombre personnalisé dans Excel avec Java. Apprenez
  à créer un classeur Excel en Java, à récupérer la date et l’heure d’une cellule,
  à calculer les formules du classeur et à afficher la valeur de date‑heure.
draft: false
keywords:
- set custom number format
- get datetime from cell
- create excel workbook java
- calculate workbook formulas
- output datetime value
language: fr
og_description: Définir un format de nombre personnalisé dans Excel avec Java. Ce
  guide montre comment créer un classeur Excel en Java, récupérer la date et l’heure
  d’une cellule, calculer les formules du classeur et restituer la valeur de date
  et d’heure.
og_title: Définir un format de nombre personnalisé dans Excel avec Java – Tutoriel
  complet
schemas:
- author: Aspose
  dateModified: '2026-06-30'
  description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  headline: Set Custom Number Format in Excel with Java – Complete Guide
  type: TechArticle
- description: Set custom number format in Excel using Java. Learn how to create Excel
    workbook Java, get datetime from cell, calculate workbook formulas and output
    datetime value.
  name: Set Custom Number Format in Excel with Java – Complete Guide
  steps:
  - name: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
    text: The **set custom number format** was applied (you can open the generated
      `.xlsx` in Excel to see “令和2年4月1日”).
  - name: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
    text: The **calculate workbook formulas** step succeeded, turning the era string
      into a real date.
  - name: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
    text: The **get datetime from cell** call returned a proper `Calendar`, which
      we then **output datetime value** to the console.
  type: HowTo
tags:
- Java
- Excel
- Aspose.Cells
- DateTime
title: Définir un format de nombre personnalisé dans Excel avec Java – Guide complet
url: /fr/java/formatting/set-custom-number-format-in-excel-with-java-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Définir un format de nombre personnalisé dans Excel avec Java – Guide complet

Vous avez déjà eu besoin de **définir un format de nombre personnalisé** dans une feuille Excel en travaillant avec Java ? Vous n'êtes pas le seul. Que vous construisiez un moteur de reporting ou que vous essayiez simplement d'afficher correctement les dates de l'ère japonaise, maîtriser cette astuce vous fait gagner d'innombrables heures de post‑traitement. Dans ce tutoriel, nous parcourrons un exemple réel qui **crée un classeur Excel en Java**, applique un format spécifique à la locale, recalculera les formules, et enfin **récupère le DateTime depuis la cellule** pour **afficher la valeur datetime**.

Nous utiliserons la populaire bibliothèque Aspose.Cells for Java car elle gère les formats de nombre et les dates sensibles à la culture dès le départ. À la fin du guide, vous disposerez d'un programme autonome et exécutable que vous pourrez intégrer à n'importe quel projet Maven ou Gradle. Pas de raccourcis vagues du type « voir la documentation » — seulement du code solide et des explications claires.

---

## Ce que vous apprendrez

- Comment **créer un classeur Excel en Java** de manière programmatique.
- Les étapes exactes pour **définir un format de nombre personnalisé** pour les dates de l'ère japonaise.
- Pourquoi appeler **calculate workbook formulas** est essentiel avant d'extraire la valeur.
- La bonne façon de **get datetime from cell** et **output datetime value**.
- Les pièges courants (locale manquante, formules obsolètes) et les solutions rapides.

## Prérequis

- Java 8 ou version plus récente installé sur votre machine.  
- Aspose.Cells for Java 23.11 (ou toute version récente).  
- Un IDE ou éditeur de texte basique — IntelliJ IDEA, Eclipse, VS Code, ce que vous préférez.  

Si vous n'avez pas encore ajouté Aspose.Cells à votre projet, collez le fragment Maven suivant dans votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.11</version>
</dependency>
```

Les utilisateurs de Gradle peuvent ajouter :

```gradle
implementation 'com.aspose:aspose-cells:23.11'
```

Maintenant que l'environnement est prêt, plongeons dans le code.

---

## Étape 1 : Définir un format de nombre personnalisé – Vue d’ensemble

Avant d'écrire du Java, il est utile de visualiser ce que nous recherchons. Imaginez une cellule Excel qui doit afficher **« 令和2年4月1日 »** au lieu de la chaîne ISO‑8601 « 2020‑04‑01 ». La valeur sous‑jacente reste une vraie date (les formules fonctionnent toujours), mais l’*affichage* suit le format de l’ère japonaise. C’est exactement ce que réalise l’opération **set custom number format**.

Ci-dessous le fichier source complet. N'hésitez pas à le copier‑coller dans `src/main/java/SetCustomNumberFormatDemo.java`.

```java
// File: SetCustomNumberFormatDemo.java
import com.aspose.cells.*;

public class SetCustomNumberFormatDemo {
    public static void main(String[] args) throws Exception {
        // -------------------------------------------------
        // 1️⃣ Create Excel workbook Java – a fresh workbook
        // -------------------------------------------------
        Workbook workbook = new Workbook();               // in‑memory workbook, no file yet

        // -------------------------------------------------
        // 2️⃣ Access the first worksheet
        // -------------------------------------------------
        Worksheet worksheet = workbook.getWorksheets().get(0);

        // -------------------------------------------------
        // 3️⃣ Retrieve cell A1 where we’ll store the date string
        // -------------------------------------------------
        Cell cellA1 = worksheet.getCells().get("A1");

        // -------------------------------------------------
        // 4️⃣ Insert a Japanese era date string (Reiwa 2‑04‑01)
        // -------------------------------------------------
        // Note: Aspose.Cells will treat this as a text value until we recalc.
        cellA1.putValue("R02-04-01");

        // -------------------------------------------------
        // 5️⃣ Apply the custom number format (our primary goal)
        // -------------------------------------------------
        // [$-ja-JP] tells Excel to use the Japanese locale.
        // ggge年m月d日 renders as "令和2年4月1日".
        cellA1.setNumberFormat("[$-ja-JP]ggge年m月d日");

        // -------------------------------------------------
        // 6️⃣ Calculate workbook formulas – crucial step!
        // -------------------------------------------------
        // Without this, the cell remains a plain string and the
        // DateTime conversion below will fail.
        workbook.calculateFormula();

        // -------------------------------------------------
        // 7️⃣ Get DateTime from cell – now the value is a true date
        // -------------------------------------------------
        // The getDateTime() method returns a java.util.Calendar instance.
        java.util.Calendar dt = cellA1.getDateTime();

        // -------------------------------------------------
        // 8️⃣ Output datetime value – see the result in console
        // -------------------------------------------------
        System.out.println("Converted DateTime: " + dt.getTime()); // → Tue Apr 01 00:00:00 UTC 2020
    }
}
```

### Pourquoi cela fonctionne

- **`setNumberFormat`** indique à Excel comment *afficher* la valeur numérique sous‑jacente. La chaîne de format `[$-ja-JP]ggge年m月d日` est la clé ; `ggg` sélectionne le nom de l’ère, `e` l’année au sein de l’ère, suivi des littéraux du mois et du jour.  
- **`calculateFormula`** force Aspose.Cells à interpréter le texte « R02-04-01 » comme une date selon le calendrier japonais. Ignorer cette étape laisse la cellule en texte brut, et `getDateTime()` lèverait une exception.  
- **`getDateTime`** extrait enfin le *véritable* objet `java.util.Calendar`, que vous pouvez manipuler, formater ou stocker ailleurs.

## Étape 2 : Créer un classeur Excel en Java – Analyse approfondie

Lorsque vous **créez un classeur Excel en Java**, vous n’allouez pas seulement de la mémoire ; vous établissez également des styles par défaut, une feuille de calcul par défaut et une culture par défaut (généralement la locale du système). Si vous avez besoin d’une locale par défaut différente, vous pouvez passer un objet `LoadOptions` :

```java
LoadOptions opts = new LoadOptions(LoadFormat.XLSX);
opts.setLocale(new java.util.Locale("ja", "JP"));
Workbook workbook = new Workbook(opts);
```

Dans la plupart des scénarios, le constructeur simple suffit, mais il est bon de connaître l’alternative — surtout lorsque vous gérez plusieurs locales dans la même application.

*Astuce :* Gardez toujours le classeur en mémoire jusqu’à ce que vous ayez terminé le formatage. Écrire sur le disque après chaque modification engendre un surcoût I/O inutile.

## Étape 3 : Récupérer le DateTime depuis la cellule – Gestion du résultat

La ligne `java.util.Calendar dt = cellA1.getDateTime();` effectue le travail lourd. En coulisses, Aspose.Cells convertit le numéro de série interne (le nombre de jours depuis le 31‑12‑1899) en un `Calendar`. Cette conversion respecte la locale du classeur, vous obtenez donc la bonne date grégorienne même si l’affichage utilise l’ère japonaise.

Si vous avez besoin d’un `java.time.LocalDate` (la nouvelle API), convertissez ainsi :

```java
java.time.LocalDate localDate = dt.toInstant()
        .atZone(java.time.ZoneId.systemDefault())
        .toLocalDate();
System.out.println("LocalDate: " + localDate); // 2020-04-01
```

Cela couvre le besoin de **output datetime value** tout en restant moderne.

## Étape 4 : Calculer les formules du classeur – Quand c’est important

Vous pourriez vous demander : *« Dois‑je vraiment appeler `calculateFormula()` ? »* La réponse est un oui retentissant, sauf si vous alimentez la cellule avec un objet Java natif `Date` dès le départ. Lorsque vous **définissez un format de nombre personnalisé** sur une chaîne de texte, Excel (et Aspose.Cells) la traitent comme une expression de type formule qui nécessite une évaluation. Sans recalcul, `getDateTime()` renverra la valeur par défaut `1900‑01‑00` ou lèvera une `CellValueException`.

Si votre classeur contient déjà des formules complexes faisant référence à la cellule nouvellement formatée, appelez `calculateFormula()` *une fois* après tous les changements. Les appels répétés sont coûteux.

## Étape 5 : Afficher la valeur DateTime – Vérification du résultat

L’exécution de la démo affiche quelque chose comme :

```
Converted DateTime: Tue Apr 01 00:00:00 UTC 2020
```

Cette ligne confirme trois choses :

1. Le **set custom number format** a été appliqué (vous pouvez ouvrir le `.xlsx` généré dans Excel pour voir « 令和2年4月1日 »).  
2. L’étape **calculate workbook formulas** a réussi, transformant la chaîne d’ère en une vraie date.  
3. L’appel **get datetime from cell** a renvoyé un `Calendar` correct, que nous avons ensuite **output datetime value** sur la console.

Si vous ouvrez le classeur avec un programme de tableur, vous verrez le texte formaté, mais la valeur sous‑jacente de la cellule reste le numéro de série `43831` (la représentation Excel de 2020‑04‑01). Cette dualité est ce qui rend Excel puissant.

## Pièges courants & cas limites

| Issue | Why It Happens | Fix |
|-------|----------------|-----|
| `cellA1.getDateTime()` throws `CellValueException` | La cellule est encore une chaîne car `calculateFormula()` a été omis. | Toujours invoquer `workbook.calculateFormula()` après avoir défini une date texte qui nécessite une conversion. |
| Japanese era not displayed correctly | Code de locale manquant ou incorrect. | Utilisez `[$-ja-JP]` dans la chaîne de format, ou définissez la locale du classeur via `LoadOptions`. |
| Format shows “#VALUE!” in Excel | La chaîne de format est malformée. | Vérifiez à nouveau les crochets et les caractères ; le motif `ggge年m月d日` est requis pour l’année d’ère. |
| Time component appears (e.g., “00:00:00”) | La chaîne source inclut l’heure ou le style de la cellule l’ajoute. | Coupez la chaîne source ou ajustez le format à `ggge年m月d日;@`. |

## Exemple complet – Exécution en un clic

Si vous préférez un seul fichier sans commentaires supplémentaires, voici la version minimale :



## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Créer un classeur Excel avec Aspose.Cells en Java : Guide étape par étape](/cells/english/java/getting-started/create-excel-workbook-aspose-cells-java/)
- [Maîtriser la présentation des données dans Excel : Formatage des nombres et des dates personnalisées avec Aspose.Cells pour Java](/cells/english/java/formatting/aspose-cells-java-data-formatting-excel/)
- [Comment créer et formater des cellules Excel avec Aspose.Cells pour Java : Guide étape par étape](/cells/english/java/formatting/aspose-cells-java-excel-automation-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}