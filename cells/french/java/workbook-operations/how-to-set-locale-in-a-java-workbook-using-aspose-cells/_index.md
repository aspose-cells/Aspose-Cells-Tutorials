---
category: general
date: 2026-11-22
description: Apprenez comment définir la locale dans un classeur Java, changer la
  langue du classeur et régler le calendrier en japonais avec des exemples de code
  clairs.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- how to set locale
- change workbook language
- set locale to japanese
- how to set calendar
language: fr
lastmod: 2026-11-22
og_description: Comment définir rapidement la locale dans un classeur Java. Suivez
  ce tutoriel pour changer la langue du classeur, définir la locale en japonais et
  configurer le calendrier japonais.
og_image_alt: Screenshot showing how to set locale in a Java workbook
og_title: Comment définir la locale dans un classeur Java – guide étape par étape
schemas:
- author: Aspose
  dateModified: '2026-11-22'
  description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  headline: How to set locale in a Java workbook using Aspose.Cells
  type: TechArticle
- description: Learn how to set locale in a Java workbook, change workbook language,
    and set the calendar to Japanese with clear code examples.
  name: How to set locale in a Java workbook using Aspose.Cells
  steps:
  - name: Run the **FullLocaleExample** class.
    text: Run the **FullLocaleExample** class.
  - name: Open the generated `FullJapaneseLocale.xlsx` in Excel.
    text: Open the generated `FullJapaneseLocale.xlsx` in Excel.
  - name: 'Verify that:'
    text: 'Verify that:'
  type: HowTo
tags:
- Java
- Aspose.Cells
- Internationalization
- Workbook
title: How to set locale in a Java workbook using Aspose.Cells
url: /fr/java/workbook-operations/how-to-set-locale-in-a-java-workbook-using-aspose-cells/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Comment définir la locale dans un classeur Java avec Aspose.Cells

Définir la locale dans un classeur Java est une exigence courante lorsque vous devez adapter votre feuille de calcul à différentes régions. Dans ce guide, vous apprendrez comment définir la locale, changer la langue du classeur et définir le calendrier en japonais à l'aide de l'API Aspose.Cells.

Internationaliser un classeur va au-delà de la traduction du texte ; cela influence également les formats numériques, l'analyse des dates et le système de calendrier par défaut. À la fin de ce tutoriel, vous serez capable de :

* Configurer la locale du classeur en japonais (Japon) – **set locale to japanese**.  
* Changer la langue du classeur afin que les formules et les chaînes d'interface respectent la culture cible – **change workbook language**.  
* Passer le calendrier au calendrier impérial japonais – **how to set calendar**.  

Ces étapes fonctionnent avec n'importe quelle version récente d'Aspose.Cells pour Java (v23.9 ou ultérieure) et ne nécessitent qu'un environnement de développement Java standard.

## Prérequis

| Exigence | Raison |
|----------|--------|
| Java 8 or higher | La bibliothèque cible Java 8+. |
| Aspose.Cells for Java (v23.9+) | Fournit `Workbook`, `WorkbookSettings`, et les utilitaires de locale. |
| IDE (IntelliJ IDEA, Eclipse, or VS Code) | Pour compiler et exécuter l'exemple. |
| Basic knowledge of Java | Nécessaire pour comprendre les extraits de code. |

Ajoutez la dépendance Maven Aspose.Cells à votre `pom.xml` (ou téléchargez le JAR manuellement) :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>23.9</version>
    <classifier>jdk17</classifier> <!-- adjust for your JDK version -->
</dependency>
```

## Comment définir la locale et le calendrier dans un classeur

La première étape consiste à créer une instance de classeur et à obtenir son objet de paramètres. L'objet de paramètres expose les API de locale et de calendrier.

```java
import com.aspose.cells.Workbook;
import com.aspose.cells.WorkbookSettings;
import java.util.Locale;
import java.util.Calendar;

public class WorkbookLocaleDemo {
    public static void main(String[] args) {
        // Step 1: Create a new workbook (empty by default)
        Workbook workbook = new Workbook();

        // Step 2: Access the workbook's settings
        WorkbookSettings settings = workbook.getSettings();

        // Step 3: Set the calendar to the Japanese calendar
        // Aspose.Cells uses java.util.Calendar; the Japanese calendar is available via Calendar.JAPANESE
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // Step 4: Set the locale to Japanese (Japan)
        // This influences number formats, date formats, and built‑in function behaviour.
        settings.setLocale(new Locale("ja", "JP"));

        // Optional: Save the workbook to verify the settings
        workbook.save("LocaleDemo.xlsx");
    }
}
```

### Pourquoi chaque ligne est importante

* **`new Workbook()`** – Instancie un classeur vide que vous pouvez manipuler avant de l'enregistrer.  
* **`getSettings()`** – Retourne un objet `WorkbookSettings` ; toutes les options régionales se trouvent ici.  
* **`setCalendar(...)`** – Remplace le calendrier grégorien par défaut par le calendrier impérial japonais, affectant la façon dont les dates sont affichées et analysées.  
* **`setLocale(new Locale("ja","JP"))`** – Modifie la langue et les conventions régionales (par ex., les mois, les séparateurs décimaux). C’est le cœur de **how to set locale** pour le classeur.  

L'exécution du programme crée `LocaleDemo.xlsx`. Ouvrez-le dans Excel ou LibreOffice et vous verrez les noms de mois en japonais, les symboles monétaires du yen japonais, et les dates formatées selon le calendrier japonais.

## Modifier la langue du classeur (définir la locale en japonais)

Si votre objectif principal est de **change workbook language**, vous pouvez vous concentrer uniquement sur l'appel `setLocale`. L'extrait suivant isole cette étape :

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Change only the language to Japanese (Japan)
settings.setLocale(new Locale("ja", "JP"));
workbook.save("JapaneseLanguage.xlsx");
```

**Qu'est-ce qui change ?**  
* Les chaînes de format de cellule passent en japonais (par ex., `#,##0.00` devient `#,##0.00` avec le symbole yen).  
* Les noms des fonctions intégrées (comme `SUM`) restent en anglais car la locale des fonctions Excel est indépendante, mais les chaînes de dates et les messages d'erreur suivent les conventions japonaises.  

**Quand l'utiliser ?**  
* Lorsque vous avez besoin d'une feuille de calcul qui affiche les nombres et les dates pour un public japonais mais que le calendrier sous-jacent peut rester grégorien.  
* Pour les rapports exportés en PDF ou imprimés, afin de garantir que la langue visuelle correspond au marché cible.

## Comment définir le calendrier au calendrier japonais

Parfois, le besoin de **how to set calendar** est distinct de la locale. Pour les systèmes hérités qui stockent les dates dans l'ère impériale japonaise, vous devez définir explicitement le calendrier tout en conservant éventuellement la locale par défaut.

```java
Workbook workbook = new Workbook();
WorkbookSettings settings = workbook.getSettings();

// Set only the calendar; keep the default (US) locale
settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

// Verify the calendar by creating a date cell
int row = 0, column = 0;
workbook.getWorksheets().get(0).getCells().putValue(row, column, new java.util.Date());

// Save to see the Japanese era (e.g., "R3/04/01" for Reiwa 3)
workbook.save("JapaneseCalendar.xlsx");
```

**Points clés :**

- `Calendar.getInstance(Locale.JAPAN)` renvoie un `java.util.Calendar` configuré pour l'ère japonaise.  
- Le classeur affichera désormais les dates en utilisant les symboles d'ère (R pour Reiwa, H pour Heisei, etc.).  
- Ce paramètre n'affecte **pas** le format des nombres ni la langue de l'interface ; combinez-le avec `setLocale` si vous avez besoin des deux.

## Exemple complet de bout en bout

Ci-dessous se trouve un programme complet et exécutable qui démontre **how to set locale**, **change workbook language** et **set the calendar** dans un flux cohérent. Il ajoute également une cellule d'exemple pour illustrer l'effet.

```java
import com.aspose.cells.*;
import java.util.*;

public class FullLocaleExample {
    public static void main(String[] args) throws Exception {
        // Create a new workbook
        Workbook workbook = new Workbook();

        // Access settings
        WorkbookSettings settings = workbook.getSettings();

        // 1️⃣ Set the locale to Japanese (Japan) – changes language & number formats
        settings.setLocale(new Locale("ja", "JP"));

        // 2️⃣ Set the calendar to the Japanese imperial calendar
        settings.setCalendar(Calendar.getInstance(Locale.JAPAN));

        // 3️⃣ Add a sample date and number to visualize the changes
        Worksheet sheet = workbook.getWorksheets().get(0);
        Cells cells = sheet.getCells();

        // Date cell – will show Japanese era after applying the calendar
        cells.putValue(0, 0, new Date());

        // Number cell – will use Japanese Yen symbol and comma separator
        cells.putValue(1, 0, 1234567.89);

        // Apply a style to the number cell for currency formatting
        Style style = cells.getRows().get(1).getStyle();
        style.setNumber(3); // Built‑in currency format
        cells.getRows().get(1).setStyle(style);

        // Save the workbook
        workbook.save("FullJapaneseLocale.xlsx");
        System.out.println("Workbook created with Japanese locale and calendar.");
    }
}
```

**Sortie attendue :**  
L'ouverture de `FullJapaneseLocale.xlsx` montre la première cellule avec une date comme `R3/04/01` (Reiwa 3) et la deuxième cellule formatée en `¥1,234,567.89`. Cela confirme que **how to set locale**, **change workbook language** et **how to set calendar** fonctionnent tous ensemble.

## Pièges courants et comment les éviter

| Piège | Pourquoi cela se produit | Solution |
|-------|--------------------------|----------|
| Using `Locale.CHINA` instead of `new Locale("ja","JP")` | `Locale.CHINA` définit la langue chinoise, pas le japonais. | Instanciez toujours `Locale` avec `"ja", "JP"` pour le japonais. |
| Forgetting to call `settings.setCalendar(...)` after `setLocale` | Le calendrier par défaut est le grégorien, donc les dates apparaissent dans la mauvaise ère. | Appelez `setCalendar` **après** avoir défini la locale, ou définissez les deux ensemble comme indiqué. |
| Saving the workbook before applying settings | Les paramètres sont appliqués à l'objet en mémoire ; un enregistrement prématuré écrit la locale par défaut. | Appliquez tous les changements de locale/calendrier **avant** d'appeler `workbook.save()`. |
| Using an outdated Aspose.Cells version | Les versions antérieures ne disposent pas des surcharges `setCalendar`. | Mettez à jour vers v23.9+ ou consultez les notes de version pour la prise en charge des locales. |

## Tester votre configuration

1. Exécutez la classe **FullLocaleExample**.  
2. Ouvrez le fichier généré `FullJapaneseLocale.xlsx` dans Excel.  
3. Vérifiez que :  
   * La colonne de dates affiche les symboles d'ère japonais (`R`, `H`, etc.).  
   * La colonne de nombres utilise le symbole Yen et les séparateurs de virgules.  
   * Tous les messages d'erreur intégrés (par ex., `#DIV/0!`) apparaissent en japonais si le classeur contient des erreurs.  

Si l'une de ces vérifications échoue, revérifiez que l'objet `WorkbookSettings` que vous avez modifié est la même instance utilisée lors de l'enregistrement.

## Prochaines étapes

* **Localiser les formules** – Bien que la locale contrôle le formatage, vous pouvez également traduire les noms de fonctions personnalisées à l'aide de `FormulaParser`.  
* **Appliquer la locale aux classeurs existants** – Chargez un classeur avec `new Workbook

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s'appuient sur les techniques démontrées dans ce guide. Chaque ressource comprend des exemples de code complets et fonctionnels avec des explications étape par étape pour vous aider à maîtriser des fonctionnalités supplémentaires de l'API et explorer des approches d'implémentation alternatives dans vos propres projets.

- [Aspose Cells Date Format: How to Set Custom Date Format in Java](/cells/english/java/formatting/aspose-cells-date-format-how-to-set-custom-date-format-in-ja/)
- [How to Set Language in Excel Files Using Aspose.Cells .NET for Multilingual Support](/cells/english/net/formulas-functions/specify-language-excel-aspose-cells-net/)
- [How to set cell number format and convert Japanese dates in C# using Aspose.Cells](/cells/english/net/excel-custom-number-date-formatting/set-cell-number-format-and-convert-japanese-dates-in-c/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}