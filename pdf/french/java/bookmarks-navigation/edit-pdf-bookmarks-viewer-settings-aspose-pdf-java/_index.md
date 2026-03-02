---
date: '2025-12-19'
description: Apprenez à modifier la mise en page des pages PDF, à éditer les signets
  PDF et à personnaliser les paramètres du visualiseur avec Aspose.PDF pour Java.
  Maîtrisez la navigation et les préférences de mise en page pour une expérience utilisateur
  plus fluide.
keywords:
- edit PDF bookmarks Java
- Aspose.PDF viewer settings
- configure PDF navigation Java
title: 'Modifier la mise en page PDF en Java - modifier les signets et les paramètres'
url: /fr/java/bookmarks-navigation/edit-pdf-bookmarks-viewer-settings-aspose-pdf-java/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}

{{< blocks/products/pf/main-container >}}

{{< blocks/products/pf/tutorial-page-section >}}
# Modifier la mise en page PDF en Java : Modifier les signets et les paramètres

## Introduction
Naviguer dans des documents PDF complexes peut être fastidieux, surtout lorsque le paramètre **change PDF page layout** n’est pas configuré correctement ou que les signets pointent vers les mauvais emplacements. Dans ce tutoriel, vous apprendrez à **change PDF page layout**, **edit PDF bookmarks**, et **configure PDF viewer settings** en utilisant Aspose.PDF for Java. À la fin, vous aurez le contrôle complet sur la navigation, les destinations des signets et la façon dont le document est présenté aux lecteurs.

**Ce que vous apprendrez**
- Comment modifier les signets PDF existants afin qu’ils pointent vers le début d’une page.  
- Comment définir les destinations des signets lors de la création d’un PDF.  
- Comment modifier les préférences du visualiseur, comme la mise en page.  
- Conseils pratiques pour charger un document PDF en Java et optimiser les performances.

### Réponses rapides
- **Quelle est la méthode principale pour changer la mise en page PDF ?** Utilisez `PdfContentEditor.changeViewerPreference()` avec `ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE`.  
- **Puis‑je modifier les destinations des signets après la création d’un PDF ?** Oui – chargez le document, accédez au plan, et définissez un nouveau `ExplicitDestination`.  
- **Ai‑je besoin d’une licence pour ces fonctionnalités ?** Un essai gratuit suffit pour l’évaluation ; une licence complète supprime toutes les limitations.  
- **Quelle dépendance Maven est requise ?** `com.aspose:aspose-pdf:25.3` (ou ultérieure).  
- **Cette fonctionnalité est‑elle compatible avec Java 11 et supérieur ?** Absolument – Aspose.PDF prend en charge Java 8+.

## Qu’est‑ce que « change PDF page layout » ?
Modifier la mise en page PDF contrôle la façon dont les pages sont affichées dans un visualiseur — page unique, continue, vue double page, etc. Ajuster ce paramètre améliore la lisibilité, surtout pour les longs rapports ou catalogues.

## Pourquoi modifier les signets PDF et définir les destinations des signets ?
Les signets fonctionnent comme une table des matières. Des destinations précises garantissent que les lecteurs accèdent directement à la section souhaitée, réduisant la frustration et améliorant l’expérience utilisateur globale.

## Prérequis
- **Bibliothèques et dépendances** : Aspose.PDF for Java v25.3 ou ultérieure.  
- **Environnement** : JDK 8 ou plus récent, outil de construction Maven ou Gradle.  
- **Connaissances** : programmation Java de base et familiarité avec les concepts PDF.

## Configuration d’Aspose.PDF pour Java
### Installation Maven
```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-pdf</artifactId>
    <version>25.3</version>
</dependency>
```
### Installation Gradle
```gradle
implementation 'com.aspose:aspose-pdf:25.3'
```
**Acquisition de licence** : Commencez avec un essai gratuit ou demandez une licence temporaire pour un accès complet aux fonctionnalités. Envisagez d’acheter une licence permanente pour une utilisation en production.

### Initialisation de base
```java
import com.aspose.pdf.Document;

public class PDFSetup {
    public static void main(String[] args) {
        // Initialize document object
        Document pdfDocument = new Document("path/to/your/pdf");
        
        System.out.println("Aspose.PDF for Java initialized successfully.");
    }
}
```

## Guide de mise en œuvre
### Comment modifier la mise en page PDF en Java
**Vue d’ensemble** : Ajustez les préférences du visualiseur pour afficher les pages comme vous le souhaitez.

#### Initialisation de PdfContentEditor
```java
import com.aspose.pdf.facades.PdfContentEditor;
import com.aspose.pdf.facades.ViewerPreference;

PdfContentEditor editor = new PdfContentEditor();
editor.bindPdf("YOUR_DOCUMENT_DIRECTORY/input.pdf");
```
#### Modification des préférences du visualiseur
```java
editor.changeViewerPreference(ViewerPreference.PAGE_LAYOUT_SINGLE_PAGE);
```
#### Enregistrement du document mis à jour
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/settingViewerPreferences.pdf";
editor.save(outputDir);
```

### Comment modifier les signets PDF
**Vue d’ensemble** : Ajustez les signets existants afin qu’ils pointent précisément au début d’une page spécifique.

#### Accès aux signets
```java
import com.aspose.pdf.Document;
import com.aspose.pdf.ExplicitDestination;
import com.aspose.pdf.OutlineItemCollection;

Document pdfDocument = new Document("YOUR_DOCUMENT_DIRECTORY/input.pdf");
OutlineItemCollection pdfOutline = pdfDocument.getOutlines().get_Item(1);
```
#### Définition d’une nouvelle destination
```java
pdfOutline.setDestination(
    ExplicitDestination.createDestination(pdfDocument.getPages().get_Item(1),
        ExplicitDestinationType.FitH,
        pdfDocument.getPages().get_Item(1).getMediaBox().getHeight())
);
```
#### Enregistrement des modifications
```java
String outputDir = "YOUR_OUTPUT_DIRECTORY/bookmarkShouldPointToStartOfPage.pdf";
pdfDocument.save(outputDir);
```

### Comment définir la destination d’un signet lors de la création d’un PDF
**Vue d’ensemble** : Créez des signets qui dirigent les utilisateurs directement vers les emplacements souhaités dans un PDF nouvellement généré.

#### Création et configuration du signet
```java
import com.aspose.pdf.GoToAction;
import com.aspose.pdf.FitVExplicitDestination;

OutlineItemCollection pdfOutline_new = new OutlineItemCollection(pdfDocument.getOutlines());
pdfOutline_new.setTitle("Test Bookmark");
pdfOutline_new.setItalic(true);
pdfOutline_new.setBold(true);
```
#### Définition de la destination du signet
```java
pdfOutline_new.setAction(new GoToAction(
    new FitVExplicitDestination(pdfDocument.getPages().get_Item(2), 0)));
```
#### Ajout et enregistrement du PDF
```java
pdfDocument.getOutlines().add(pdfOutline_new);

String outputDir = "YOUR_OUTPUT_DIRECTORY/setDestinationWhileCreatingPDF.pdf";
pdfDocument.save(outputDir);
```

## Applications pratiques
1. **Livres numériques** – Assurez‑vous que chaque signet de chapitre atterrit en haut de la page pour une expérience de lecture fluide.  
2. **Manuels techniques** – Une navigation précise aide les ingénieurs à trouver rapidement les sections, surtout dans les gros PDF.  
3. **Catalogues de produits** – La mise en page en page unique rend la navigation dans les catalogues sur tablette plus intuitive.

## Considérations de performance
- **Optimisation des ressources** : Lors du traitement de gros PDF, utilisez `Document.optimizeResources()` pour réduire la consommation de mémoire.  
- **Gestion de la mémoire Java** : Fermez explicitement les flux et laissez le ramasse‑miettes récupérer les objets après le traitement.

## Problèmes courants et solutions
- **Les signets ne se mettent pas à jour** : Vérifiez que vous modifiez le bon index du plan (`get_Item(1)` fait référence au premier signet de niveau supérieur).  
- **La préférence du visualiseur n’est pas appliquée** : Assurez‑vous d’appeler `editor.save()` après avoir modifié les préférences ; sinon les changements restent uniquement en mémoire.  
- **Exceptions de licence** : Une licence d’essai peut ajouter des filigranes ; obtenez une licence complète pour la production.

## Foire aux questions
**Q : Quelle est la façon la plus simple de charger un document PDF en Java ?**  
R : Utilisez `new Document("path/to/file.pdf")` ; Aspose.PDF détecte automatiquement le format du fichier.

**Q : Puis‑je changer la mise en page sans utiliser PdfContentEditor ?**  
R : Oui, vous pouvez définir les préférences du visualiseur directement sur l’objet `Document` via `pdfDocument.getViewerPreferences().setPageLayout(...)`.

**Q : Le changement de la mise en page du visualiseur affecte‑t‑il l’impression ?**  
R : La mise en page du visualiseur n’influence que l’affichage à l’écran ; elle ne modifie pas la sortie imprimée.

**Q : Existe‑t‑il des limites au nombre de signets que je peux créer ?**  
R : Aucun plafond explicite, mais des arbres de plan très volumineux peuvent impacter les performances ; gardez‑les organisés.

**Q : Comment garantir que les destinations des signets sont précises après l’ajout ou la suppression de pages ?**  
R : Re‑calculez les destinations en utilisant les indices de pages actuels après toute modification structurelle.

## Ressources
- **Documentation** : [Aspose.PDF Java Reference](https://reference.aspose.com/pdf/java/)
- **Téléchargement** : [Latest Releases for Java](https://releases.aspose.com/pdf/java/)
- **Achat** : [Buy Aspose.PDF License](https://purchase.aspose.com/buy)
- **Essai gratuit** : [Try Aspose.PDF Free](https://releases.aspose.com/pdf/java/)
- **Licence temporaire** : [Request Temporary License](https://purchase.aspose.com/temporary-license)

---

**Dernière mise à jour** : 2025-12-19  
**Testé avec** : Aspose.PDF for Java v25.3  
**Auteur** : Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}

{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}