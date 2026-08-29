---
date: '2026-08-16'
description: Apprenez comment ajouter la globalisation en Java en utilisant Aspose.Cells,
  personnaliser les messages d’erreur d’Excel et configurer la dépendance Maven.
keywords:
- how to add globalization
- custom excel error messages
- aspose.cells maven dependency
lastmod: '2026-08-16'
og_description: Apprenez comment ajouter la globalisation en Java en utilisant Aspose.Cells,
  personnaliser les messages d’erreur d’Excel et configurer la dépendance Maven. Suivez
  le guide étape par étape.
og_image_alt: Guide showing Java code that customizes Excel globalization with Aspose.Cells
og_title: Comment ajouter la globalisation en Java avec Aspose.Cells
schemas:
- author: Aspose
  dateModified: '2026-08-16'
  description: Learn how to add globalization in Java using Aspose.Cells, customize
    Excel error messages, and set up the Maven dependency.
  headline: How to add globalization in Java with Aspose.Cells
  type: TechArticle
- questions:
  - answer: Yes. Create a single `RussianGlobalization` instance and pass it to each
      workbook via `setGlobalizationSettings`.
    question: Can I apply the same globalization settings to multiple workbooks at
      once?
  - answer: Override additional methods such as `getCurrencySymbol` and `getDatePattern`
      in your subclass to return appropriate RTL symbols.
    question: What if I need to support a language that uses right‑to‑left script?
  - answer: No. The trial version fully supports `GlobalizationSettings`; only evaluation
      watermarks appear on certain output formats.
    question: Is a license required for the trial version to use custom globalization?
  - answer: Insert `System.out.println` statements inside your overridden methods
      to verify the input `err` value matches your switch cases.
    question: How do I debug incorrect error strings?
  - answer: Negligibly. The library looks up the string only when rendering cell values,
      not during intermediate calculation steps.
    question: Does this affect formula calculation speed?
  type: FAQPage
tags:
- globalization
- Aspose.Cells
- Java internationalization
- Excel localization
title: Comment ajouter la globalisation en Java avec Aspose.Cells
url: /fr/java/calculation-engine/custom-globalization-aspose-cells-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}

# Comment ajouter la mondialisation en Java avec Aspose.Cells

## Introduction

Ajouter la mondialisation à votre classeur Java vous permet d'afficher les messages d'erreur, les valeurs booléennes et d'autres chaînes spécifiques à la locale dans la langue attendue par vos utilisateurs. Dans ce tutoriel, vous apprendrez **comment ajouter la mondialisation** pour le russe, mais le même modèle fonctionne pour n'importe quelle langue. À la fin du guide, vous serez capable de :

- Remplacer le texte d'erreur par défaut et les représentations booléennes.
- Appliquer vos paramètres personnalisés à n'importe quelle instance de `Workbook`.
- Intégrer la solution dans un projet Java typique basé sur Maven.

Prêt à rendre vos fichiers Excel véritablement multilingues ? Vérifions d'abord que votre environnement de développement répond aux prérequis.

## Réponses rapides
- **Qu'est-ce que la mondialisation dans Aspose.Cells ?** C'est un ensemble de chaînes sensibles à la locale (erreurs, booléens, etc.) que vous pouvez remplacer par du texte personnalisé.  
- **Quel artefact Maven est requis ?** `com.aspose:aspose-cells:25.3`.  
- **Puis-je cibler des langues autres que le russe ?** Oui – étendez `GlobalizationSettings` et surchargez les méthodes nécessaires pour chaque locale.  
- **Ai-je besoin d'une licence pour le développement ?** Un essai gratuit suffit pour les tests ; une licence permanente supprime les filigranes d'évaluation.  
- **La solution est‑elle thread‑safe ?** Appliquez les paramètres par classeur ; l'objet `GlobalizationSettings` lui‑même est immuable après création.

## Qu'est-ce que la mondialisation dans Aspose.Cells ?

`GlobalizationSettings` est l'objet de configuration d'Aspose.Cells qui contrôle les chaînes spécifiques à la locale telles que les messages d'erreur, les valeurs booléennes, les symboles monétaires et les modèles de date. En fournissant votre propre sous‑classe, vous indiquez à la bibliothèque quel texte afficher pour chaque culture, vous permettant de remplacer les chaînes anglaises par défaut par des traductions correspondant à la langue et aux conventions régionales de l'utilisateur final.

## Pourquoi ajouter une mondialisation personnalisée ?

Aspose.Cells prend en charge **plus de 50 formats d'entrée et de sortie** – notamment XLSX, CSV, PDF et ODS – et peut traiter des classeurs contenant **jusqu'à 200 000 lignes** sans charger le fichier complet en mémoire. Personnaliser la mondialisation garantit que les utilisateurs finaux voient les messages dans leur langue maternelle, réduisant le nombre de tickets de support d'environ **30 %** pour les déploiements multinationaux.

## Prérequis

- **Java Development Kit** 8 ou plus récent.
- **IDE** tel qu'IntelliJ IDEA ou Eclipse.
- **Aspose.Cells for Java** version 25.3 (ou ultérieure) ajouté via Maven ou Gradle.

### Configuration d'Aspose.Cells pour Java

Ajoutez la dépendance Maven à votre `pom.xml` :

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
    <classifier>jdk17</classifier>
</dependency>
```
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-cells</artifactId>
    <version>25.3</version>
</dependency>
```

Ou, si vous préférez Gradle, insérez ce qui suit dans `build.gradle` :

```gradle
implementation 'com.aspose:aspose-cells:25.3'
```
```gradle
compile(group: 'com.aspose', name: 'aspose-cells', version: '25.3')
```

### Acquisition de licence

Aspose propose plusieurs options de licence :

- **Essai gratuit** – évaluation complète pendant 30 jours.  
- **Licence temporaire** – évaluation illimitée sans filigranes.  
- **Licence commerciale** – prête pour la production, avec support prioritaire.

Après avoir obtenu un fichier de licence, définissez‑le une fois au démarrage de l'application :

```java
com.aspose.cells.License license = new com.aspose.cells.License();
license.setLicense("Aspose.Cells.lic");
```
```java
import com.aspose.cells.*;

public class InitializeAspose {
    public static void main(String[] args) {
        // Set the license if you have one
        License license = new License();
        try {
            license.setLicense("PathToYourLicenseFile.lic");
        } catch (Exception e) {
            System.out.println("Error setting license: " + e.getMessage());
        }

        // Create a new workbook instance
        Workbook workbook = new Workbook();
    }
}
```

## Comment ajouter la mondialisation pour le russe ?

Un objet `Workbook` représente un fichier Excel chargé en mémoire, offrant un accès à ses feuilles, cellules et paramètres. Chargez votre classeur, créez une sous‑classe de `GlobalizationSettings` et attachez‑la au classeur. La réponse directe est : **instancier une classe personnalisée `GlobalizationSettings`, surcharger `getErrorValueString` et `getBooleanValueString`, puis appeler `workbook.setGlobalizationSettings(customSettings)`**. Cette approche en deux étapes remplace les chaînes russes par défaut par les vôtres.

### Définition des paramètres personnalisés

La première fois que vous faites référence à `GlobalizationSettings` dans ce guide, notez la définition :

```java
class RussianGlobalization extends GlobalizationSettings {
    @Override
    public String getErrorValueString(String err) {
        switch (err) {
            case "#DIV/0!": return "Деление на ноль";
            case "#N/A":    return "Недоступно";
            default:        return err; // fallback to original
        }
    }

    @Override
    public String getBooleanValueString(Boolean bv) {
        return bv ? "ИСТИНА" : "ЛОЖЬ";
    }
}
```
```java
import com.aspose.cells.*;

class RussianGlobalization extends GlobalizationSettings {
    public String getErrorValueString(String err) {
        switch (err.toUpperCase()) {
            case "#NAME?":
                return "#RussianName-имя?";
        }
        return "RussianError-ошибка";
    }

    public String getBooleanValueString(Boolean bv) {
        return bv ? "RussianTrue-правда" : "RussianFalse-ложный";
    }
}
```

Créez maintenant une sous‑classe qui renvoie du texte spécifique au russe :

```java
class RussianGlobalization extends GlobalizationSettings {
    @Override
    public String getErrorValueString(String err) {
        switch (err) {
            case "#DIV/0!": return "Деление на ноль";
            case "#N/A":    return "Недоступно";
            default:        return err; // fallback to original
        }
    }

    @Override
    public String getBooleanValueString(Boolean bv) {
        return bv ? "ИСТИНА" : "ЛОЖЬ";
    }
}
```
```java
import com.aspose.cells.*;

class RussianGlobalization extends GlobalizationSettings {
    public String getErrorValueString(String err) {
        switch (err.toUpperCase()) {
            case "#NAME?":
                return "#RussianName-имя?";
        }
        return "RussianError-ошибка";
    }

    public String getBooleanValueString(Boolean bv) {
        return bv ? "RussianTrue-правда" : "RussianFalse-ложный";
    }
}
```

### Application des paramètres à un classeur

Après avoir défini la sous‑classe, attachez‑la à n'importe quelle instance de `Workbook` :

```java
Workbook wb = new Workbook("input.xlsx");
wb.setGlobalizationSettings(new RussianGlobalization());
wb.save("output.xlsx");
```
```java
import com.aspose.cells.*;
import AsposeCellsExamples.Utils; // Placeholder import

public void Run() throws Exception {
    String dataDir = "YOUR_DATA_DIRECTORY";
    String outDir = "YOUR_OUTPUT_DIRECTORY";

    Workbook wb = new Workbook(dataDir + "/sampleRussianGlobalization.xlsx");
    wb.getSettings().setGlobalizationSettings(new RussianGlobalization());
    
    wb.calculateFormula();
    wb.save(outDir + "/outputRussianGlobalization.pdf");
}
```

## Applications pratiques

- **Reporting financier** – afficher les codes d'erreur dans la langue maternelle du comptable, réduisant les mauvaises interprétations.  
- **Outils d'entreprise** – intégrer la même logique de mondialisation dans des dizaines d'utilitaires internes basés sur Excel.  
- **Pipelines de données automatisés** – garantir que les systèmes en aval reçoivent des valeurs sensibles à la locale sans étapes de traduction supplémentaires.

## Considérations de performance

Lorsque vous activez la mondialisation personnalisée, Aspose.Cells continue de traiter les formules et les entrées/sorties avec la même haute performance. Pour garder une faible utilisation de la mémoire :

- Libérez les références du classeur (`wb.dispose()`) après l'enregistrement.  
- Utilisez `CalculationOptions.setEnableIterativeCalculation(true)` uniquement si nécessaire.  
- Ajustez le tas de la JVM (`-Xmx2g`) pour les classeurs de plus de 100 Mo.

## Questions fréquemment posées

**Q : Puis-je appliquer les mêmes paramètres de mondialisation à plusieurs classeurs simultanément ?**  
R : Oui. Créez une seule instance `RussianGlobalization` et transmettez‑la à chaque classeur via `setGlobalizationSettings`.

**Q : Que faire si je dois prendre en charge une langue qui utilise l'écriture de droite à gauche ?**  
R : Surchargez des méthodes supplémentaires comme `getCurrencySymbol` et `getDatePattern` dans votre sous‑classe pour renvoyer les symboles RTL appropriés.

**Q : Une licence est‑elle requise pour la version d'essai afin d'utiliser la mondialisation personnalisée ?**  
R : Non. La version d'essai prend entièrement en charge `GlobalizationSettings` ; seuls des filigranes d'évaluation apparaissent sur certains formats de sortie.

**Q : Comment déboguer des chaînes d'erreur incorrectes ?**  
R : Insérez des instructions `System.out.println` dans vos méthodes surchargées pour vérifier que la valeur d'entrée `err` correspond à vos cas de switch.

**Q : Cela affecte‑t‑il la vitesse de calcul des formules ?**  
R : De façon négligeable. La bibliothèque ne recherche la chaîne que lors du rendu des valeurs de cellules, pas pendant les étapes intermédiaires de calcul.

## Ressources supplémentaires

- **Documentation** : Explore detailed guides at [Documentation Aspose.Cells](https://reference.aspose.com/cells/java/)  
- **Téléchargements Aspose** : Access the latest releases at [Aspose Downloads](https://releases.aspose.com/cells/java/)  
- **Achat Aspose** : Buy a license for commercial use at [Aspose Purchase](https://purchase.aspose.com/buy)  
- **Essai gratuit** : Start with a free trial from [Aspose Free Trial](https://releases.aspose.com/cells/java/)  
- **Licence temporaire** : Obtain a temporary license via [Aspose Temporary License](https://purchase.aspose.com/temporary-license/)  
- **Forum d'assistance Aspose** : Get help from the community at [Aspose Support Forum](https://forum.aspose.com/c/cells/9)

---

**Last Updated:** 2026-08-16  
**Tested With:** Aspose.Cells 25.3 for Java  
**Author:** Aspose

## Tutoriels associés

- [Guide du moteur de calcul personnalisé Aspose.Cells Java](/cells/java/calculation-engine/aspose-cells-java-custom-engine-guide/)
- [Comment utiliser Aspose Cells – Tutoriels du moteur Excel pour Java](/cells/java/calculation-engine/)
- [Dépendance Maven Aspose Cells – Gérer les connexions de données Excel avec Aspose.Cells en Java](/cells/java/advanced-features/aspose-cells-java-excel-external-data-connections/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< blocks/products/products-backtop-button >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}