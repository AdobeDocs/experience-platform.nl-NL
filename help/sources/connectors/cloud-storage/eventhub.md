---
title: Azure Event Hubs Source Connector - Overzicht
description: Leer hoe u Azure Event Hubs met Adobe Experience Platform kunt verbinden via API's of de gebruikersinterface.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: b4d4bc7f-2241-482d-a5c2-4422c31705bf
source-git-commit: bad1e0a9d86dcce68f1a591060989560435070c5
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# [!DNL Azure Event Hubs] bron

>[!IMPORTANT]
>
>* De [!DNL Azure Event Hubs] -bron is in de broncatalogus beschikbaar voor gebruikers die Real-Time CDP Ultimate hebben aangeschaft.
>
>* U kunt nu de [!DNL Azure Event Hubs] -bron gebruiken wanneer u Adobe Experience Platform uitvoert op Amazon Web Services (AWS). Experience Platform die op AWS wordt uitgevoerd, is momenteel beschikbaar voor een beperkt aantal klanten. Meer over de gesteunde infrastructuur van Experience Platform leren, zie het [ multi-wolkenoverzicht van Experience Platform ](../../../landing/multi-cloud.md).

Adobe Experience Platform biedt native connectiviteit voor cloudproviders zoals AWS, [!DNL Google Cloud Platform] en [!DNL Azure] . U kunt uw gegevens van deze systemen naar Experience Platform overbrengen.

Opslagbronnen in de cloud kunnen uw eigen gegevens naar Experience Platform brengen zonder dat ze hoeven te worden gedownload, opgemaakt of geüpload. Ingebedde gegevens kunnen worden opgemaakt als XDM JSON, XDM Parquet, of afgebakend. Elke stap van het proces is geïntegreerd in het Bronwerkschema. Met Experience Platform kunt u gegevens van [!DNL Event Hubs] in real-time invoeren.

## Schalen met [!DNL Event Hubs]

De schaalfactor van uw [!DNL Event Hubs] -instantie moet worden verhoogd als u gegevens met een hoog volume moet invoeren, de parallellisme moet verhogen of de snelheid van inname op Experience Platform moet verhogen.

### Hoger volume-gegevens opnemen

Het maximale gegevensvolume dat u van uw [!DNL Event Hubs] -account naar Experience Platform kunt verzenden, is momenteel 2000 records per seconde. Neem contact op met uw Adobe-vertegenwoordiger als u de schaal wilt verhogen en meer gegevens wilt invoeren.

### Parallelisme vergroten voor [!DNL Event Hubs] en Experience Platform

Parallelisme verwijst naar de gelijktijdige uitvoering van dezelfde taken op meerdere verwerkingseenheden om de snelheid en prestaties te verhogen. U kunt het parallellisme aan de [!DNL Event Hubs] zijde verhogen door verdeling te verhogen of door meer verwerkingseenheden voor uw [!DNL Event Hubs] rekening te verwerven. Zie dit [[!DNL Event Hubs]  document op het schrapen ](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-scalability) voor meer informatie.

Experience Platform moet het aantal taken in de bronconnector verhogen om te kunnen lezen vanaf uw [!DNL Event Hubs] -partities om de snelheid van inname aan de Experience Platform-zijde te verhogen. Nadat u het parallellisme aan de [!DNL Event Hubs] zijde hebt vergroot, neemt u contact op met uw Adobe-vertegenwoordiger om Experience Platform-taken op basis van uw nieuwe partitie te schalen. Dit proces is momenteel niet geautomatiseerd.

## Een virtueel netwerk gebruiken om verbinding te maken met [!DNL Event Hubs] en Experience Platform

U kunt een virtueel netwerk instellen om [!DNL Event Hubs] te verbinden met Experience Platform terwijl uw firewallmetingen zijn ingeschakeld. Aan opstelling een virtueel netwerk, hoofd aan dit [[!DNL Event Hubs]  document van de de netwerkregelreeks ](https://learn.microsoft.com/en-us/azure/event-hubs/network-security) en volg de hieronder vermelde stappen:

* Selecteer **probeert het** van het REST API paneel;
* Verifieer uw [!DNL Azure] rekening gebruikend uw geloofsbrieven in zelfde browser;
* Selecteer [!DNL Event Hubs] namespace, middelgroep, en abonnement dat u aan Experience Platform wilt brengen en dan **RUN** selecteren;
* Voeg in de JSON-hoofdtekst die wordt weergegeven de volgende Experience Platform-subnet toe onder `virtualNetworkRules` inside `properties` :


>[!IMPORTANT]
>
>U moet een steun van het lichaam maken JSON dat u ontvangt, alvorens `virtualNetworkRules` met subnet van Experience Platform bij te werken aangezien het uw bestaande IP het filtreren regels bevat. Anders, zullen de regels na de vraag worden geschrapt.


```json
{
    "subnet": {
        "id": "/subscriptions/93f21779-b1fd-49ee-8547-2cdbc979a44f/resourceGroups/ethos_12_prod_va7_network/providers/Microsoft.Network/virtualNetworks/ethos_12_prod_va7_network_10_19_144_0_22/subnets/ethos_12_prod_va7_network_10_19_144_0_22"
    },
    "ignoreMissingVnetServiceEndpoint": true
}
```

Zie de onderstaande lijst voor verschillende gebieden van Experience Platform-subnetten:

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

Zie het volgende [[!DNL Event Hubs]  document ](https://learn.microsoft.com/en-us/azure/event-hubs/network-security) voor meer informatie over de reeksen van de netwerkregel.

## Verbinden [!DNL Event Hubs] met Experience Platform

>[!NOTE]
>
>Nadat u een streaming gegevensstroom hebt gemaakt of bijgewerkt, moet u de gegevensinvoer kort na vijf minuten pauzeren om te voorkomen dat gegevens verloren gaan of dat gegevens verloren gaan.

In de onderstaande documentatie vindt u informatie over het tot stand brengen van een verbinding tussen [!DNL Event Hubs] en Experience Platform via API&#39;s of de gebruikersinterface:

### API&#39;s gebruiken

* [Creeer een de bronverbinding van de Hubs van de Gebeurtenis gebruikend de Dienst API van de Stroom](../../tutorials/api/create/cloud-storage/eventhub.md)
* [Streaming gegevens verzamelen met de Flow Service API](../../tutorials/api/collect/streaming.md)

### UI gebruiken

* [Creeer een de bronverbinding van de Hubs van de Gebeurtenis in UI](../../tutorials/ui/create/cloud-storage/eventhub.md)
* [Een gegevensstroom configureren voor een verbinding voor cloudopslag in de gebruikersinterface](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
