---
keywords: Experience Platform;thuis;populaire onderwerpen;verenigde markeringen;markeringen;
title: Overzicht van Unified Tags
description: Dit document bevat informatie over uniforme tags in Adobe Experience Platform
exl-id: a19e37c3-697a-4000-9cb8-d67478b47dc6
source-git-commit: 6977438d57dc8e1390812e58bf039ebc60cb830d
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 1%

---

# Overzicht van verenigde codes

Tags zijn een mogelijkheid van Adobe Experience Platform waarmee beheerders metagegevenstaxonomieën kunnen beheren om bedrijfsobjecten te classificeren voor een eenvoudigere detectie en categorisering. Tags zijn metagegevens die kunnen worden beschouwd als trefwoorden die kunnen worden gekoppeld aan een segment, gegevensset, reis of andere objecten, zodat zoekopdrachten naar dat object en verwante objecten kunnen worden uitgevoerd. Tags worden in twee typen geclassificeerd: gecategoriseerd en niet gecategoriseerd.

Categorieën organiseren tags in handige sets om meer context te bieden en het doel van een tag te definiëren. Een beheerder bepaalt welke gecategoriseerde markeringen voor gebruikers aan voorwerpen beschikbaar zijn toe te voegen. Nieuwe tags zonder categorieën kunnen ook online worden gemaakt in workflows waarin labels worden toegepast. Deze tags worden weergegeven in het gedeelte zonder categorie van de taginventaris. Tags kunnen door beheerders en gebruikers worden toegepast, ongeacht wie ze heeft gemaakt. Alle typen tags kunnen worden geselecteerd wanneer u deze toewijst aan een object, zoekt of filtert.

## Tagterminologie

Bij labelen worden de volgende onderdelen gebruikt:

| Terminologie | Definitie |
| --- | --- |
| Gearchiveerd | Een status voor een tag die de huidige koppelingen met objecten behoudt, maar die de tag beperkt van toepassing op andere objecten.  Gearchiveerde tags worden verborgen in de tagkiezer. |
| Object | An Experience Cloud item that can have a tag applied.  Voorbeelden: Segment, Reis, Dataset. |
| Tag | Tags zijn metagegevens en kunnen worden beschouwd als trefwoorden die kunnen worden gekoppeld aan een segment, gegevensset, reis of andere objecten, zodat zoekopdrachten naar dat object en verwante objecten kunnen worden uitgevoerd. |
| Tagcategorie | Tags voor categorieën groeperen in betekenisvolle sets voor een betere context of een beschrijving van het doel van de tag.  Beheerders beheren tagcategorieën en -tags binnen categorieën. |
| Niet-gecategoriseerde tag | Een nieuwe tag die wordt gemaakt in de regel waar tags worden toegepast. Deze tags kunnen door elke gebruiker worden gemaakt en toegepast, maar zijn niet aan een categorie gebonden.  Beheerders kunnen deze tags naar een categorie verplaatsen om deze uit te lijnen met andere, vergelijkbare tags. |

## Tags inventariseren

Tagcategorie en tagbeheer met behulp van de taginventaris is beschikbaar in de navigatie in het Experience Platform en Journey Optimizer. Wijzigingen in codes in de inventaris worden doorgevoerd in alle objecten die tags ondersteunen. Alle gebruikers kunnen de taginventaris openen en doorbladeren, maar het tagbeheer is beperkt tot systeem- en productbeheerders.

De inventarisatie van tags heeft drie hiërarchische niveaus, waarmee gebruikers tagcategorieën, tags binnen een categorie en afzonderlijke tags kunnen beheren. Wanneer gebruikers een individuele tag beheren, kunnen ze naar elk object navigeren waarop die tag momenteel is toegepast.

### Categorieën tags

Categorieën groeperen markeringen in zinvolle reeksen om grotere context te verstrekken of het doel van de markering te beschrijven. Als een tag uit een categorie bestaat, komt de naam van de categorie gevolgd door een dubbele punt voor de naam van de tag.

De volgende acties zijn mogelijk bij het gebruik van tagcategorieën:

* [Tagcategorie maken](./ui/tags-categories.md#create-tag-category)
* [Tagcategorie bewerken](./ui/tags-categories.md#edit-tag-category-edit-tag-category)
* [Tagcategorie verwijderen](./ui/tags-categories.md#delete-tag-category-delete-tag-category)

### Tags binnen een categorie beheren

>[!NOTE]
>
>Voor het beheren van tags voor Experience Cloud moet u een systeembeheerder of productbeheerder voor Adobe Experience Platform voor uw organisatie zijn, die een abonnement op Experience Cloud heeft.

Binnen een categorie (of de standaardgroep &#39;Niet gecategoriseerd&#39;) kunt u tags maken en beheren. De volgende acties zijn mogelijk bij het beheren van tags:

* [Een tag maken](./ui/managing-tags.md#create-a-tag-create-tag)
* [Een tag bewerken](./ui/managing-tags.md#edit-a-tag-edit-tag)
* [Een tag verplaatsen tussen categorieën](./ui/managing-tags.md#move-a-tag-between-categories-move-tag)
* [Een tag archiveren](./ui/managing-tags.md#archive-a-tag-archive-tag)
* [Een gearchiveerde tag herstellen](./ui/managing-tags.md#restore-an-archived-tag-restore-archived-tag)
* [Een tag verwijderen](./ui/managing-tags.md#delete-a-tag-delete-tag)
* [Gelabelde objecten weergeven](./ui/managing-tags.md#viewing-tagged-objects-view-tagged)
