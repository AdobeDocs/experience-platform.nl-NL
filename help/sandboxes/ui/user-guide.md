---
keywords: Experience Platform;home;populaire onderwerpen;sandbox-gebruikershandleiding;sandbox-hulplijn
solution: Experience Platform
title: Gebruiksaanwijzing voor sandbox
topic: gebruikershandleiding
description: Dit document bevat stappen voor het uitvoeren van verschillende bewerkingen met betrekking tot sandboxen in de Adobe Experience Platform-gebruikersinterface.
translation-type: tm+mt
source-git-commit: 62ce5ac92d03a6e85589fc92e8d953f7fc1d8f31
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---


# Gebruiksaanwijzing voor sandbox

Dit document bevat stappen voor het uitvoeren van verschillende bewerkingen met betrekking tot sandboxen in de Adobe Experience Platform-gebruikersinterface.

## Sandboxen weergeven

Selecteer **[!UICONTROL Sandboxes]** in de gebruikersinterface van het Experience Platform in de linkernavigatie om het dashboard **[!UICONTROL Sandboxes]** te openen. Het dashboard bevat alle beschikbare sandboxen voor uw organisatie, inclusief het type sandbox (productie of ontwikkeling) en de status (actief, maken, verwijderen of mislukt).

![](../images/ui/view-sandboxes.png)

## Schakelen tussen sandboxen

Met het besturingselement **sandboxswitch** linksboven in het scherm wordt de momenteel actieve sandbox weergegeven.

![](../images/ui/sandbox-switcher.png)

Als u wilt schakelen tussen sandboxen, selecteert u de sandboxschakelaar en selecteert u de gewenste sandbox in de vervolgkeuzelijst.

![](../images/ui/switcher-menu.png)

Als een sandbox is geselecteerd, wordt het scherm vernieuwd met de geselecteerde sandbox die nu is opgenomen in de sandbox-schakeloptie.

![](../images/ui/switched.png)

## Zoeken naar een sandbox

U kunt door de lijst van zandbakken navigeren beschikbaar aan u door de onderzoeksfunctie van het menu van de zandbakschakelaar te gebruiken. Typ de naam van de sandbox die u wilt gebruiken om te filteren via alle sandboxen die voor uw organisatie beschikbaar zijn.

![](../images/ui/sandbox-search.png)

## Een nieuwe sandbox maken

Gebruik de volgende video voor een snel overzicht van het gebruik van sandboxen in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Als u een nieuwe sandbox in de UI wilt maken, selecteert u de knop **[!UICONTROL Create Sandbox]** rechtsboven in het scherm.

![](../images/ui/create-sandbox.png)

Het dialoogvenster **[!UICONTROL Create Sandbox]** wordt weergegeven en u wordt gevraagd een weergavetoetitel en naam voor de sandbox op te geven. De **weergavetitel** moet leesbaar zijn en moet beschrijvend genoeg zijn om gemakkelijk te kunnen worden herkend. De sandbox **[!UICONTROL Name]** is een id in kleine letters voor gebruik in API-aanroepen en moet daarom uniek en beknopt zijn. De sandbox **[!UICONTROL Name]** mag alleen bestaan uit alfanumerieke tekens en afbreekstreepjes **(-)**, moet beginnen met een letter en mag niet langer zijn dan 256 tekens.

Selecteer **[!UICONTROL Create]** als u klaar bent.

![](../images/ui/create-dialog.png)

>[!NOTE]
>
>Aangezien u beperkt bent tot het maken van alleen niet-productie sandboxtypen, is de optie **[!UICONTROL type]** vergrendeld bij &quot;Niet-productie&quot; en kan deze niet worden gemanipuleerd.

Nadat u de sandbox hebt gemaakt, vernieuwt u de pagina en verschijnt de nieuwe sandbox in het dashboard **[!UICONTROL Sandboxes]** met de status &quot;[!UICONTROL Creating]&quot;. Nieuwe sandboxen nemen ongeveer 15 minuten in beslag om door het systeem te worden ingericht, waarna de status van deze sandboxen verandert in &quot;[!UICONTROL Active]&quot;.

![](../images/ui/creating.png)

## Een sandbox opnieuw instellen

>[!NOTE]
>
>Deze functionaliteit is alleen beschikbaar voor niet-productiesandboxen. Productiesandboxen kunnen niet opnieuw worden ingesteld.

Als u een niet-productiesandbox opnieuw instelt, worden alle bronnen verwijderd die aan die sandbox zijn gekoppeld (schema&#39;s, gegevenssets, enzovoort), terwijl de naam van de sandbox en de bijbehorende machtigingen behouden blijven. Deze &#39;schone&#39; sandbox blijft onder dezelfde naam beschikbaar voor gebruikers die er toegang toe hebben.

Als u een sandbox in de UI opnieuw wilt instellen, selecteert u **[!UICONTROL Sandboxes]** in de linkernav en selecteert u vervolgens de sandbox die u opnieuw wilt instellen. Selecteer **[!UICONTROL Reset Sandbox]** in het dialoogvenster dat rechts op het scherm wordt weergegeven.

![](../images/ui/reset-sandbox.png)

Er verschijnt een dialoogvenster waarin u wordt gevraagd uw keuze te bevestigen. Selecteer **[!UICONTROL Reset]** om door te gaan.

![](../images/ui/reset-confirm.png)

Er wordt een bevestigingsbericht weergegeven en de status van de sandbox verandert in &quot;**[!UICONTROL Resetting]&quot;**. Zodra het door het systeem is voorzien, zal zijn staat aan **&quot;[!UICONTROL Active]&quot;** of **&quot;[!UICONTROL Failed]&quot;** bijwerken.

![](../images/ui/resetting.png)

## Een sandbox verwijderen

>[!NOTE]
>
>Deze functionaliteit is alleen beschikbaar voor niet-productiesandboxen. Productiesandboxen kunnen niet worden verwijderd.

Als u een niet-productiesandbox verwijdert, worden alle bronnen die aan die sandbox zijn gekoppeld, inclusief de machtigingen, permanent verwijderd.

Als u een sandbox in de UI wilt verwijderen, selecteert u **[!UICONTROL Sandboxes]** in de linkernav en selecteert u vervolgens de sandbox die u wilt verwijderen. Selecteer **[!UICONTROL Delete Sandbox]** in het dialoogvenster dat rechts op het scherm wordt weergegeven.

![](../images/ui/delete-sandbox.png)

Er verschijnt een dialoogvenster waarin u wordt gevraagd uw keuze te bevestigen. Selecteer **[!UICONTROL Delete]** om door te gaan.

![](../images/ui/delete-confirm.png)

Er wordt een bevestigingsbericht weergegeven en de sandbox wordt verwijderd uit de werkruimte **[!UICONTROL Sandboxes]**.

## Volgende stappen

Dit document laat zien hoe u sandboxen beheert in de gebruikersinterface van het Experience Platform. Zie de [handleiding voor sandboxontwikkelaars](../api/getting-started.md) voor informatie over het beheren van sandboxen met de sandbox-API.