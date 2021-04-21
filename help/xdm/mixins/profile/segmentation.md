---
keywords: Experience Platform;thuis;populaire onderwerpen;schema;Schema;XDM;individueel profiel;gebieden;schema's;Schema's;segment;segmentLidmaatschap;segmentlidmaatschap;Schemaontwerp;kaart;Kaart;
solution: Experience Platform
title: Mengsel met gegevens over segmentlidmaatschap
topic-legacy: overview
description: Dit document biedt een overzicht van de mix Details segmentlidmaatschap.
exl-id: 4d463f3a-2247-4307-8afe-9527e7fd72a7
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# [!UICONTROL Segment Membership Details] mixen

>[!NOTE]
>
>De namen van verschillende mengsels zijn gewijzigd. Zie het document op [mixin naamupdates](../name-updates.md) voor meer informatie.

[!UICONTROL Segment Membership Details] is een standaardmix voor de  [[!DNL XDM Individual Profile] klasse](../../classes/individual-profile.md). De mix verstrekt één enkel kaartgebied dat informatie betreffende segmentlidmaatschap, met inbegrip van welke segmenten het individu tot, de laatste kwalificatietijd behoort, en wanneer het lidmaatschap geldig tot is.

>[!WARNING]
>
>Hoewel het veld `segmentMembership` handmatig aan uw profielschema moet worden toegevoegd met deze combinatie, moet u niet handmatig proberen dit veld te vullen of bij te werken. Het systeem werkt automatisch de `segmentMembership` kaart voor elk profiel bij aangezien de segmentatietaken worden uitgevoerd.

<img src="../../images/data-types/profile-segmentation.png" width="400" /><br />

| Eigenschap | Gegevenstype | Beschrijving |
| --- | --- | --- |
| `segmentMembership` | Kaart | A map object that describes the individu&#39;s segment membership. De structuur van dit object wordt hieronder in detail beschreven. |

Hier volgt een voorbeeld van een `segmentMembership`-kaart die door het systeem is gevuld voor een bepaald profiel. Segmentlidmaatschappen worden gesorteerd op naamruimte, zoals aangegeven door de sleutels op hoofdniveau van het object. De afzonderlijke sleutels onder elke naamruimte vertegenwoordigen vervolgens de id&#39;s van de segmenten waarvan het profiel lid is. Elk segmentobject bevat verschillende subvelden met meer informatie over het lidmaatschap:

```json
{
  "xdm:segmentMembership": {
    "AAM": {
      "04a81716-43d6-4e7a-a49c-f1d8b3129ba9": {
        "xdm:version": "15",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2019-04-26T15:52:25+00:00",
        "xdm:status": "existing",
        "xdm:payload": {
          "xdm:payloadBooleanValue": true,
          "xdm:payloadType": "boolean"
        }
      },
      "53cba6b2-a23b-454a-8069-fc41308f1c0f": {
        "xdm:version": "3",
        "xdm:lastQualificationTime": "2018-04-26T15:52:25+00:00",
        "xdm:validUntil": "2018-04-27T15:52:25+00:00",
        "xdm:status": "realized",
        "xdm:payload": {
          "xdm:payloadPropensityValue": 0.5,
          "xdm:payloadType": "propensity"
        }
      }
    },
    "Email": {
      "abcd@adobe.com": {
        "xdm:version": "1",
        "xdm:lastQualificationTime": "2017-09-26T15:52:25+00:00",
        "xdm:validUntil": "2017-12-26T15:52:25+00:00",
        "xdm:status": "exited"
      }
    }
  }
}
```

| Eigenschap | Beschrijving |
| --- | --- |
| `xdm:version` | De versie van het segment waarvoor dit profiel in aanmerking kwam. |
| `xdm:lastQualificationTime` | Een tijdstempel van de laatste keer dat dit profiel voor het segment kwalificeerde. |
| `xdm:validUntil` | Een tijdstempel waarin wordt aangegeven wanneer het segmentlidmaatschap niet langer geldig is. |
| `xdm:status` | Geeft aan of het segmentlidmaatschap is gerealiseerd als onderdeel van de huidige aanvraag. De volgende waarden worden geaccepteerd: <ul><li>`existing`: Het profiel maakte al deel uit van het segment voorafgaand aan de aanvraag en blijft bij het lidmaatschap.</li><li>`realized`: Het profiel voert het segment in als onderdeel van de huidige aanvraag.</li><li>`exited`: Het profiel verlaat het segment als deel van het huidige verzoek.</li></ul> |
| `xdm:payload` | Sommige segmentlidmaatschappen omvatten een lading die extra waarden beschrijft die direct met het lidmaatschap verband houden. Voor elk lidmaatschap kan slechts één lading van een bepaald type worden verstrekt. `xdm:payloadType` Hiermee wordt het type van de lading (`boolean`,  `number`,  `propensity`of  `string`) aangegeven, terwijl de eigenschap sibling de waarde voor het ladingstype bevat. |

Raadpleeg de openbare XDM-opslagplaats voor meer informatie over de mix:

* [Voorbeeld van vulling](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.example.1.json)
* [Volledig schema](https://github.com/adobe/xdm/blob/master/components/mixins/profile/profile-personal-details.schema.json)
