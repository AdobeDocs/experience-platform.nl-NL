---
keywords: Experience Platform;huis;populaire onderwerpen;toegangsbeheer;op attribuut-gebaseerde toegangscontrole;ABAC
title: Op kenmerken gebaseerde toegangsbeheerfuncties voor rolmachtigingen beheren
description: Dit document bevat informatie over op kenmerken gebaseerd toegangsbeheer in Adobe Experience Platform
hide: true
hidefromtoc: true
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: 02a17d8aed743b03219958cae2f0585f871e56f6
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# Machtigingen voor een rol beheren

>[!IMPORTANT]
>
>Op attributen-gebaseerde toegangscontrole is momenteel beschikbaar in een beperkte versie voor op VS-Gebaseerde gezondheidszorgklanten. Deze mogelijkheid is beschikbaar voor alle Real-time Customer Data Platform-klanten zodra deze volledig is vrijgegeven.

De toestemmingen zijn het gebied van Experience Cloud waar de beheerders gebruikersrollen en toegangsbeleid kunnen bepalen om toegangstoestemmingen voor eigenschappen en voorwerpen binnen een producttoepassing te beheren.

Door Toestemmingen, kunt u rollen tot stand brengen en beheren, evenals de gewenste middeltoestemmingen voor deze rollen toewijzen. Met machtigingen kunt u ook de labels, sandboxen en gebruikers beheren die aan een specifieke rol zijn gekoppeld.

Onmiddellijk na [een nieuwe rol creëren](#create-a-new-role), u bent teruggekeerd aan **[!UICONTROL Roles]** tab. Als u machtigingen bewerkt voor een bestaande rol, selecteert u de rol in het menu **[!UICONTROL Roles]** tab. U kunt ook de filteroptie gebruiken om de resultaten te filteren om een rol te zoeken.

## Filterrollen

Selecteer het trechter-pictogram (![Filterpictogram](../../images/icon.png)) om een lijst met filterbesturingselementen weer te geven om de resultaten te beperken.

![vlamfilters](../../images/flac-ui/flac-filters.png)

De volgende filters zijn beschikbaar voor rollen in UI:

| Filter | Beschrijving |
| --- | --- |
| [!UICONTROL Created between] | Selecteer een begindatum en/of een einddatum om een datumbereik te definiëren waarop de resultaten moeten worden gefilterd. |
| [!UICONTROL Created by] | Filteren op de maker van de rol door een gebruiker te selecteren in het vervolgkeuzemenu. |
| [!UICONTROL Modified between] | Selecteer een begindatum en/of een einddatum om een datumbereik te definiëren waarop de resultaten moeten worden gefilterd. |
| [!UICONTROL Modified by] | Filter op rolbepaling door een gebruiker van dropdown te selecteren. |

Als u een filter wilt verwijderen, selecteert u de X op het vulpictogram voor het desbetreffende filter of selecteert u **[!UICONTROL Clear all]** om alle filters te verwijderen.

![flitsklare filters](../../images/flac-ui/flac-clear-filters.png)

## Roldetails

Selecteer de rol in het menu **[!UICONTROL Roles]** , die de pagina met details van de rol opent.

![details](../../images/flac-ui/flac-details.png)

Het tabblad Details geeft een overzicht van de rol. Het overzicht toont de rolnaam, rolbeschrijving, de naam van de gebruiker die de rol creeerde en wijzigde, toen de rol werd gecreeerd en, en de toestemmingen verbonden aan de rol werd gewijzigd. De rolnaam en rolbeschrijving kunnen indien nodig worden gewijzigd.

## Labels voor een rol beheren

Selecteer **[!UICONTROL Labels]** tab om de pagina met rollabels te openen, en selecteer vervolgens **[!UICONTROL Add labels]** om labels aan de rol toe te wijzen.

![fc-labels](../../images/flac-ui/flac-labels.png)

Labels worden weergegeven op deze pagina. In de lijst staan de labelnaam, de vriendelijke naam, de categorie en de beschrijving.

Selecteer de labels in de lijst die u aan de rol wilt toevoegen en selecteer **[!UICONTROL Save]**

![flash-add-labels](../../images/flac-ui/flac-add-labels.png)

Toegevoegde labels worden weergegeven onder **[!UICONTROL Labels]** tab.

![met flac toegevoegde labels](../../images/flac-ui/flac-added-labels.png)

Als u een label uit een rol wilt verwijderen, selecteert u de optie **X** naast de naam van de labels.

![flash-delete-labels](../../images/flac-ui/flac-delete-labels.png)

## Sandboxen beheren voor rol

Selecteer **[!UICONTROL Sandboxes]** om de pagina Rollen sandboxen te openen. Hier ziet u een lijst met sandboxen die aan de rol zijn toegevoegd.

![vlc-sandboxen](../../images/flac-ui/flac-sandboxes.png)

Als u meer sandboxen aan een rol wilt toevoegen, selecteert u **[!UICONTROL Edit]**.

![flash-add-sandboxen](../../images/flac-ui/flac-add-sandboxes.png)

Het volgende scherm zet u ertoe aan om te kiezen welke middeltoestemmingen die in zandbakken bestaan om in de rol te omvatten gebruikend dropdown. Als u klaar bent, selecteert u **[!UICONTROL Save and exit]**.

![flash-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

## Gebruikers beheren voor rol

Selecteer **[!UICONTROL Users]** tab om de pagina met rolgebruikers te openen, en selecteer vervolgens **[!UICONTROL Add Users]** om gebruikers aan de rol toe te wijzen.

![gebruikers van flac](../../images/flac-ui/flac-users.png)

Selecteer de gebruikers in de lijst die u aan de rol wilt toevoegen. U kunt ook de zoekbalk gebruiken om naar de gebruiker te zoeken door de naam of het e-mailadres in te voeren en vervolgens **[!UICONTROL Save]**

![flash-add-users](../../images/flac-ui/flac-add-users.png)

Toegevoegde gebruikers worden weergegeven onder **[!UICONTROL Users]** tab.

![gebruikers met toegevoegde vlammen](../../images/flac-ui/flac-added-users.png)

Als u een gebruiker uit een rol wilt verwijderen, selecteert u de **X** naast de gebruikersnaam.

![gebruikers van flac-remove](../../images/flac-ui/flac-remove-users.png)

## API-referenties voor rol beheren

Selecteer **[!UICONTROL API credentials]** tabblad om de pagina met rollen-API-referenties te openen en selecteer vervolgens **[!UICONTROL Add API credentials]** om API-referenties aan de rol toe te wijzen.

![fc-api-credentials](../../images/flac-ui/flac-api-credentials.png)

Selecteer de API-referenties in de lijst die u wilt toevoegen aan de rol en selecteer vervolgens **[!UICONTROL Save]**

![flash-add-api-credentials](../../images/flac-ui/flac-add-api-credentials.png)

Toegevoegde API-referenties worden weergegeven onder **[!UICONTROL API credentials]** tab.

![flash-added-api-credentials](../../images/flac-ui/flac-added-api-credentials.png)

Als u API-referenties wilt verwijderen uit een rol, selecteert u de optie **X** naast de API-referentienaam.

![flash-remove-api-credentials](../../images/flac-ui/flac-remove-api-credentials.png)

De **[!UICONTROL Remove API credentials]** wordt weergegeven en u wordt gevraagd het verwijderen te bevestigen.

![flash-confirm-api-credentials-delete](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

U wordt teruggestuurd naar de **[!UICONTROL API credentials]** tab.

## Gebruikersgroepen voor rollen beheren

Gebruikersgroepen zijn meerdere gebruikers die zijn gegroepeerd en die toegang hebben om dezelfde functies uit te voeren.

Selecteer **[!UICONTROL User groups]** tab om de pagina met rolgebruikersgroepen te openen, en selecteer vervolgens **[!UICONTROL Add Groups]** om gebruikersgroepen toe te wijzen aan de rol.

![flash-user-groups](../../images/flac-ui/flac-user-groups.png)

Selecteer de gebruikersgroepen in de lijst die u aan de rol wilt toevoegen. U kunt ook de zoekbalk gebruiken om naar de gebruikersgroep te zoeken door de naam van de groep in te voeren en vervolgens **[!UICONTROL Save]**

![flash-add-user-groups](../../images/flac-ui/flac-add-user-groups.png)

Toegevoegde gebruikersgroep wordt weergegeven onder **[!UICONTROL User groups]** tab.

![flash-user-groups](../../images/flac-ui/flac-added-user-groups.png)

Als u een gebruikersgroep uit een rol wilt verwijderen, selecteert u de **X** naast de naam van de gebruikersgroep.

![flash-remove-user-groups](../../images/flac-ui/flac-remove-user-groups.png)

De **[!UICONTROL Remove user group]** wordt weergegeven en u wordt gevraagd het verwijderen te bevestigen.

![flash-confirm-user-groups -delete](../../images/flac-ui/flac-confirm-user-groups-delete.png)

U wordt teruggestuurd naar de **[!UICONTROL User groups]** tab.

## Volgende stappen

Als u machtigingen hebt ingesteld, kunt u verdergaan met de volgende stap naar [gebruikers beheren](users.md).
