---
title: Ingesloten codes testen met Adobe Experience Platform Debugger
description: Leer hoe u met Platform Debugger verschillende insluitcodes voor Adobe Experience Platform op uw website lokaal kunt testen.
exl-id: ae6183b9-0d25-49d0-b0e9-f8b5ba58ab33
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 0%

---

# Insluitcodes testen met Adobe Experience Platform Debugger

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Gelieve te verwijzen naar het volgende [ document ](../../term-updates.md) voor een geconsolideerde verwijzing van de terminologieveranderingen.

Als u wijzigingen aanbrengt in uw tagbibliotheek die in Adobe Experience Platform is gemaakt, moet u deze wijzigingen testen voordat u de build implementeert in uw productieomgeving. Als u geen specifieke testomgeving of ontwikkelomgeving voor uw website hebt, kunt u Adobe Experience Platform Debugger gebruiken om verschillende insluitcodes in uw site lokaal te testen.

## Vereisten

Deze zelfstudie vereist een goed begrip van het gebruik van omgevingen en insluitcodes voor tags. Zie het [ milieu&#39;s overzicht ](./environments.md) voor meer informatie.

Deze zelfstudie vereist ook dat u de browserextensie van Foutopsporing voor platform hebt geïnstalleerd. Foutopsporing voor platform is beschikbaar voor de Chrome-browser. Gebruik de volgende koppeling om de extensie te installeren voordat u de zelfstudie start:

* [ Debugger van het Platform voor Chrome ](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob)

## Platformfoutopsporing openen op uw website

Navigeer met de browser van uw keuze naar uw website en open de extensie Platform Debugger. De site waarmee Platform Debugger momenteel is verbonden, wordt onder in het venster weergegeven. Als er momenteel tags op uw site worden uitgevoerd, wordt deze weergegeven op het tabblad [!UICONTROL Summary] .

![](./images/embed-code-testing/summary.png)

>[!NOTE]
>
>Als Platform Debugger aanvankelijk geen verbinding maakt, moet u mogelijk het browsertabblad dat uw website weergeeft opnieuw laden voordat u het opnieuw probeert.

## Insluitcodes vervangen

Nadat Platform Foutopsporing is verbonden met uw site, selecteert u **[!UICONTROL Launch]** in de linkernavigatie. Hier ziet u informatie over de bibliotheek die momenteel op uw site wordt uitgevoerd, inclusief de omgeving en bijbehorende extensies. Selecteer van hieruit **[!UICONTROL Configuration]** om besturingselementen voor het beheren van insluitcodes weer te geven.

![](./images/embed-code-testing/launch-tab.png)

Onder [!UICONTROL Page Embed Codes] wordt de insluitcode weergegeven die uw site momenteel gebruikt. Selecteer **[!UICONTROL Actions]** aan de rechterkant van de insluitcode en selecteer vervolgens **[!UICONTROL Replace]** .

![](./images/embed-code-testing/replace.png)

Er wordt een pop-up weergegeven waarin u wordt gevraagd een insluitcode op te geven om de huidige code te vervangen door. Merk op dat het vervangen van de insluitcode die Foutopsporing van het Platform gebruikt de opgestelde insluitcode op uw plaats niet verandert. In plaats daarvan vervangt deze alleen de insluitcode die lokaal wordt uitgevoerd, zodat u de implementatie kunt testen en fouten kunt opsporen.

Plak de insluitcode die u wilt testen in het opgegeven tekstvak en selecteer vervolgens **[!UICONTROL Apply]** .

![](./images/embed-code-testing/paste-code.png)

Het tabblad **[!UICONTROL Configuration]** wordt weer weergegeven, zodat u kunt zien dat de actieve insluitcode is vervangen door de code die u hebt opgegeven. U kunt nu de webbrowser gebruiken om te controleren of de insluitcode die u test, naar behoren werkt.

![](./images/embed-code-testing/code-replaced.png)

## Volgende stappen

Deze zelfstudie besprak hoe u lokaal kunt schakelen tussen insluitcodes voor testdoeleinden met behulp van Platform Debugger. Verwijs naar de [ Debugger van het Platform documentatie ](../../../debugger/home.md) voor meer informatie over zijn diverse mogelijkheden.
