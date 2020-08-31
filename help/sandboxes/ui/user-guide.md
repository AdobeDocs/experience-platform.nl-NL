---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Gebruikershandleiding voor sandbox
topic: user guide
translation-type: tm+mt
source-git-commit: c8446f6040ac9ef1f4196d9057b531011e243258
workflow-type: tm+mt
source-wordcount: '530'
ht-degree: 0%

---


# Gebruikershandleiding voor sandbox

Dit document bevat stappen voor het uitvoeren van verschillende bewerkingen met betrekking tot sandboxen in de Adobe Experience Platform-gebruikersinterface.

## Sandboxen weergeven

Klik in de interface van het Experience Platform op **[!UICONTROL Sandboxen]** in de linkernavigatie om het dashboard _[!UICONTROL Sandboxen]_ te openen. Het dashboard bevat alle beschikbare sandboxen voor uw organisatie, inclusief het type sandbox (productie of ontwikkeling) en de status (actief, maken, verwijderen of mislukt).

![](../images/ui/sandboxes-tab.png)

## Schakelen tussen sandboxen

Met het besturingselement voor de **sandbox-schakeloptie** linksboven in het scherm wordt de momenteel actieve sandbox weergegeven.

![](../images/ui/sandbox-selector.png)

Als u wilt schakelen tussen sandboxen, klikt u op de sandboxswitch en selecteert u de gewenste sandbox in de vervolgkeuzelijst.

![](../images/ui/switch-sandbox.png)

Als een sandbox is geselecteerd, wordt het scherm vernieuwd met de geselecteerde sandbox die nu is opgenomen in de sandbox-schakeloptie.

![](../images/ui/sandbox-switched.png)

## Een nieuwe sandbox maken

Gebruik de volgende video voor een snel overzicht van het gebruik van sandboxen in Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/29838/?quality=12&learn=on)

Als u een nieuwe sandbox wilt maken in de gebruikersinterface, klikt u op **[!UICONTROL Sandboxen]** in de linkernav en klikt u op Sandbox **** maken.

![](../images/ui/create-sandbox-button.png)

Het dialoogvenster Sandbox __ maken wordt weergegeven en u wordt gevraagd een weergavetoetitel en naam voor de sandbox op te geven. De **weergavetitel** moet leesbaar zijn en moet beschrijvend genoeg zijn om gemakkelijk te kunnen worden herkend. De **[!UICONTROL naam]** van de sandbox is een id in kleine letters voor gebruik in API-aanroepen en moet daarom uniek en beknopt zijn.

When finished, click **[!UICONTROL Create]**.

![](../images/ui/create-sandbox-dialog.png)

>[!NOTE]
>
>Aangezien u beperkt bent tot het maken van alleen niet-productie-sandboxtypen, is de optie **[!UICONTROL type]** vergrendeld bij Niet-productie en kan deze optie niet worden gemanipuleerd.

Nadat u de sandbox hebt gemaakt, vernieuwt u de pagina en verschijnt de nieuwe sandbox in het dashboard _[!UICONTROL Sandboxen]_ met de status &quot;[!UICONTROL Creating]&quot;. Nieuwe sandboxen nemen ongeveer 15 minuten in beslag om door het systeem te worden ingericht, waarna de status van deze sandboxen verandert in[!UICONTROL Actief].

![](../images/ui/sandbox-created.png)

## Een sandbox opnieuw instellen

>[!NOTE]
>
>Deze functionaliteit is alleen beschikbaar voor niet-productiesandboxen. Productiesandboxen kunnen niet opnieuw worden ingesteld.

Als u een niet-productiesandbox opnieuw instelt, worden alle bronnen verwijderd die aan die sandbox zijn gekoppeld (schema&#39;s, gegevenssets, enzovoort), terwijl de naam van de sandbox en de bijbehorende machtigingen behouden blijven. Deze &#39;schone&#39; sandbox blijft onder dezelfde naam beschikbaar voor gebruikers die er toegang toe hebben.

Als u een sandbox in de UI opnieuw wilt instellen, klikt u op **[!UICONTROL Sandboxen]** in de linkernav en vervolgens op de sandbox die u opnieuw wilt instellen. Klik in het dialoogvenster dat aan de rechterkant van het scherm wordt weergegeven op Sandbox **** opnieuw instellen.

![](../images/ui/reset-sandbox-button.png)

Er verschijnt een dialoogvenster waarin u wordt gevraagd uw keuze te bevestigen. Klik op **[!UICONTROL Herstellen]** om door te gaan.

<img src="../images/ui/reset-are-you-sure.png" width="350"><br>

Er wordt een bevestigingsbericht weergegeven en de status van de sandbox verandert in &quot;[!UICONTROL Opnieuw instellen]&quot;. Zodra het door het systeem is provisioned, zal zijn staat aan &quot;[!UICONTROL Actief]&quot;of &quot;[!UICONTROL Mislukt]&quot;bijwerken.

![](../images/ui/sandbox-resetting.png)

## Een sandbox verwijderen

>[!NOTE]
>
>Deze functionaliteit is alleen beschikbaar voor niet-productiesandboxen. Productiesandboxen kunnen niet worden verwijderd.

Als u een niet-productiesandbox verwijdert, worden alle bronnen die aan die sandbox zijn gekoppeld, inclusief de machtigingen, permanent verwijderd.

Als u een sandbox in de UI wilt verwijderen, klikt u op **[!UICONTROL Sandboxen]** in de linkernav en vervolgens op de sandbox die u wilt verwijderen. Klik in het dialoogvenster dat aan de rechterkant van het scherm wordt weergegeven op Sandbox **** verwijderen.

![](../images/ui/delete-sandbox-button.png)

Er verschijnt een dialoogvenster waarin u wordt gevraagd uw keuze te bevestigen. Klik op **[!UICONTROL Verwijderen]** om door te gaan.

<img src="../images/ui/delete-are-you-sure.png" width="350"><br>

Er wordt een bevestigingsbericht weergegeven en de sandbox wordt verwijderd uit de _[!UICONTROL sandboxwerkruimte]_ .

## Volgende stappen

Dit document laat zien hoe u sandboxen beheert in de gebruikersinterface van het Experience Platform. Zie de handleiding voor [sandboxontwikkelaars voor informatie over het beheren van sandboxen met de sandbox-API](../api/getting-started.md).