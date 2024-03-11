---
keywords: Experience Platform;home;populaire onderwerpen;sandboxgebruikersgids;sandboxhulplijn
solution: Experience Platform
title: Gebruiksaanwijzing voor sandbox
description: Dit document bevat stappen voor het uitvoeren van verschillende bewerkingen met betrekking tot sandboxen in de Adobe Experience Platform-gebruikersinterface.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: 0db23e475d6546ebb886a56d5915d023ea215125
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 0%

---

# Gebruiksaanwijzing voor sandbox

Dit document bevat stappen voor het uitvoeren van verschillende bewerkingen met betrekking tot sandboxen in de Adobe Experience Platform-gebruikersinterface.

## Sandboxen weergeven

Selecteer in de interface Platform de optie **[!UICONTROL Sandboxes]** in de linkernavigatie en selecteer vervolgens **[!UICONTROL Browse]** om de [!UICONTROL Sandboxes] dashboard. In het dashboard worden alle beschikbare sandboxen voor uw organisatie vermeld, inclusief de respectievelijke typen (productie of ontwikkeling).

![weergave-sandboxen](../images/ui/view-sandboxes.png)

## Schakelen tussen sandboxen

De sandboxindicator bevindt zich in de bovenste header van de platforminterface en geeft de titel van de sandbox weer waarin u zich momenteel bevindt, het gebied en het type van de sandbox.

![sandbox-indicator](../images/ui/sandbox-indicator.png)

Als u wilt schakelen tussen sandboxen, selecteert u de sandboxindicator en selecteert u de gewenste sandbox in de vervolgkeuzelijst.

![switch-interface](../images/ui/switcher-interface.png)

Als een sandbox is geselecteerd, wordt het scherm vernieuwd en wordt de door u geselecteerde sandbox bijgewerkt.

![sandbox-changed](../images/ui/sandbox-switched.png)

## Een nieuwe sandbox maken {#create}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxname"
>title="Naam sandbox"
>abstract="De naam van de sandbox is de tekst die aan de achterkant wordt gebruikt om een unieke id voor deze sandbox te maken."

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtitle"
>title="Sandbox-titel"
>abstract="De sandboxtitel is de weergavenaam die de sandbox in menu&#39;s en vervolgkeuzelijsten in de gehele interface van het Experience Platform vertegenwoordigt."

>[!NOTE]
>
>Voor het maken van een nieuwe sandbox moet u de sandbox toevoegen aan een rol in [[!UICONTROL Permissions]](../../access-control/abac/ui/permissions.md) voordat u het kunt gaan gebruiken. Als u wilt weten hoe u een sandbox voor een rol instelt, raadpleegt u de [sandboxen beheren voor een rol](../../access-control/abac/ui/permissions.md#managing-sandboxes-for-role) documentatie.

Gebruik de volgende video voor een snel overzicht van het gebruik van sandboxen in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Als u een nieuwe sandbox wilt maken, selecteert u **[!UICONTROL Create sandbox]** rechtsboven in het scherm.

![aanmaken-sandbox](../images/ui/create-sandbox.png)

De **[!UICONTROL Create sandbox]** wordt weergegeven. Als u een ontwikkelingssandbox maakt, selecteert u **[!UICONTROL Development]** in het vervolgkeuzevenster. Als u een nieuwe productiesandbox wilt maken, selecteert u **[!UICONTROL Production]**.

![sandbox-type](../images/ui/sandbox-type.png)

Nadat u het type hebt geselecteerd, geeft u de sandbox een naam en een titel. De titel moet leesbaar zijn en moet beschrijvend genoeg zijn om gemakkelijk te kunnen worden herkend. De naam van de sandbox is een id in kleine letters voor gebruik in API-aanroepen en moet daarom uniek en beknopt zijn. De naam van de sandbox moet beginnen met een letter, maximaal 256 tekens bevatten en mag alleen bestaan uit alfanumerieke tekens en afbreekstreepjes (-).

Selecteer **[!UICONTROL Create]**.

![sandbox-info](../images/ui/sandbox-info.png)

Als u de sandbox hebt gemaakt, vernieuwt u de pagina en verschijnt de nieuwe sandbox in het dialoogvenster **[!UICONTROL Sandboxes]** dashboard met de status &quot;[!UICONTROL Creating]&quot;. Nieuwe sandboxen nemen ongeveer 30 seconden in beslag om te worden ingericht door het systeem, waarna hun status verandert in &quot;[!UICONTROL Active]&quot;.

![new-sandbox](../images/ui/new-sandbox.png)

## Een sandbox opnieuw instellen

>[!WARNING]
>
>Hieronder volgt een lijst met uitzonderingen die kunnen voorkomen dat u de standaardproductiessandbox of een door de gebruiker gemaakte productiesandbox opnieuw instelt:
>* De standaardproductiesandbox kan niet opnieuw worden ingesteld als de identiteitsgrafiek die in de sandbox wordt gehost, ook door Adobe Analytics wordt gebruikt voor de [Cross-Device Analytics (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html?lang=nl) gebruiken.
>* De standaardproductiesandbox kan niet opnieuw worden ingesteld als de identiteitsgrafiek die in de sandbox wordt gehost, ook door Adobe Audience Manager wordt gebruikt voor de [Op mensen gebaseerde Doelen (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html?lang=nl).
>* De standaardproductiefandbox kan niet worden opnieuw ingesteld als het gegevens voor zowel eigenschappen CDA als PBD bevat.
>* Een door de gebruiker gemaakte productiesandbox die wordt gebruikt voor bidirectioneel segmentdelen met Adobe Audience Manager of Audience Core Service kan na een waarschuwingsbericht worden hersteld.
>* Voordat u een sandbox-reset start, moet u de composities handmatig verwijderen om ervoor te zorgen dat de bijbehorende publieksgegevens op de juiste wijze worden opgeschoond.

### Advertentiecomposities verwijderen

De compositie van het publiek is momenteel niet geïntegreerd met de functie voor het opnieuw instellen van de sandbox, zodat het publiek handmatig moet worden verwijderd voordat de sandbox opnieuw wordt ingesteld.

Selecteren **[!UICONTROL Audiences]** van de linkernavigatie en selecteer dan **[!UICONTROL Compositions]**.

![De [!UICONTROL Compositions] in de [!UICONTROL Audiences] werkruimte.](../images/ui/audiences.png)

Selecteer vervolgens de ellips (`...`) naast de eerste doelgroep en selecteer vervolgens **[!UICONTROL Delete]**.

![Het publieksmenu markeert de [!UICONTROL Delete] -optie.](../images/ui/delete-composition.png)

Er wordt een bevestiging van een geslaagde verwijdering weergegeven en u wordt teruggestuurd naar de **[!UICONTROL Compositions]** tab.

Herhaal bovenstaande stappen met al uw composities. Hiermee verwijdert u alle soorten publiek uit het overzicht van het publiek. Wanneer alle soorten publiek zijn verwijderd, kunt u de sandbox opnieuw instellen.

### Sandbox opnieuw instellen

Als u een productie- of ontwikkelingssandbox opnieuw instelt, worden alle bronnen verwijderd die aan die sandbox zijn gekoppeld (schema&#39;s, gegevenssets, enzovoort), terwijl de naam van de sandbox en de bijbehorende machtigingen behouden blijven. Deze &#39;schone&#39; sandbox blijft onder dezelfde naam beschikbaar voor gebruikers die er toegang toe hebben.

Selecteer de sandbox die u wilt herstellen in de lijst met sandboxen. Selecteer in het rechternavigatievenster dat wordt weergegeven **[!UICONTROL Sandbox reset]**.

![reset](../images/ui/reset.png)

Er verschijnt een dialoogvenster waarin u wordt gevraagd uw keuze te bevestigen. Selecteren **[!UICONTROL Continue]** om verder te gaan.

![resetwaarschuwing](../images/ui/reset-warning.png)

Voer in het laatste bevestigingsvenster de naam van de sandbox in het dialoogvenster in en selecteer **[!UICONTROL Reset]**.

![opnieuw bevestigen](../images/ui/reset-confirm.png)

## Een sandbox verwijderen

>[!WARNING]
>
>U kunt de standaardproductiesandbox niet verwijderen. Nochtans, om het even welke user-created productiesandbox die voor bidirectioneel segment het delen met wordt gebruikt [!DNL Audience Manager] of [!DNL Audience Core Service] kan na een waarschuwingsbericht worden verwijderd.

Als u een productie- of ontwikkelingssandbox verwijdert, worden alle bronnen die aan die sandbox zijn gekoppeld, inclusief de machtigingen, permanent verwijderd.

Selecteer de sandbox die u wilt verwijderen uit de lijst met sandboxen. Selecteer in het rechternavigatievenster dat wordt weergegeven **[!UICONTROL Delete]**.

![delete](../images/ui/delete.png)

Er verschijnt een dialoogvenster waarin u wordt gevraagd uw keuze te bevestigen. Selecteren **[!UICONTROL Continue]** om verder te gaan.

![delete-warning](../images/ui/delete-warning.png)

Voer in het laatste bevestigingsvenster de naam van de sandbox in het dialoogvenster in en selecteer  **[!UICONTROL Continue]**.

![delete-confirm](../images/ui/delete-confirm.png)

## Volgende stappen

Dit document laat zien hoe u sandboxen beheert in de gebruikersinterface van het Experience Platform. Voor informatie over het beheren van sandboxen met de sandbox-API raadpleegt u de [sandboxontwikkelaarshandleiding](../api/getting-started.md).
