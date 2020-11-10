---
keywords: Experience Platform;home;popular topics;sandbox user guide;sandbox guide
solution: Experience Platform
title: Gebruikershandleiding voor sandbox
topic: user guide
description: Dit document bevat stappen voor het uitvoeren van verschillende bewerkingen met betrekking tot sandboxen in de Adobe Experience Platform-gebruikersinterface.
translation-type: tm+mt
source-git-commit: 2d1a9699866bd39de7251731e9f0cd2f753a5083
workflow-type: tm+mt
source-wordcount: '623'
ht-degree: 0%

---


# Gebruikershandleiding voor sandbox

Dit document bevat stappen voor het uitvoeren van verschillende bewerkingen met betrekking tot sandboxen in de Adobe Experience Platform-gebruikersinterface.

## Sandboxen weergeven

Selecteer in de interface van het Experience Platform de optie **[!UICONTROL Sandboxen]** in de linkernavigatie om het dashboard **[!UICONTROL Sandboxen]** te openen. Het dashboard bevat alle beschikbare sandboxen voor uw organisatie, inclusief het type sandbox (productie of ontwikkeling) en de status (actief, maken, verwijderen of mislukt).

![](../images/ui/view-sandboxes.png)

## Schakelen tussen sandboxen

Met het besturingselement voor de **sandbox-schakeloptie** linksboven in het scherm wordt de momenteel actieve sandbox weergegeven.

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

Als u een nieuwe sandbox wilt maken in de gebruikersinterface, selecteert u de knop Sandbox **** maken rechtsboven in het scherm.

![](../images/ui/create-sandbox.png)

Het dialoogvenster Sandbox **** maken wordt weergegeven en u wordt gevraagd een weergavetoetitel en naam voor de sandbox op te geven. De **weergavetitel** moet leesbaar zijn en moet beschrijvend genoeg zijn om gemakkelijk te kunnen worden herkend. De **[!UICONTROL naam]** van de sandbox is een id in kleine letters voor gebruik in API-aanroepen en moet daarom uniek en beknopt zijn. De **[!UICONTROL naam]** van de sandbox mag alleen bestaan uit alfanumerieke tekens en afbreekstreepjes **(-)**. De naam moet beginnen met een letter en mag maximaal 256 tekens bevatten.

Als u klaar bent, selecteert u **[!UICONTROL Maken]**.

![](../images/ui/create-dialog.png)

>[!NOTE]
>
>Aangezien u beperkt bent tot het maken van alleen niet-productie-sandboxtypen, is de optie **[!UICONTROL type]** vergrendeld bij Niet-productie en kan deze optie niet worden gemanipuleerd.

Nadat u de sandbox hebt gemaakt, vernieuwt u de pagina en verschijnt de nieuwe sandbox in het dashboard **[!UICONTROL Sandboxen]** met de status &quot;[!UICONTROL Creating]&quot;. Nieuwe sandboxen nemen ongeveer 15 minuten in beslag om door het systeem te worden ingericht, waarna de status van deze sandboxen verandert in[!UICONTROL Actief].

![](../images/ui/creating.png)

## Een sandbox opnieuw instellen

>[!NOTE]
>
>Deze functionaliteit is alleen beschikbaar voor niet-productiesandboxen. Productiesandboxen kunnen niet opnieuw worden ingesteld.

Als u een niet-productiesandbox opnieuw instelt, worden alle bronnen verwijderd die aan die sandbox zijn gekoppeld (schema&#39;s, gegevenssets, enzovoort), terwijl de naam van de sandbox en de bijbehorende machtigingen behouden blijven. Deze &#39;schone&#39; sandbox blijft onder dezelfde naam beschikbaar voor gebruikers die er toegang toe hebben.

Als u een sandbox in de UI opnieuw wilt instellen, selecteert u **[!UICONTROL Sandboxen]** in de linkernav en selecteert u vervolgens de sandbox die u opnieuw wilt instellen. Selecteer Sandbox **[!UICONTROL opnieuw instellen in het dialoogvenster dat aan de rechterkant van het scherm wordt weergegeven]**.

![](../images/ui/reset-sandbox.png)

Er verschijnt een dialoogvenster waarin u wordt gevraagd uw keuze te bevestigen. Selecteer **[!UICONTROL Herstellen]** om door te gaan.

![](../images/ui/reset-confirm.png)

Er wordt een bevestigingsbericht weergegeven en de status van de sandbox verandert in &quot;**[!UICONTROL Opnieuw instellen]&quot;**. Zodra het door het systeem is voorzien, zal zijn staat aan **&quot;[!UICONTROL Actief]&quot;** of **&quot;[!UICONTROL Mislukt]&quot;** bijwerken.

![](../images/ui/resetting.png)

## Een sandbox verwijderen

>[!NOTE]
>
>Deze functionaliteit is alleen beschikbaar voor niet-productiesandboxen. Productiesandboxen kunnen niet worden verwijderd.

Als u een niet-productiesandbox verwijdert, worden alle bronnen die aan die sandbox zijn gekoppeld, inclusief de machtigingen, permanent verwijderd.

Als u een sandbox in de UI wilt verwijderen, selecteert u **[!UICONTROL Sandboxen]** in de linkernav en selecteert u vervolgens de sandbox die u wilt verwijderen. Selecteer Sandbox **[!UICONTROL verwijderen in het dialoogvenster dat rechts op het scherm wordt weergegeven]**.

![](../images/ui/delete-sandbox.png)

Er verschijnt een dialoogvenster waarin u wordt gevraagd uw keuze te bevestigen. Selecteer **[!UICONTROL Verwijderen]** om door te gaan.

![](../images/ui/delete-confirm.png)

Er wordt een bevestigingsbericht weergegeven en de sandbox wordt verwijderd uit de **[!UICONTROL sandboxwerkruimte]** .

## Volgende stappen

Dit document laat zien hoe u sandboxen beheert in de gebruikersinterface van het Experience Platform. Zie de handleiding voor [sandboxontwikkelaars voor informatie over het beheren van sandboxen met de sandbox-API](../api/getting-started.md).