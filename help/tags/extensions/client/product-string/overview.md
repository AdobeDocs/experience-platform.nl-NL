---
title: Overzicht van extensie Adobe Analytics-producttekenreeks
description: Meer informatie over de extensie van de Adobe Analytics Product String-tag in Adobe Experience Platform.
exl-id: a49feb4e-f166-41d2-9f85-639f6ff8bb8f
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# Overzicht van de extensie Adobe Analytics Product String

>[!NOTE]
>
>Adobe Experience Platform Launch is omgedoopt tot een reeks technologieën voor gegevensverzameling in Adobe Experience Platform. Diverse terminologische wijzigingen zijn als gevolg hiervan in de productdocumentatie doorgevoerd. Raadpleeg het volgende [document](../../../term-updates.md) voor een geconsolideerde referentie van de terminologische wijzigingen.

De `products` Met variabele wordt bijgehouden hoe gebruikers werken met producten op uw site. De `products` met deze variabele kunt u bijhouden hoe vaak een product wordt weergegeven, aan het winkelwagentje wordt toegevoegd, uitgecheckt en aangeschaft. U kunt ook de relatieve effectiviteit van de handelscategorieën op uw site volgen.

De `products` variabele moet altijd samen met een succesgebeurtenis worden ingesteld.

De [!DNL Adobe Analytics Product String Builder] extensie stelt automatisch de `products` variabele door uw gegevenslaag te herhalen, alle noodzakelijke productgerelateerde gegevens op te nemen, en het te formatteren in de juiste hieronder getoonde syntaxis. U hoeft geen aangepaste JavaScript meer te schrijven en te onderhouden om deze complexe handelingen uit te voeren.

## Syntaxis van de productvariabele

```bash
Category;Product;Quantity;Price;eventN=X|eventN2=X2;eVarN=merch_category|eVarN2=merch_category2
```

Voor volledige documentatie gaat u naar [Producten](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html).

## Extensieinstructies

### Configuratie van handelingen

Voeg de actie &quot;Adobe Analytics Product String - Set s.products&quot; toe aan uw regel.

![Actieconfiguratie](./images/screenshot-action-config.png)

### Standaardproductgegevens instellen

Definieer vervolgens de gegevenslaagvariabelen. Nadat u de handeling hebt geconfigureerd zoals beschreven in de vorige stap, wordt het volgende scherm weergegeven:

![Standaardvelden](./images/screenshot-standard-fields.png)

Voor elk van de gegevenspunten u in het productkoord wilt omvatten, ga de weg aan de aangewezen variabele van de gegevenslaag in.

Als uw gegevenslaag bijvoorbeeld als volgt is gestructureerd:

```json
digitalData = {
  "transaction": {
    "item": [{
      "productInfo": {
        "productName": "My Product"
      }
    }]
  }
};
```

U zou het volgende pad invoeren in het veld &quot;Variabele voor product-id/naam&quot; om het volgende vast te leggen `productName` variabele:

```json
digitalData.transaction.item.productInfo.productName
```

>[!NOTE]
>
>Als u een gegevenselement gebruikt om het gebied te bevolken, zou het moeten worden gevormd gebruikend het het gegevenstype van de Code van de Constante of van de Douane en moet de weg hierboven als koord letterlijk terugkeren.

### Prijssoort

De `price` in de [!DNL Adobe Analytics] de productreeks moet de totale prijs voor het aantal gekochte eenheden, niet de eenheidsprijs, voor dat product weerspiegelen. Wanneer u het veld Prijs inschakelt in de extensiehandeling, moet u opgeven of de gegevenslaag de totale prijs of de eenheidsprijs blootstelt. Bij gebruik van de eenheidsprijs [!DNL Adobe Analytics Product String] de extensie vermenigvuldigt automatisch de eenheidsprijs met de hoeveelheid om de totale prijs op te halen en de productreeks correct in te stellen .

![Prijssoort](./images/screenshot-price-type.png)

### Aangepaste gebeurtenissen en wijzigingen in handelsversies

![Gebeurtenissen en gebeurtenissen](./images/screenshot-events-evars.png)

Voer de volgende stappen uit als uw implementatie aangepaste gebeurtenissen gebruikt of eVars verkoopt:

1. Gekoppelde selecteren **[!UICONTROL Add]** knop.
1. Kies in het vervolgkeuzemenu de gebeurtenis die of de eVar die u wilt instellen.
1. Voer het pad naar de desbetreffende variabele voor de gegevenslaag in met dezelfde syntaxis als hierboven beschreven.

### Handelingenreeks

Deze actie moet vergezeld gaan van een actie &quot;Adobe Analytics - Set Variables&quot; die de corresponderende succesgebeurtenissen instelt, en van een actie &quot;Adobe Analytics - Send Beacon&quot;. De juiste volgorde van handelingen wordt hieronder weergegeven.

![Standaardvelden](./images/screenshot-price-type.png)

### Vereisten

* Op een object gebaseerd [gegevenslaag](https://theblog.adobe.com/data-layers-buzzword-best-practice/) met variabelen voor alle productgerelateerde gegevens (zoals product-id, hoeveelheid, prijs). Deze extensie werkt niet met op arrays gebaseerde gegevenslagen.
* De [Adobe Analytics](../analytics/overview.md) extensie moet zijn geïnstalleerd.
