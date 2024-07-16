---
keywords: Experience Platform;beheren, tags;tags;
title: Verenigde tags beheren
description: Dit document bevat informatie over het beheer van uniforme tags in Adobe Experience Cloud
exl-id: 179b0618-3bd3-435c-9d17-63681177ca47
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 0%

---

# Handleiding voor tags beheren

Met labels kunt u metagegevenstaxonomieën beheren om bedrijfsobjecten te classificeren voor eenvoudigere detectie en categorisering. Tags kunnen belangrijke taxonomische kenmerken identificeren voor het publiek waarmee uw teams zullen werken, zodat ze deze sneller kunnen vinden en ook het algemene publiek in een descriptor kunnen groeperen. U zou gemeenschappelijke markeringscategorieën zoals geografische gebieden, bedrijfseenheden, productlijnen, projecten, teams, tijdwaaiers (kwarten, maanden, jaren), of om het even wat anders moeten identificeren die betekenis kunnen toepassen en publieksontdekking voor uw team vergemakkelijken. 

## Een tag maken {#create-tag}

Als u een nieuwe tag wilt maken, selecteert u **[!UICONTROL tags]** in de linkernavigatie en selecteert u vervolgens de gewenste tagcategorie.

![ selecteer een markeringscategorie ](./images/tag-selection.png)

Selecteer **[!UICONTROL Create tag]** om een nieuwe tag te maken.

![ creeer een nieuwe markering ](./images/new-tag.png)

Het dialoogvenster **[!UICONTROL Create tag]** wordt weergegeven en u wordt gevraagd een unieke tagnaam in te voeren. Selecteer **[!UICONTROL Save]** als u klaar bent.

![ creeer markeringsdialoog met nieuwe markeringsnaam ](./images/create-tag-dialog.png)

De nieuwe tag wordt gemaakt en u wordt omgeleid naar het scherm met tags, waar de nieuwe tag in de lijst wordt weergegeven.

![ Nieuw gecreeerde markering voor de markeringscategorie ](./images/new-tag-listed.png)

## Een tag bewerken {#edit-tag}

Als u een tag bewerkt, kunt u beter spelfouten, naamgevingsupdates of terminologische updates gebruiken. Als u een tag bewerkt, blijft de koppeling van de tag behouden met alle objecten waarop de tag momenteel is toegepast.

Als u een bestaande tag wilt bewerken, selecteert u in de lijst met tagcategorieën de ellips (`...`) naast de naam van de tag die u wilt bewerken. In een vervolgkeuzelijst worden besturingselementen weergegeven voor het bewerken, verplaatsen of archiveren van de tag. Selecteer **[!UICONTROL Edit]** in de vervolgkeuzelijst.

![ geeft actie uit die in dropdown ](./images/edit-action.png) wordt getoond

Het dialoogvenster **[!UICONTROL Edit tag]** verschijnt waarin u wordt gevraagd de tagnaam te bewerken. Selecteer **[!UICONTROL Save]** als u klaar bent.

![ geef markeringsdialoog met bijgewerkte markeringsnaam ](./images/edit-dialog.png) uit

De tagnaam wordt bijgewerkt en u wordt omgeleid naar het scherm Tags, waar de bijgewerkte tag in de lijst wordt weergegeven.

![ Bijgewerkte markering voor de markeringscategorie ](./images/updated-tag-listed.png)

## Een tag verplaatsen tussen categorieën {#move-tag}

Tags kunnen naar andere tagcategorieën worden verplaatst. Als u een tag verplaatst, blijft de koppeling van de tag behouden met alle objecten waarop de tag momenteel is toegepast.

Als u een bestaande tag wilt verplaatsen, selecteert u in de lijst met tagcategorieën de ellips (`...`) naast de naam van de tag die u wilt verplaatsen. In een vervolgkeuzelijst worden besturingselementen weergegeven voor het bewerken, verplaatsen of archiveren van de tag. Selecteer **[!UICONTROL Edit]** in de vervolgkeuzelijst.

![ actie van de Beweging die in dropdown ](./images/move-action.png) wordt getoond

Het dialoogvenster **[!UICONTROL Move tag]** verschijnt waarin u wordt gevraagd de tagcategorie te selecteren waarnaar de geselecteerde tag moet worden verplaatst.

U kunt in de lijst bladeren en selecteren, maar u kunt ook de zoekfunctie gebruiken om de categorienaam in te voeren. Selecteer **[!UICONTROL Move]** als u klaar bent.

![ de markeringsdialoog van de beweging met onderzoekscriteria om markeringscategorie ](./images/move-dialog.png) te vinden

De tag wordt verplaatst en u wordt omgeleid naar het scherm met tags, waar de bijgewerkte taglijst wordt weergegeven en waar de tag niet meer wordt weergegeven.

![ Bijgewerkte markeringslijst voor de huidige markeringscategorie ](./images/current-tag-category.png)

De tag wordt nu weergegeven in de eerder geselecteerde tagcategorie.

![ lijst van de Markering voor de geselecteerde markeringscategorie om de markering ](./images/moved-to-tag-category.png) te bewegen

## Een tag archiveren {#archive-tag}

U kunt de status van een tag wijzigen tussen actief en gearchiveerd. Gearchiveerde labels worden niet verwijderd van objecten waarop ze al zijn toegepast, maar kunnen niet meer worden toegepast op nieuwe objecten. Voor elke tag wordt dezelfde status weerspiegeld in alle objecten. Dit is vooral handig wanneer u de huidige tag-objectkoppelingen wilt behouden, maar niet wilt dat de tag in de toekomst wordt gebruikt.

Als u een bestaande tag wilt archiveren, selecteert u in de lijst met tagcategorieën de ellips (`...`) naast de naam van de tag die u wilt archiveren. In een vervolgkeuzelijst worden besturingselementen weergegeven voor het bewerken, verplaatsen of archiveren van de tag. Selecteer **[!UICONTROL Archive]** in de vervolgkeuzelijst.

![ actie van het Archief die in dropdown ](./images/archive-action.png) wordt getoond

Het dialoogvenster **[!UICONTROL Archive tag]** wordt weergegeven en u wordt gevraagd het tagarchief te bevestigen. Selecteer **[!UICONTROL Archive]**.

![ dialoog van de de markeringsvraag van het Archief bevestiging ](./images/archive-dialog.png)

De tag wordt gearchiveerd en u wordt omgeleid naar het tagscherm. In de bijgewerkte taglijst wordt nu de status van de tag als `Archived` weergegeven.

![ Bijgewerkte markeringslijst voor de huidige markeringscategorie die markering tonen zoals gearchiveerd ](./images/archive-status.png)

## Een gearchiveerde tag herstellen {#restore-archived-tag}

Als u een tag `Archived` op nieuwe objecten wilt toepassen, moet de tag de status `Active` hebben. Als u een gearchiveerde tag herstelt, wordt de status `Active` van de tag hersteld.

Als u een gearchiveerde tag wilt herstellen, selecteert u in de lijst met tagcategorieën de ellips (`...`) naast de naam van de tag die u wilt herstellen. In een vervolgkeuzelijst worden besturingselementen weergegeven om de tag te herstellen of te verwijderen. Selecteer **[!UICONTROL Restore]** in de vervolgkeuzelijst.

![ herstel actie die in dropdown ](./images/restore-action.png) wordt getoond

Het dialoogvenster **[!UICONTROL Restore tag]** wordt weergegeven en u wordt gevraagd het herstellen van de tag te bevestigen. Selecteer **[!UICONTROL Restore]**.

![ herstel de dialoog van de markeringsvraag om bevestiging ](./images/restore-dialog.png)

De tag wordt hersteld en u wordt omgeleid naar het tagscherm. In de bijgewerkte taglijst wordt nu de status van de tag als `Active` weergegeven.

![ bijgewerkte markeringslijst voor de huidige markeringscategorie die markering als actief tonen ](./images/restored-active-status.png)

## Een tag verwijderen {#delete-tag}

>[!NOTE]
>
>Alleen tags in de status `Archived` die niet aan objecten zijn gekoppeld, kunnen worden verwijderd.

Als u een tag verwijdert, wordt deze volledig uit het systeem verwijderd.

Als u een gearchiveerde tag wilt verwijderen, selecteert u in de lijst met tagcategorieën de ellips (`...`) naast de naam van de tag die u wilt verwijderen. In een vervolgkeuzelijst worden besturingselementen weergegeven om de tag te herstellen of te verwijderen. Selecteer **[!UICONTROL Delete]** in de vervolgkeuzelijst.

![ actie van de Schrapping die in dropdown ](./images/delete-action.png) wordt getoond

Het dialoogvenster **[!UICONTROL Delete tag]** verschijnt waarin u wordt gevraagd de verwijdering van tags te bevestigen. Selecteer **[!UICONTROL Delete]**.

![ de tagdialoog van de Schrapping om bevestiging te verzoeken ](./images/delete-dialog.png)

De tag wordt verwijderd en u wordt omgeleid naar het tagscherm. Het label wordt niet meer in de lijst weergegeven en is volledig verwijderd.

![ bijgewerkte markeringslijst voor de huidige markeringscategorie die markering tonen verschijnt niet meer in de lijst ](./images/deleted-updated-list.png)

## Gelabelde objecten weergeven {#view-tagged}

Elke tag heeft een detailpagina die toegankelijk is via de taginventaris. Deze pagina bevat een lijst met alle objecten waarop dat label is toegepast, zodat gebruikers gerelateerde objecten van verschillende apps en mogelijkheden in één weergave kunnen bekijken.

Als u de lijst met gelabelde objecten wilt weergeven, zoekt u de tag in een categorie met tags en selecteert u de tag.

![ selectie van de markering binnen de markeringscategorie ](./images/view-tag-selection.png)

De pagina [!UICONTROL Tagged objects] wordt weergegeven met een overzicht van gelabelde objecten.

![ Overzicht van geëtiketteerde voorwerpen ](./images/tagged-objects.png)

## Volgende stappen

U hebt nu geleerd hoe u tags kunt beheren. Voor een overzicht op hoog niveau van markeringen in Experience Platform, gelieve te verwijzen naar de [ documentatie van het markeringsoverzicht ](../overview.md).
