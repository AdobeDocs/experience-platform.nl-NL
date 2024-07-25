---
keywords: Experience Platform;huis;populaire onderwerpen;toegangsbeheer;op attribuut-gebaseerde toegangscontrole;ABAC
title: Op kenmerken gebaseerde toegangsbeheerfuncties voor rolmachtigingen beheren
description: Dit document bevat informatie over het configureren van machtigingen voor een rol via de interface voor machtigingen in Adobe Experience Cloud
exl-id: 8acd2bb6-eef8-4b23-8fd8-3566c7508fe7
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
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

Onmiddellijk nadat [ creërend een nieuwe rol ](#create-a-new-role), bent u teruggekeerd aan het **[!UICONTROL Roles]** lusje. Als u machtigingen voor een bestaande rol bewerkt, selecteert u de rol op het tabblad **[!UICONTROL Roles]** . U kunt ook de filteroptie gebruiken om de resultaten te filteren om een rol te zoeken.

## Filterrollen

Selecteer het kanaalpictogram (![ pictogram van de Filter ](/help/images/icons/filter.png)) om een lijst van filtercontroles te tonen om smalle resultaten te helpen.

![ flc-filters ](../../images/flac-ui/flac-filters.png)

De volgende filters zijn beschikbaar voor rollen in UI:

| Filter | Beschrijving |
| --- | --- |
| [!UICONTROL Created between] | Selecteer een begindatum en/of een einddatum om een datumbereik te definiëren waarop de resultaten moeten worden gefilterd. |
| [!UICONTROL Created by] | Filteren op de maker van de rol door een gebruiker te selecteren in het vervolgkeuzemenu. |
| [!UICONTROL Modified between] | Selecteer een begindatum en/of een einddatum om een datumbereik te definiëren waarop de resultaten moeten worden gefilterd. |
| [!UICONTROL Modified by] | Filter op rolbepaling door een gebruiker van dropdown te selecteren. |

Als u een filter wilt verwijderen, selecteert u de &quot;X&quot; op het vulpictogram voor het desbetreffende filter of selecteert u **[!UICONTROL Clear all]** om alle filters te verwijderen.

![ flc-duidelijk-filters ](../../images/flac-ui/flac-clear-filters.png)

## Roldetails

Selecteer de rol op het tabblad **[!UICONTROL Roles]** , waarop de pagina met details voor de rol wordt geopend.

![ flac-details ](../../images/flac-ui/flac-details.png)

Het tabblad Details geeft een overzicht van de rol. Het overzicht toont de rolnaam, rolbeschrijving, de naam van de gebruiker die de rol creeerde en wijzigde, toen de rol werd gecreeerd en, en de toestemmingen verbonden aan de rol werd gewijzigd. De rolnaam en rolbeschrijving kunnen indien nodig worden gewijzigd.

## Labels voor een rol beheren

Selecteer het tabblad **[!UICONTROL Labels]** om de pagina met rollabels te openen en selecteer vervolgens **[!UICONTROL Add labels]** om labels aan de rol toe te wijzen.

![ fc-labels ](../../images/flac-ui/flac-labels.png)

Labels worden weergegeven op deze pagina. In de lijst staan de labelnaam, de vriendelijke naam, de categorie en de beschrijving.

Selecteer de labels in de lijst die u aan de rol wilt toevoegen en selecteer vervolgens **[!UICONTROL Save]**

![ flc-toe:voegen-etiketten ](../../images/flac-ui/flac-add-labels.png)

Toegevoegde labels worden weergegeven onder **[!UICONTROL Labels]** tab.

![ flc-toegevoegde-etiketten ](../../images/flac-ui/flac-added-labels.png)

Om een etiket uit een rol te verwijderen, selecteer het **X** pictogram naast de naam van de etiketten.

![ fc-schrapping-etiketten ](../../images/flac-ui/flac-delete-labels.png)

## Sandboxen beheren voor rol

Selecteer het tabblad **[!UICONTROL Sandboxes]** om de pagina Rollensandboxen te openen. Hier ziet u een lijst met sandboxen die aan de rol zijn toegevoegd.

![ flc-zandbakken ](../../images/flac-ui/flac-sandboxes.png)

Als u meer sandboxen aan een rol wilt toevoegen, selecteert u **[!UICONTROL Edit]** .

![ flc-toe:voegen-zandbakken ](../../images/flac-ui/flac-add-sandboxes.png)

Het volgende scherm zet u ertoe aan om te kiezen welke middeltoestemmingen die in zandbakken bestaan om in de rol te omvatten gebruikend dropdown. Selecteer **[!UICONTROL Save and exit]** als u klaar bent.

![ fc-toe:voegen-rol-toestemming ](../../images/flac-ui/flac-add-role-permission.png)

## Gebruikers beheren voor rol

Selecteer het tabblad **[!UICONTROL Users]** om de pagina Rollengebruikers te openen en selecteer vervolgens **[!UICONTROL Add Users]** om gebruikers aan de rol toe te wijzen.

![ flc-users ](../../images/flac-ui/flac-users.png)

Selecteer de gebruikers in de lijst die u aan de rol wilt toevoegen. U kunt ook de zoekbalk gebruiken om naar de gebruiker te zoeken door de naam of het e-mailadres in te voeren en vervolgens **[!UICONTROL Save]** te selecteren.

![ flc-toe:voegen-gebruikers ](../../images/flac-ui/flac-add-users.png)

Toegevoegde gebruikers worden weergegeven onder **[!UICONTROL Users]** tab.

![ fc-toegevoegde-gebruikers ](../../images/flac-ui/flac-added-users.png)

Om een gebruiker uit een rol te verwijderen, selecteer het **X** pictogram naast de gebruikersnaam.

![ flc-remove-users ](../../images/flac-ui/flac-remove-users.png)

De volgende video is bedoeld om uw begrip van het creëren van een nieuwe rol en het leiden van gebruikers voor die rol te steunen.

>[!VIDEO](https://video.tv.adobe.com/v/336081/?learn=on)

## API-referenties voor rol beheren {#manage-api-credentials-for-role}

Selecteer het tabblad **[!UICONTROL API credentials]** om de pagina met API-referenties voor rollen te openen en selecteer vervolgens **[!UICONTROL Add API credentials]** om API-referenties aan de rol toe te wijzen.

![ fc-api-geloofsbrieven ](../../images/flac-ui/flac-api-credentials.png)

Selecteer de API-referenties in de lijst die u aan de rol wilt toevoegen en selecteer vervolgens **[!UICONTROL Save]**

![ fc-add-api-credentials ](../../images/flac-ui/flac-add-api-credentials.png)

Toegevoegde API-referenties worden weergegeven onder **[!UICONTROL API credentials]** tab.

![ fc-added-api-geloofsbrieven ](../../images/flac-ui/flac-added-api-credentials.png)

Om een API geloofsbrieven van een rol te verwijderen, selecteer het **X** pictogram naast de API credentienaam.

![ fc-remove-api-geloofsbrieven ](../../images/flac-ui/flac-remove-api-credentials.png)

Het dialoogvenster **[!UICONTROL Remove API credentials]** verschijnt waarin u wordt gevraagd het verwijderen te bevestigen.

![ fc-confirm-api-credentials-delete ](../../images/flac-ui/flac-confirm-api-credentials-delete.png)

U wordt teruggestuurd naar het tabblad **[!UICONTROL API credentials]** .

## Gebruikersgroepen voor rollen beheren

Gebruikersgroepen zijn meerdere gebruikers die zijn gegroepeerd en die toegang hebben om dezelfde functies uit te voeren.

Selecteer het tabblad **[!UICONTROL User groups]** om de pagina Rollengebruikersgroepen te openen en selecteer vervolgens **[!UICONTROL Add Groups]** om gebruikersgroepen aan de rol toe te wijzen.

![ fc-user-groups ](../../images/flac-ui/flac-user-groups.png)

Selecteer de gebruikersgroepen in de lijst die u aan de rol wilt toevoegen. U kunt ook de zoekbalk gebruiken om naar de gebruikersgroep te zoeken door de naam van de groep in te voeren en vervolgens **[!UICONTROL Save]** te selecteren

![ fc-toe:voegen-gebruiker-groepen ](../../images/flac-ui/flac-add-user-groups.png)

Toegevoegde gebruikersgroepen worden weergegeven onder **[!UICONTROL User groups]** tab.

![ fc-toegevoegde-gebruiker-groepen ](../../images/flac-ui/flac-added-user-groups.png)

Om een gebruikersgroep uit een rol te verwijderen, selecteer het **X** pictogram naast de naam van de gebruikersgroep.

![ fc-remove-user-groups ](../../images/flac-ui/flac-remove-user-groups.png)

Het dialoogvenster **[!UICONTROL Remove user group]** verschijnt waarin u wordt gevraagd het verwijderen te bevestigen.

![ fc-confirm-user-groups-delete ](../../images/flac-ui/flac-confirm-user-groups-delete.png)

U wordt teruggestuurd naar het tabblad **[!UICONTROL User groups]** .

## Gebruikers aan Experience Platform toevoegen via een rol

Als u een gebruiker aan een rol wilt toevoegen, meldt u zich aan bij de Admin Console en selecteert u **[!UICONTROL Add users]**

![ product-profiel-toe:voegen-gebruikers ](../../images/flac-ui/product-profile-add-users.png)

Het dialoogvenster **[!UICONTROL Add users to your team]** wordt weergegeven. Voer het e-mailadres, de voornaam (optioneel) en de achternaam (optioneel) van de gebruiker in.

Selecteer het potloodpictogram om producten en gebruikersgroepen te selecteren, selecteer **[!UICONTROL Adobe Experience Platform]**, selecteer **[!UICONTROL AEP-Default-All-Users]** en selecteer vervolgens **[!UICONTROL Save]** .

![ product-profiel ](../../images/flac-ui/product-profile.png)

## Volgende stappen

Met gevestigde toestemmingen, kunt u aan de volgende stap te werk gaan [ gebruikers ](users.md) beheren.
