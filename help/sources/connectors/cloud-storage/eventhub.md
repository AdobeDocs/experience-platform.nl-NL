---
title: Azure Event Hubs Source Connector - Overzicht
description: Leer hoe u Azure Event Hubs met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
badgeUltimate: label="Ultieme" type="Positive"
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: 087100b23f95cef527a507fb11440467feb78c9e
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# [!DNL Azure Event Hubs] bron

>[!IMPORTANT]
>
>De [!DNL Azure Event Hubs] De bron is in de broncatalogus beschikbaar voor gebruikers die Real-time Customer Data Platform Ultimate hebben aangeschaft.

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, [!DNL Google Cloud Platform], en [!DNL Azure]. U kunt uw gegevens van deze systemen overbrengen naar Platform.

Met bronnen voor cloudopslag kunt u uw eigen gegevens overbrengen naar Platform zonder dat u deze hoeft te downloaden, opmaken of uploaden. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM Parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema. Met Platform kunt u gegevens van [!DNL Event Hubs] in real time.

## Schalen met [!DNL Event Hubs]

De schaalfactor van uw [!DNL Event Hubs] De instantie moet worden verhoogd als u gegevens met een hoog volume moet invoeren, parallellisme moet vergroten of de snelheid van het innameplatform moet verhogen.

### Hoger volume-gegevens opnemen

Het maximale gegevensvolume dat u van uw [!DNL Event Hubs] account aan Platform is 2000 records per seconde. Neem contact op met uw Adobe als u de schaal wilt verhogen en meer gegevens over het volume wilt invoeren.

### parallellisme vergroten op [!DNL Event Hubs] en platform

Parallelisme verwijst naar de gelijktijdige uitvoering van dezelfde taken op meerdere verwerkingseenheden om de snelheid en prestaties te verhogen. U kunt het parallellisme van de [!DNL Event Hubs] naast elkaar door verdeling te verhogen of door meer verwerkingseenheden voor uw [!DNL Event Hubs] account. Zie dit [[!DNL Event Hubs] document over schalen](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability) voor meer informatie .

Om de snelheid van opname op de kant van het Platform te verhogen, moet het Platform het aantal taken in de bronschakelaar verhogen om van uw te lezen [!DNL Event Hubs] partities. Als u eenmaal een verhoogd parallellisme hebt op de [!DNL Event Hubs] Neem contact op met uw vertegenwoordiger van de Adobe om de platformtaken op basis van uw nieuwe partitie te schalen. Dit proces is momenteel niet geautomatiseerd.

## Een virtueel netwerk gebruiken om verbinding te maken met [!DNL Event Hubs] naar platform

U kunt een virtueel netwerk instellen om verbinding te maken [!DNL Event Hubs] aan Platform terwijl het hebben van uw firewallmaatregelen toegelaten. Aan opstelling een virtueel netwerk, hoofd aan dit [[!DNL Event Hubs] netwerkregelsetdocument](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set#code-try-0) en voert u de volgende stappen uit:

* Selecteren **Probeer het** vanuit het REST API-deelvenster;
* Verifieer uw [!DNL Azure] account met uw referenties in dezelfde browser;
* Selecteer de [!DNL Event Hubs] namespace, middelgroep, en abonnement dat u aan Platform wilt brengen en dan selecteren **RUN**;
* In het lichaam JSON dat verschijnt, voeg volgende subnet van het Platform onder toe `virtualNetworkRules` binnenkant `properties`:


>[!IMPORTANT]
>
>Maak een back-up van de JSON-instantie die u ontvangt voordat u de update uitvoert `virtualNetworkRules` met subnet van het Platform aangezien het uw bestaande IP het filtreren regels bevat. Anders, zullen de regels na de vraag worden geschrapt.


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

Zie de lijst hieronder voor verschillende gebieden van Platform subnets:

### VA7: Noord-Amerika

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### NLD2: Europa

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
            "id": "/subscriptions/40bde086-46ad-44c3-afba-c306f54b64ec/resourceGroups/ethos_12_prod_nld2_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_nld2-vnet/subnets/ethos_12_prod_nld2_network_10_20_40_0_23"
        }, 
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

### AUS5: Australië

```json
{
  "properties": {
    "defaultAction": "Deny",
    "virtualNetworkRules": [
      {
        "subnet": {
          "id": "/subscriptions/1618ef18-9edc-48bf-88dd-61cc979629b5/resourceGroups/ethos_12_prod_aus5_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_aus5-vnet/subnets/ethos_12_prod_aus5_network_10_21_116_0_22"
        },
        "ignoreMissingVnetServiceEndpoint": true
      },
    ],
    "ipRules": []
  }
}
```

Zie het volgende [[!DNL Event Hubs] document](https://docs.microsoft.com/en-us/rest/api/eventhub/preview/namespaces-network-rule-set/create-or-update-network-rule-set) voor meer informatie over de reeksen van de netwerkregel.

## Verbinden [!DNL Event Hubs] naar platform

In de onderstaande documentatie vindt u informatie over de verbinding [!DNL Event Hubs] naar Platform met API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

* [Creeer een de bronverbinding van de Hubs van de Gebeurtenis gebruikend de Dienst API van de Stroom](../../tutorials/api/create/cloud-storage/eventhub.md)
* [Streaming gegevens verzamelen met de Flow Service API](../../tutorials/api/collect/streaming.md)

### UI gebruiken

* [Creeer een de bronverbinding van de Hubs van de Gebeurtenis in UI](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [Een gegevensstroom configureren voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
