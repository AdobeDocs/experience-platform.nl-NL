---
keywords: Experience Platform;home;populaire onderwerpen;sandbox-gebruikershandleiding;sandbox-hulplijn
solution: Experience Platform
title: Gebruiksaanwijzing voor sandbox
description: Dit document bevat stappen voor het uitvoeren van verschillende bewerkingen met betrekking tot sandboxen in de Adobe Experience Platform-gebruikersinterface.
exl-id: b258c822-5182-4217-9d1b-8196d889740f
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '1086'
ht-degree: 0%

---

# Gebruiksaanwijzing voor sandbox

Dit document bevat stappen voor het uitvoeren van verschillende bewerkingen met betrekking tot sandboxen in de Adobe Experience Platform-gebruikersinterface.

## Sandboxen weergeven

Selecteer in de gebruikersinterface van Experience Platform de optie **[!UICONTROL Sandboxes]** in de linkernavigatie en selecteer vervolgens de tab **[!UICONTROL Browse]** om het dashboard van [!UICONTROL Sandboxes] te openen. In het dashboard worden alle beschikbare sandboxen voor uw organisatie vermeld, inclusief de respectievelijke typen (productie of ontwikkeling).

![ het zandbakendashboard met het doorbladerlusje selecteerde dat een lijst van beschikbare zandbakken toont.](../images/ui/view-sandboxes.png)

## Schakelen tussen sandboxen

De sandboxindicator bevindt zich in de bovenste header van de gebruikersinterface van Experience Platform en geeft de titel van de sandbox weer waarin u zich momenteel bevindt, het gebied en het type van de sandbox.

![ het zandbakendashboard met de benadrukte zandbakindicator.](../images/ui/sandbox-indicator.png)

Als u wilt schakelen tussen sandboxen, selecteert u de sandboxindicator en selecteert u de gewenste sandbox in de vervolgkeuzelijst. U kunt ook naar de gewenste sandbox zoeken met de zoekfunctie in het vervolgkeuzemenu.

![ het dropdown menu van de zandbakindicator wordt getoond, tonend een lijst van zandbakken u toegang tot hebt.](../images/ui/switcher-interface.png)

Als een sandbox is geselecteerd, wordt het scherm vernieuwd en wordt de door u geselecteerde sandbox bijgewerkt.

![ het zandbakdashboard met de veranderde benadrukte zandbakindicator.](../images/ui/sandbox-switched.png)

## Een nieuwe sandbox maken {#create}

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxname"
>title="Naam sandbox"
>abstract="De naam van de sandbox is de tekst die aan de achterkant wordt gebruikt om een unieke id voor deze sandbox te maken."

>[!CONTEXTUALHELP]
>id="platform_sandboxes_sandboxtitle"
>title="Sandbox-titel"
>abstract="De sandboxtitel is de weergavenaam die de sandbox in menu&#39;s en vervolgkeuzelijsten in de gehele Experience Platform-gebruikersinterface vertegenwoordigt."

>[!WARNING]
>
>Wanneer u een nieuwe sandbox wilt maken, moet u deze toevoegen aan een rol in [[!UICONTROL Permissions]](../../access-control/abac/ui/permissions.md) voordat u deze kunt gebruiken. Leren hoe te om een zandbak voor een rol te verstrekken, verwijs naar [ het leiden zandbakken voor een rol ](../../access-control/abac/ui/permissions.md#managing-sandboxes-for-role) documentatie.

Gebruik de volgende video voor een snel overzicht van het gebruik van sandboxen in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Als u een nieuwe sandbox wilt maken, selecteert u **[!UICONTROL Create sandbox]** in de rechterbovenhoek van het scherm.

![ creeer-zandbak ](../images/ui/create-sandbox.png)

Het dialoogvenster **[!UICONTROL Create sandbox]** wordt weergegeven. Selecteer het vervolgkeuzemenu **[!UICONTROL Type]** en kies het type [!UICONTROL Development] of [!UICONTROL Production] sandbox.

![ creeer zandbak dialoogdoos met de zandbaktype benadrukte selecteur.](../images/ui/sandbox-type.png)

Nadat u het type hebt geselecteerd, geeft u een naam voor de sandbox op in het veld **[!UICONTROL Name]** . De naam van de sandbox is een id in kleine letters voor gebruik in API-aanroepen en moet daarom uniek en beknopt zijn. De naam van de sandbox moet beginnen met een letter, maximaal 256 tekens bevatten en mag alleen bestaan uit alfanumerieke tekens en afbreekstreepjes (-). Geef vervolgens een titel voor de sandbox op in het veld **[!UICONTROL Title]** . De titel moet leesbaar zijn en moet beschrijvend genoeg zijn om gemakkelijk te kunnen worden herkend.

Selecteer **[!UICONTROL Create]** als u klaar bent.

![ creeer zandbak dialoog met de Naam en Titled binnen en de Create benadrukte optie.](../images/ui/sandbox-info.png)

Nadat u de sandbox hebt gemaakt, vernieuwt u de pagina en verschijnt de nieuwe sandbox in het **[!UICONTROL Sandboxes]** -dashboard met de status &quot;[!UICONTROL Creating]&quot;. De nieuwe zandbakken nemen ongeveer 30 seconden in om door het systeem worden provisioned, waarna hun status in &quot;[!UICONTROL Active]&quot;verandert.

![ het zandbakendashboard met de onlangs gecreeerd benadrukte zandbak.](../images/ui/new-sandbox.png)

## Een sandbox opnieuw instellen

>[!WARNING]
>
>Hieronder volgt een lijst met uitzonderingen die kunnen voorkomen dat u de standaardproductiessandbox of een door de gebruiker gemaakte productiesandbox opnieuw instelt:
>
>* Een door de gebruiker gemaakte productiesandbox die wordt gebruikt voor bidirectioneel segmentdelen met Adobe Audience Manager of Audience Core Service kan na een waarschuwingsbericht worden hersteld.
>* Voordat u een sandbox-reset start, moet u de composities handmatig verwijderen om ervoor te zorgen dat de bijbehorende publieksgegevens op de juiste wijze worden opgeschoond.
>* De sandbox-id verandert nadat de reset is voltooid.
>* Voor [ Journey Optimizer B2B edition ](https://experienceleague.adobe.com/nl/docs/journey-optimizer-b2b/user/guide-overview), wordt het terugstellen van de zandbak momenteel niet gesteund **&#x200B;**. Als u een sandbox die is toegewezen aan Journey Optimizer B2B edition opnieuw instelt of verwijdert, kan dit leiden tot een permanent gegevensverlies in Journey Optimizer B2B edition en kan het nodig zijn een nieuwe Journey Optimizer B2B edition-instantie in te stellen.

### Advertentiecomposities verwijderen

De compositie van het publiek is momenteel niet geïntegreerd met de functie voor het opnieuw instellen van de sandbox, zodat het publiek handmatig moet worden verwijderd voordat de sandbox opnieuw wordt ingesteld.

Selecteer **[!UICONTROL Audiences]** in de sectie **[!UICONTROL Customers]** links in de navigatie en selecteer vervolgens de tab **[!UICONTROL Compositions]** .

![ het dashboard van het publiek met het geselecteerde en benadrukte lusje van Samenstellingen.](../images/ui/audiences.png)

Selecteer vervolgens de ellips (`...`) naast het eerste publiek en selecteer **[!UICONTROL Delete]** .

![ het publieksmenu dat de [!UICONTROL Delete] optie benadrukt.](../images/ui/delete-composition.png)

Er wordt een bevestiging van een geslaagde verwijdering weergegeven en u wordt teruggestuurd naar het tabblad **[!UICONTROL Compositions]** .

Herhaal bovenstaande stappen met al uw composities. Hiermee verwijdert u alle soorten publiek uit het overzicht van het publiek. Wanneer alle soorten publiek zijn verwijderd, kunt u de sandbox opnieuw instellen.

### Sandbox opnieuw instellen

Als u een productie- of ontwikkelingssandbox opnieuw instelt, worden alle bronnen verwijderd die aan die sandbox zijn gekoppeld (schema&#39;s, gegevenssets, enzovoort), terwijl de naam van de sandbox en de bijbehorende machtigingen behouden blijven. Deze &#39;schone&#39; sandbox blijft onder dezelfde naam beschikbaar voor gebruikers die er toegang toe hebben.

Selecteer de sandbox die u wilt herstellen in de lijst met sandboxen. Selecteer **[!UICONTROL Sandbox reset]** in het rechternavigatievenster dat wordt weergegeven.

![ het zandbakdashboard met de gekozen geselecteerde geselecteerde zandbak en Sandbox benadrukte het terugstellen optie.](../images/ui/reset.png)

Er verschijnt een dialoogvenster waarin u wordt gevraagd uw keuze te bevestigen. Selecteer **[!UICONTROL Continue]** om door te gaan.

![ het terugstellendialoog wordt getoond met de verdere benadrukte optie.](../images/ui/reset-warning.png)

Voer in het laatste bevestigingsvenster de naam van de sandbox in het dialoogvenster in en selecteer **[!UICONTROL Reset]** .

![ het terugstellendialoog met het bevestigingsnaamgebied en terugstellenoptie benadrukte.](../images/ui/reset-confirm.png)

## Een sandbox verwijderen

>[!WARNING]
>
>U kunt de standaardproductiesandbox niet verwijderen. Elke door de gebruiker gemaakte productiesandbox die wordt gebruikt voor bidirectioneel segmentdelen met [!DNL Audience Manager] of [!DNL Audience Core Service] , kan echter na een waarschuwingsbericht worden verwijderd.

Als u een productie- of ontwikkelingssandbox verwijdert, worden alle bronnen die aan die sandbox zijn gekoppeld, inclusief de machtigingen, permanent verwijderd.

Selecteer de sandbox die u wilt verwijderen uit de lijst met sandboxen. Selecteer **[!UICONTROL Delete]** in het rechternavigatievenster dat wordt weergegeven.

![ het zandbakdashboard met de gekozen geselecteerde zandbak en benadrukte optie van de Schrapping.](../images/ui/delete.png)

Er verschijnt een dialoogvenster waarin u wordt gevraagd uw keuze te bevestigen. Selecteer **[!UICONTROL Continue]** om door te gaan.

![ de schrappingsdialoog wordt getoond met de verdere benadrukte optie.](../images/ui/delete-warning.png)

Voer in het laatste bevestigingsvenster de naam van de sandbox in het dialoogvenster in en selecteer **[!UICONTROL Continue]** .

![ schrapt dialoog met het bevestigingsnaamgebied en blijft benadrukte optie.](../images/ui/delete-confirm.png)

## Volgende stappen

Dit document laat zien hoe u sandboxen beheert in de gebruikersinterface van Experience Platform. Nu u weet hoe te om zandbakken te beheren, leer hoe te om configuratienauwkeurigheid over zandbakken te verbeteren en naadloos zandbakconfiguraties tussen zandbakken met de [ zandbak tooling eigenschap](./sandbox-tooling.md) gids uit te voeren en in te voeren.

Voor informatie over hoe te om zandbakken te beheren gebruikend zandbak API, zie de [ gids van de zandbakontwikkelaar ](../api/getting-started.md).
