---
keywords: Experience Platform;huis;populaire onderwerpen;toegangsbeheer;op attribuut-gebaseerde toegangscontrole;ABAC
title: Op kenmerken gebaseerde toegangsbeheerfuncties voor rolmachtigingen beheren
description: Dit document bevat informatie over het configureren van machtigingen voor een rol via de interface voor machtigingen in Adobe Experience Cloud
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: c1c7a851315214e2362085d3283d144066d4dd8a
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 0%

---

# Machtigingen voor een rol beheren

>[!IMPORTANT]
>
>Het toegangsbeheer gebruikt gebruiker - identiteitskaart (een interne unieke identiteitskaart die aan een gebruiker wordt toegewezen) voor het verlenen van toestemmingen. Wanneer een organisatie van Adobe ID naar bedrijfs-id wordt gemigreerd, gaan alle machtigingen die voor de gebruikers zijn ingesteld, verloren omdat de gebruikers-id wordt gewijzigd en het toegangsbeheer de nieuwe gebruikers-id gebruikt. Als uw organisatie is gemigreerd naar bedrijfs-id, neemt u contact op met uw Adobe-vertegenwoordiger om uw gebruikersnaam te migreren van Adobe ID naar bedrijfs-id.

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

Als u een filter wilt verwijderen, selecteert u de X op het vulpictogram voor het desbetreffende filter of selecteert u **[!UICONTROL Clear all]** alle filters verwijderen.

![flitsklare filters](../../images/flac-ui/flac-clear-filters.png)

## Roldetails

Selecteer de rol in het menu **[!UICONTROL Roles]** , die de pagina met details van de rol opent.

![details van flac](../../images/flac-ui/flac-details.png)

Het tabblad Details geeft een overzicht van de rol. Het overzicht toont de rolnaam, rolbeschrijving, de naam van de gebruiker die de rol creeerde en wijzigde, toen de rol werd gecreeerd en, en de toestemmingen verbonden aan de rol werd gewijzigd. De rolnaam en rolbeschrijving kunnen indien nodig worden gewijzigd.

## Labels voor een rol beheren

Selecteer de **[!UICONTROL Labels]** tab om de pagina met rollabels te openen, en selecteer vervolgens **[!UICONTROL Add labels]** om labels aan de rol toe te wijzen.

![fc-labels](../../images/flac-ui/flac-labels.png)

Labels worden weergegeven op deze pagina. In de lijst staan de labelnaam, de vriendelijke naam, de categorie en de beschrijving.

Selecteer de labels in de lijst die u aan de rol wilt toevoegen en selecteer **[!UICONTROL Save]**

![flash-add-labels](../../images/flac-ui/flac-add-labels.png)

Toegevoegde labels worden weergegeven onder **[!UICONTROL Labels]** tab.

![met flac toegevoegde labels](../../images/flac-ui/flac-added-labels.png)

Als u een label uit een rol wilt verwijderen, selecteert u de optie **X** naast de naam van de labels.

![flash-delete-labels](../../images/flac-ui/flac-delete-labels.png)

## Sandboxen beheren voor rol

Selecteer de **[!UICONTROL Sandboxes]** om de pagina Rollen sandboxen te openen. Hier ziet u een lijst met sandboxen die aan de rol zijn toegevoegd.

![vlc-sandboxen](../../images/flac-ui/flac-sandboxes.png)

Als u meer sandboxen aan een rol wilt toevoegen, selecteert u **[!UICONTROL Edit]**.

![flash-add-sandboxen](../../images/flac-ui/flac-add-sandboxes.png)

Het volgende scherm zet u ertoe aan om te kiezen welke middeltoestemmingen die in zandbakken bestaan om in de rol te omvatten gebruikend dropdown. Selecteer **[!UICONTROL Save and exit]**.

![flash-add-role-permission](../../images/flac-ui/flac-add-role-permission.png)

## Gebruikers beheren voor rol

Selecteer de **[!UICONTROL Users]** tab om de pagina met rolgebruikers te openen, en selecteer vervolgens **[!UICONTROL Add Users]** om gebruikers aan de rol toe te wijzen.

![gebruikers van flac](../../images/flac-ui/flac-users.png)

Selecteer de gebruikers in de lijst die u aan de rol wilt toevoegen. U kunt ook de zoekbalk gebruiken om naar de gebruiker te zoeken door de naam of het e-mailadres in te voeren en vervolgens **[!UICONTROL Save]**

![flash-add-users](../../images/flac-ui/flac-add-users.png)

Toegevoegde gebruikers worden weergegeven onder **[!UICONTROL Users]** tab.

![gebruikers met toegevoegde vlammen](../../images/flac-ui/flac-added-users.png)

Als u een gebruiker uit een rol wilt verwijderen, selecteert u de **X** naast de gebruikersnaam.

![gebruikers van flac-remove](../../images/flac-ui/flac-remove-users.png)

De volgende video is bedoeld om uw begrip van het creëren van een nieuwe rol en het leiden van gebruikers voor die rol te steunen.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## API-referenties voor rol beheren {#manage-api-credentials-for-role}

Selecteer de **[!UICONTROL API credentials]** tabblad om de pagina met rollen-API-referenties te openen en selecteer vervolgens **[!UICONTROL Add API credentials]** om API-referenties aan de rol toe te wijzen.

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

Selecteer de **[!UICONTROL User groups]** tabblad om de pagina Rollengroepen te openen en selecteer vervolgens **[!UICONTROL Add Groups]** om gebruikersgroepen toe te wijzen aan de rol.

![flash-user-groups](../../images/flac-ui/flac-user-groups.png)

Selecteer de gebruikersgroepen in de lijst die u aan de rol wilt toevoegen. U kunt ook de zoekbalk gebruiken om naar de gebruikersgroep te zoeken door de naam van de groep in te voeren en vervolgens **[!UICONTROL Save]**

![flash-add-user-groups](../../images/flac-ui/flac-add-user-groups.png)

Toegevoegde gebruikersgroep wordt weergegeven onder **[!UICONTROL User groups]** tab.

![flash-user-groups](../../images/flac-ui/flac-added-user-groups.png)

Als u een gebruikersgroep uit een rol wilt verwijderen, selecteert u de **X** naast de naam van de gebruikersgroep.

![flash-remove-user-groups](../../images/flac-ui/flac-remove-user-groups.png)

De **[!UICONTROL Remove user group]** wordt weergegeven en u wordt gevraagd het verwijderen te bevestigen.

![flash-confirm-user-groups-delete](../../images/flac-ui/flac-confirm-user-groups-delete.png)

U wordt teruggestuurd naar de **[!UICONTROL User groups]** tab.

## Gebruikers aan Experience Platform toevoegen via een rol

Als u een gebruiker aan een rol wilt toevoegen, meldt u zich aan bij de Admin Console en selecteert u **[!UICONTROL Add users]**

![product-profile-add-users](../../images/flac-ui/product-profile-add-users.png)

De **[!UICONTROL Add users to your team]** wordt weergegeven. Voer het e-mailadres, de voornaam (optioneel) en de achternaam (optioneel) van de gebruiker in.

Selecteer het potloodpictogram om producten en gebruikersgroepen te selecteren. Selecteer **[!UICONTROL Adobe Experience Platform]** selecteert u vervolgens **[!UICONTROL AEP-Default-All-Users]** selecteert u vervolgens  **[!UICONTROL Save]**.

![productprofiel](../../images/flac-ui/product-profile.png)

## Volgende stappen

Als u machtigingen hebt ingesteld, kunt u verdergaan met de volgende stap naar [gebruikers beheren](users.md).
