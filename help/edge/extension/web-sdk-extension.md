---
title: Overzicht van Adobe Experience Platform Web SDK-extensie
description: Meer informatie over de Adobe Experience Platform Web SDK Extension voor Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 0b9a92f006d1ec151a0bb11c10c607ea9362f729
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---


# Overzicht van Adobe Experience Platform Web SDK-extensie

De extensie Adobe Experience Platform Web SDK verzendt gegevens naar de Adobe Experience Cloud vanuit wegeigenschappen via het Adobe Experience Platform Edge Network. Met de Adobe Experience Platform Web SDK-extensie kunt u gegevens streamen naar een platform, identiteiten synchroniseren, inbellen en automatisch contextgegevens verzamelen.

## De extensie configureren

Deze sectie bevat een verwijzing naar de beschikbare opties bij het configureren van de extensie Adobe Experience Platform Web SDK.

Als de extensie Adobe Experience Platform Web SDK nog niet is geïnstalleerd, opent u de eigenschap en selecteert u **[!UICONTROL Extensies > Catalog]**, plaatst u de aanwijzer op de SDK-extensie Adobe Experience Platform Web en selecteert u **[!UICONTROL Installeren]**.

Als u de extensie wilt configureren, opent u het tabblad **[!UICONTROL Extensies]**, plaatst u de muis boven de extensie en selecteert u **[!UICONTROL Configureren]**.

![](./assets/ext-aep-config.png)

### Instantienaam

De extensie Adobe Experience Platform Web SDK ondersteunt meerdere exemplaren op de pagina. Dit wordt gebruikt om gegevens naar veelvoudige organisaties met één enkele configuratie van Adobe Experience Platform Launch te verzenden. De **[!UICONTROL Naam]** is standaard gelegeerd. U kunt de instantienaam echter wijzigen in elke geldige naam voor een JavaScript-object. De extensie Adobe Experience Platform vereist dat elke instantie een andere **[!UICONTROL Config ID]** en een andere **[!UICONTROL Organisatie-id]** heeft.

## **[!UICONTROL Configuratie-id]**

De **[!UICONTROL Configuratie-id]** geeft Adobe Experience Platform aan waar de gegevens moeten worden gerouteerd en welke configuraties op de server moeten worden gebruikt. Dit is vereist voor de Adobe Experience Platform-extensie. U kunt een configuratie-id verkrijgen door contact op te nemen met de klantenservice.


### **[!UICONTROL Organisatie-id]**

De **[!UICONTROL Organisatie-id]** is de organisatie waarnaar u de gegevens op Adobe wilt verzenden. Meestal moet u de standaardwaarde gebruiken die automatisch wordt ingevuld. Wanneer u meerdere exemplaren op de pagina hebt, vult u deze met de waarde van de tweede organisatie waarnaar u gegevens wilt verzenden.

### **[!UICONTROL Edge-domein]**

Het **[!UICONTROL Edge-domein]** is het domein waarvan de Adobe Experience Platform-extensie gegevens verzendt en ontvangt. De uitbreiding vereist dat u 1st-partij CNAME voor productieverkeer gebruikt. Het standaard domein van derden werkt voor ontwikkelomgevingen, maar is niet geschikt voor productieomgevingen. Instructies over hoe te opstelling een eerste-partij CNAME zijn vermeld [hier](https://docs.adobe.com/content/help/en/core-services/interface/ec-cookies/cookies-first-party.html).

### **[!UICONTROL Fouten inschakelen]**

Als er een fout met de extensie optreedt, wordt de fout standaard geregistreerd bij de console. Als u de fouten in een productieomgeving wilt verbergen, kunt u het selectievakje **[!UICONTROL Fouten inschakelen]** uitschakelen. Fouten worden nog steeds afgedrukt wanneer foutopsporing is ingeschakeld in Platform launch.

### **[!UICONTROL Inschakelen inschakelen]**

Als **[!UICONTROL Opt-in inschakelen]** is ingeschakeld, kan de extensie hits bevatten totdat de optie opt-in is ontvangen. De extensie stelt een handeling beschikbaar waarmee de voorkeuren voor aanmelding worden ingesteld.

### **[!UICONTROL ECID migreren inschakelen]**

De uitbreiding van SDK van het Web van het Platform gebruikt een nieuw koekje om ECID op te slaan. Deze instelling maakt compatibiliteit tussen de nieuwe cookie en de oude cookie voor migratiedoeleinden mogelijk. Adobe raadt u ten zeerste aan deze optie in te schakelen, tenzij u geen bestaande bezoekers met een ECID hebt.

### **[!UICONTROL Cookies van derden gebruiken]**

De Adobe Experience Platform slaat altijd een cookie op in het domein van de eerste partij. Met deze optie kunt u een cookie van een andere fabrikant gebruiken die is ingesteld op demdex.net, naast de cookie in het domein van de eerste fabrikant. Dit kan handig zijn als u gebruikers hebt die tussen meerdere domeinen bewegen. Dit zal vraag aan demdex.net onbruikbaar maken.

### **[!UICONTROL Context]**

De extensie verzamelt automatisch informatie over de context van de aanvraag (bijvoorbeeld informatie over de URL en de browser). Dit kan worden uitgeschakeld door specifieke contexten uit te schakelen.

- **[!UICONTROL web]** : details over de webpagina, zoals de URL, de referentie, enz.
- **[!UICONTROL apparaat]**  - Gegevens over het apparaat, zoals de schermstand, schermhoogte en schermbreedte.
- **[!UICONTROL omgeving]**  - Informatie over de computeromgeving (browser, verbinding, enzovoort)
- **[!UICONTROL locatie]**  - Beperkte informatie over de locatie van de gebruiker

## Wat nu

1. Stel [actietypen](action-types.md) in.
2. Stel [gegevenselemetypen](data-element-types.md) in.
