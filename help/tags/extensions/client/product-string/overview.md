---
title: Overzicht van extensie Adobe Analytics-producttekenreeks
description: Meer informatie over de extensie van de Adobe Analytics Product String-tag in Adobe Experience Platform.
exl-id: a49feb4e-f166-41d2-9f85-639f6ff8bb8f
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '470'
ht-degree: 0%

---

# Overzicht van de extensie Adobe Analytics Product String

De variabele `products` houdt bij hoe gebruikers met producten op uw site werken. Met de variabele `products` kunt u bijvoorbeeld bijhouden hoe vaak een product wordt weergegeven, aan het winkelwagentje worden toegevoegd, uitgecheckt en aangeschaft. U kunt ook de relatieve effectiviteit van de handelscategorieën op uw site volgen.

De variabele `products` moet altijd worden ingesteld in combinatie met een succesgebeurtenis.

De extensie [!DNL Adobe Analytics Product String Builder] stelt de variabele `products` automatisch in door de gegevenslaag te doorlopen, alle benodigde productgerelateerde gegevens op te halen en deze op te maken in de hieronder weergegeven juiste syntaxis. U hoeft geen aangepaste JavaScript meer te schrijven en te onderhouden om deze complexe handelingen uit te voeren.

## Syntaxis van de productvariabele

```bash
Category;Product;Quantity;Price;eventN=X|eventN2=X2;eVarN=merch_category|eVarN2=merch_category2
```

Voor volledige documentatie, bezoek [&#x200B; Producten &#x200B;](https://experienceleague.adobe.com/docs/analytics/implementation/vars/page-vars/products.html).

## Extensieinstructies

### Configuratie van handelingen

Voeg de actie &quot;Adobe Analytics Product String - Set s.products&quot; toe aan uw regel.

![&#x200B; configuratie van de Actie &#x200B;](./images/screenshot-action-config.png)

### Standaardproductgegevens instellen

Definieer vervolgens de gegevenslaagvariabelen. Nadat u de handeling hebt geconfigureerd zoals beschreven in de vorige stap, wordt het volgende scherm weergegeven:

![&#x200B; Standaardgebieden &#x200B;](./images/screenshot-standard-fields.png)

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

U voert het volgende pad in het veld &quot;Variabele voor product-id/naam&quot; in om de variabele `productName` vast te leggen:

```json
digitalData.transaction.item.productInfo.productName
```

>[!NOTE]
>
>Als u een gegevenselement gebruikt om het gebied te bevolken, zou het moeten worden gevormd gebruikend het het gegevenstype van de Code van de Constante of van de Douane en moet de weg hierboven als koord letterlijk terugkeren.

### Prijssoort

De parameter `price` in de [!DNL Adobe Analytics] -productreeks moet de totale prijs weergeven voor het aantal eenheden dat is aangeschaft, niet de eenheidsprijs voor dat product. Wanneer u het veld Prijs inschakelt in de extensiehandeling, moet u opgeven of de gegevenslaag de totale prijs of de eenheidsprijs blootstelt. Wanneer u de eenheidsprijs gebruikt, vermenigvuldigt de extensie [!DNL Adobe Analytics Product String] automatisch de eenheidsprijs met de hoeveelheid om de totale prijs op te halen en de productreeks correct in te stellen.

![&#x200B; Type van Prijs &#x200B;](./images/screenshot-price-type.png)

### Aangepaste gebeurtenissen en wijzigingen in handelsversies

![&#x200B; Gebeurtenissen en eVars &#x200B;](./images/screenshot-events-evars.png)

Voer de volgende stappen uit als uw implementatie aangepaste gebeurtenissen gebruikt of eVars verkoopt:

1. Selecteer de bijbehorende knop **[!UICONTROL Add]** .
1. Kies in het vervolgkeuzemenu de gebeurtenis of eVar die u wilt instellen.
1. Voer het pad naar de desbetreffende variabele voor de gegevenslaag in met dezelfde syntaxis als hierboven beschreven.

### Handelingenreeks

Deze actie moet vergezeld gaan van een actie &quot;Adobe Analytics - Set Variables&quot; die de corresponderende succesgebeurtenissen instelt, en van een actie &quot;Adobe Analytics - Send Beacon&quot;. De juiste volgorde van handelingen wordt hieronder weergegeven.

![&#x200B; Standaardgebieden &#x200B;](./images/screenshot-action-type.png)

### Vereisten

* Een op voorwerp-gebaseerde [&#x200B; gegevenslaag &#x200B;](https://theblog.adobe.com/data-layers-buzzword-best-practice/) met variabelen voor alle product verwante gegevens (zoals product ID, hoeveelheid, prijs). Deze extensie werkt niet met op arrays gebaseerde gegevenslagen.
* De [&#x200B; uitbreiding van Adobe Analytics &#x200B;](../analytics/overview.md) moet worden geïnstalleerd.
