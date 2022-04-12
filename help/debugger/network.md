---
title: Het Lusje van het Netwerk
description: Leer hoe u het tabblad Netwerk in Adobe Experience Platform Debugger gebruikt.
keywords: foutopsporing;ervaring met Platform debugger-extensie;chroom;extensie;netwerk;informatie
seo-description: Experience Platform Debugger Network screen
seo-title: Network Tab
uuid: 839686c9-6e4f-4661-acf6-150ea24dc47f
exl-id: ed0579ef-ec26-43df-9453-a395c105038a
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# Het tabblad Netwerk

De **Netwerk** worden alle Adobe Experience Cloud-oplossingsaanroepen op de pagina samengevoegd en in volgorde van links naar rechts weergegeven. Standaardparameters worden automatisch geëtiketteerd met vriendelijke namen en gerangschikt om gemeenschappelijke parameters op dezelfde rol te groeperen.

![](images/network.jpg)

Dit scherm is nuttig om zeer belangrijke waardeparen over klappen te vergelijken. U kunt bevestigen dat de parameters die voor integratie worden gebruikt, zoals identiteitskaart van de Bezoeker van de Experience Cloud of Supplementale identiteitskaart van Gegevens, over integratie verenigbaar zijn.

>[!NOTE]
>
>Op dit ogenblik, zijn niet alle parameters die in de oplossingsvraag worden overgegaan (bijvoorbeeld, de contextvariabelen van Analytics, de douaneparameters van het Doel, of de Klant IDs van de Dienst van Experience Cloud ID) zichtbaar in het scherm van het Netwerk.

Om de informatie door oplossing te veranderen, selecteer de oplossing u van de lijst in linkernav wilt bekijken. In het volgende voorbeeld wordt alleen Analytics weergegeven:

![](images/network-analytics.jpg)

Als u wilt terugkeren naar het weergeven van alle oplossingen, selecteert u **[!UICONTROL Network]**

Selecteer op een punt in de mening van het Netwerk om een uitgebreide mening te zien. Vanuit het uitgevouwen weergavevenster kunt u de weergegeven informatie naar het klembord kopiëren.

![](images/network-expand.jpg)

<!--Use the icon at the top of each column to copy the server call URL to your clipboard, where you can paste it into another document for reference or debugging purposes.

![](images/copy.jpg)-->

Als u de lijst wilt wissen, selecteert u **[!UICONTROL Remove Events]**.

Als u een Excel-bestand met de informatie op dit scherm wilt downloaden, selecteert u **[!UICONTROL Download]**.
